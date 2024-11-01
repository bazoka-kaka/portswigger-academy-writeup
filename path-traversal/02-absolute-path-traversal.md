# Lab Writeup: File path traversal, traversal sequences blocked with absolute path bypass

URL: https://portswigger.net/web-security/learning-paths/path-traversal/common-obstacles-to-exploiting-path-traversal-vulnerabilities/file-path-traversal/lab-absolute-path-bypass#

## Description

This lab contains a path traversal vulnerability in the display of product images.

The application blocks traversal sequences but treats the supplied filename as being relative to a default working directory.

To solve the lab, retrieve the contents of the `/etc/passwd` file.

## Solution

1. Open in new tab one of the images e.g: `https://0a80000c03ffe99d885933f7004500eb.web-security-academy.net/image?filename=6.jpg`
2. Change the filename param to become `/etc/passwd` using burp repeater. Here's the full path `/image?filename=/etc/passwd`
3. Send the request, get all the file's contents and the challenge is solved

   ![Absolute Path Traversal](/assets/absolute-path-traversal.png)
