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
