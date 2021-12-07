# Setup Instructions for Darkflame Universe (Google Cloud Setup)

The following is a guide to setting up a functioning Darkflame Universe server instance running in the cloud, which has several key benefits:

- These steps don't vary based on what kind of computer you have.
- You can easily start over if you mess up (just delete the instance).
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

Next, **TODO: Make a script which downloads and extracts the navmeshes from the repository and puts them into a local folder**. Put the resulting `navmeshes` folder into the `res/maps` folder in your resource directory.

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

Next, [sign up for an account with Google Cloud](https://cloud.google.com/). You should see this popup to let you know you've received $300 in trial credits:

![](../images/google-cloud-trial.png)