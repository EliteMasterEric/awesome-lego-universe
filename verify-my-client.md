# Verifying My Client

So you've just downloaded what appears to be a Lego Universe client, but you don't know if it's the right one. Maybe it's too old? Is the download corrupted? Or worse, what if it's actually a virus?

Thankfully, there's a foolproof method to verify a client: Checksums.

## What is a checksum?

*Note: You can [skip this section](#basic-steps) if you don't care what a checksum is, I won't get offended.*

A checksum function is a procedure which takes some input data and generates an output string. The output string is always the same length, regardless of the length of the input string. The input data can be anything, including a string or a file.

The important thing to know is that if the input data is even the tiniest bit different, it will completely change the output string. See below.

[](!/images/checksum.png)

By the nature of the checksum function, it is basically impossible to intentionally create a file that even resembles, much less exactly matches, a given checksum. For SHA-256 (the checksum function we will be using in this guide), the odds that two files will have the same checksum is approximately...

1 in 4,300,000,000,000,000,000,000,000,000,000,000,000,000,000,000,000,000,000,000,000

Add on top of that the odds that the file isn't a garbled mess, on top of the odds that the file resembles a Lego Universe client...

## Basic Steps

I'll go over a tutorial for each computer in a moment, but simply put, you'll be performing the following steps:

* Start with the file containing the client (it should be a single .rar file)

### Valid Checksums

Here is a list of known valid 

## Windows

With how useful taking the checksum of a file is, it's really something that Windows should make easier to do. Just add it to the Properties panel or something!

### WORK IN PROGRESS

## MacOS

### WORK IN PROGRESS

## Linux

### WORK IN PROGRESS
