# Setup Instructions for Darkflame Universe (Google Cloud Setup)

The following is a guide to setting up a functioning Darkflame Universe server instance running in the cloud, which has several key benefits:

- These steps don't vary based on what kind of computer you have.
- You can easily start over if you mess up (just delete the instance).
- You can easily change the server's settings and manage it from anywhere.
- The server can continue to run even if you turn off your PC.

The downside to this method is that it does technically cost money. You will have to provide a payment method with Google. However, there is a one-year trial which gives $300 in credits, and the smallest instance is about $5 a month.

## WORK IN PROGRESS

## Table of Contents

1. [Setup Client Files](#setup-client-files)
2. [Unpack Client Files](#unpack-client-files)
3. [Setup Resource Directory](#setup-resource-directory)

## Setup Client Files

The first step in this process is setting up your client files. You will need a Lego Universe 1.10.64 client before continuing. Note that a link to a client cannot be provided in this guide for legal reasons, but Google should be able to help you.

Once you've obtained a client, [make sure it is good by validating the checksum](verify-my-client.md).

## Unpack Client Files

If you downloaded an unpacked client, you may skip this section and move onto [creating the server 'res' directory](#setup-resource-directory).

Darkflame Universe requires an unpacked client, both for setup and for play. An unpacked client can be distinguished by containing extra files and folders in the `res` folder in the client, such as the `macros`, `names`, `maps`, and `scripts`.

If these folders are missing, you will need to extract them from the client resource data.

**TODO: Write good instructions on running [pkextractor](https://github.com/lcdr/utils/blob/master/utils/pkextractor.pyw)**

## Setup Resource Directory

Once you have an unpacked client, you will need to retrieve several files from it, that the DLU server needs in order for it to work.Create a folder somewhere easy to remember, and follow these steps:

* Create a folder called `res`.
* Copy the `LEGO Universe/res/macros` folder into the `res` folder in your resource directory.
* Copy the `LEGO Universe/res/BrickModels` folder into the `res` folder in your resource directory.
* Copy the `LEGO Universe/res/names` folder into the `res` folder in your resource directory.
* Copy the `LEGO Universe/res/maps` folder into the `res` folder in your resource directory.
* Copy the `LEGO Universe/res/chatplus_en_us.txt` file into the `res` folder in your resource directory.
* Create a folder called `locale`.
* Copy the `LEGO Universe/locale/locale.xml` file  into the `locale` folder in your resource directory.

Next, **TODO: Write good instructions on running [fdb_to_sqlite](https://github.com/lcdr/utils/blob/master/utils/fdb_to_sqlite.py)**. This will create a file called `cdclient.sqlite`.

Next, **TODO: Create a script that will download and run the migration queries on the sqlite file**. This will update the database to fix several issues with its contents.

Next, [download the navmeshes from the repository](https://github.com/DarkflameUniverse/DarkflameServer/blob/main/resources/navmeshes.zip) and extract it. Put the resulting `navmeshes` folder into the `res/maps` folder in your resource directory.

Finally, move the corrected `cdclient.sqlite` file to the `res` folder in your resource directory, and rename it to `CDServer.sqlite`.

You should have a directory containing the following file structure.

```
|
|-res
  |-macros
    |- ...
  |-BrickModels
    |- ...
  |-names
    |- ...
  |-maps
    |-navmeshes
      |- ...
    |- ...
  |-chatplus_en_us.txt
  |-CDServer.sqlite
|-locale
  |-locale.xml
```

## Getting Started with Google Cloud

Google makes it very easy to set up a server instance in the cloud. First, [sign up for an account with Google Cloud](https://cloud.google.com/). You should see this popup to let you know you've received $300 in trial credits:

![](../images/google-cloud-trial.png)

Then, you can access your cloud account from the [Google Cloud Console](https://console.cloud.google.com/). Google has a LOT of powerful tools and resources, but most of them are designed for larger businesses and not relevant to this guide, so don't get overwhelmed.

Click on the `Compute Engine` tab, and then click on the `Create Instance` button to create a new VM instance.

* Name it if you like. The default regon and zone are fine.
* Select the machine type. The default is a 2-core, 4GB memory machine, which is way overkill for what we want. Select the series N1, machine type `f1-micro`, which at time of writing is currently priced at $4.88/month or $0.01/hour. Even this is more than what you need for a DLU server but smaller instances aren't available.
* Scroll to the bottom and click Create.

Once the instance is ready, click it, then click SSH to connect to your instance. You will then see a browser window containing a terminal.

Congratulations! What you've essentially done is reserve a tiny spot on Google's massive server farm, and created a Linux computer in it. We're going to build and install Darkflame Universe on here, and you and your friends will be able to connect and play the game.

## Configuring the Server's Firewall

Before we get started building the server, we need to configure the server's firewall. Follow these steps:

* Click 'Compute Engine' to move back to the Compute Engine homepage.
* Under Related Actions, click 'Set up Firewall rules'
* Click 'Create Firewall Rule' at the top.

We're going to create a set of Firewall rules that allow access to the server.

* Set the name to `darkflame-server`.
* Add `darkflame-server` to the list of target tags. We're going to assign this tag to our server later.
* Set the Source IPv4 ranges to `0.0.0.0/0`. This represents all IP addresses, meaning this rule will allow any incoming IP.
* Under Protocols and ports, check `TCP` and enter the string `1001, 2000, 2005, 3000-4000, 5000`. This will allow access to the auth server, master server, chat server, world servers, and account manager.

Now lets assign these rules to the server.

* Move back to the home of your Google Cloud project (which currently contains your cloud instance).
* Click 'Compute Engine'. You should see your `darkflame-instance` listed. Click on it.
* Click 'Edit' at the top.
* Scroll down to 'Network tags' and enter `darkflame-server`.
* Scroll to the bottom and click 'Save'.

## Setup the MySQL Database

Run these commands, one at a time, in order.

```
sudo apt-get update
sudo apt-get install -y python3 python3-pip build-essential gcc libssl-dev default-mysql-server zlib1g zlib1g-dev sqlite git gpg wget

# Install the latest cmake
sudo apt remove -y --purge --auto-remove cmake
pip3 install cmake --upgrade
export PATH="$HOME/.local/bin:$PATH"

# Allocate swap space so we don't run out of memory while building.
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
sudo swapon -s

sudo mysql -u root
```

The last command will start a MariaDB shell. Enter the following commands one at a time (be sure to change the password on the first line to something more secure):

```
CREATE OR REPLACE USER darkflame IDENTIFIED BY 'password';
CREATE OR REPLACE DATABASE darkflame;
EXIT;
```

You will now have an empty database ready for later.

## Download and Build the Server

Next, run these commands one at a time to download and build the server:

```
git clone --recursive https://github.com/DarkflameUniverse/DarkflameServer
cd DarkflameServer
chmod +x build.sh
./build.sh
```

Wait until the build process is complete. This will take a while. Go get a snack, watch some TV, or do something else while you wait. Just don't close the window, or you'll have to start the build all over again.

## Upload Resources

Next, we're going to upload the resources folder [we created earlier](#setup-resource-directory) to the proper location.

## Setup the Server

Now we're going to do the final configur

## Updating Darkflame Universe

In the future, updates will be release to DarkflameServer that will include bug fixes and potentially even new features. To update the server, you can run the following commands:

**TODO: Complete this.**

## Contributing

This guide is a work in progress and could use your help.
* Complete Google Cloud setup instructions.
* Rewrite instructions for running pkextractor on the client (should be easy for anyone to follow).
* Rewrite instructions for running fdb_to_sqlite to be easier to follow (should be easy for anyone to follow).
  - Maybe make an executable you can drag and drop the FDB onto?
* Rewrite instructions for running the migration queries on the SQLite to be easier to follow (should be easy for anyone to follow).
