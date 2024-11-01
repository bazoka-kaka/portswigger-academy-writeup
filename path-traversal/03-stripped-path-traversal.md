# Lab Writeup: File path traversal, traversal sequences stripped non-recursively

URL: https://portswigger.net/web-security/learning-paths/path-traversal/common-obstacles-to-exploiting-path-traversal-vulnerabilities/file-path-traversal/lab-sequences-stripped-non-recursively#

## Description

This lab contains a path traversal vulnerability in the display of product images.

The application strips path traversal sequences from the user-supplied filename before using it.

To solve the lab, retrieve the contents of the `/etc/passwd` file.

## Solution

1. Open in new tab one of the images e.g: `https://0a80000c03ffe99d885933f7004500eb.web-security-academy.net/image?filename=6.jpg`
2. Change the filename param to become `/etc/passwd` using burp repeater. Use double payload to bypass the traversal sequences stripped non-recursively. Here's the full path `/image?filename=....//....//....//etc//passwd`
3. Send the request, get all the file's contents and the challenge is solved

   ![Stripped Path Traversal](/assets/stripped-path-traversal.png)
