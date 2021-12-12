# Google Cloud Setup - Troubleshooting Guide

## Error: No such table Activity rewards! Fatal error, stacktrace...

Make sure you are running the Darkflame Universe server in the same working directory.

Instead of:

```
$: ~/DarkflameServer/build/MasterServer
```

You need to instead run:
```
cd ~/DarkflameServer/build
./MasterServer
```

## I can connect to the Account manager but not to the game!

Make sure your Firewall settings are correct. You may need to edit them such that both the TCP and UDP ports are open.

## I tried to write a file to the Google Cloud bucket but got a 403 Forbidden error!

This error occurs when the instance's service account does not have the correct permissions to write to the bucket.

Follow the steps below to configure the instance:

1. Go to the Google Cloud Console and navigate to the Compute Engine tab.
2. Select the instance and click `Stop`. This will temporarily shut down the server and stop the instance. You will be ablt to start it back up later.
3. Click the instance name in the list of instances to open up the details page, then click `Edit` at the top.
4. Scroll down to the subheading named `Access scopes` and select `Allow full access to all Cloud APIs`.
5. Click `Save` to save the changes.
6. Click `Start/Resume` to start the instance back up. Then run the commands from [Run the Server](./google-cloud-setup.md#run-the-server) again.

We've configured the instance and now we need to configure the bucket.

1. Scroll down to the bottom of the details page for the instance and copy the `Service Account` value.
2. Go back to the Storage view and open the details page for your bucket.
3. Move to the `Permissions` tab and click `Add`.
4. For the principal, paste the `Service Account` value from the previous step.
5. Under roles, add the role `Storage Object Viewer`, then click `Add another role` and add the role `Storage Object Creator`.
6. Back on the instance, run `rm -rf ~/.gsutil` to clear out any cached credentials.

Any file write commands should now work.
