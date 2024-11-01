# Lab Writeup: File path traversal, simple case

URL: https://portswigger.net/web-security/learning-paths/path-traversal/reading-arbitrary-files-via-path-traversal/file-path-traversal/lab-simple

## Description

This lab contains a path traversal vulnerability in the display of product images.

To solve the lab, retrieve the contents of the `/etc/passwd` file.

## Solution

1. open an image in new tab e.g: `https://0ad500be03b7c1508216c42a002400cf.web-security-academy.net/image?filename=56.jpg`
2. Intercept the request using burp repeater and change `filename` param with `../../../etc/passwd`
3. You'll get all the passwords as response and the lab is solved

   ![Simple Path Traversal](/assets/simple-path-traversal.png)
