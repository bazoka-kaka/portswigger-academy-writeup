# Lab Writeup: Basic SSRF against another back-end system

URL: https://portswigger.net/web-security/learning-paths/ssrf-attacks/ssrf-attacks-common-ssrf-attacks/ssrf/lab-basic-ssrf-against-backend-system

## Description

This lab has a stock check feature which fetches data from an internal system.

To solve the lab, use the stock check functionality to scan the internal `192.168.0.X` range for an admin interface on port `8080`, then use it to delete the user `carlos`.

## Solution

1. View details on one of the objects in homepage
2. Click on "check stock" to do POST request against an API then send the request to burp intruder to find the right IP address that contains the admin API
3. Here's what the admin's the URL looks like `http://192.168.0.x:8080/admin` then set the x then bruteforce the ip range from `1-255` using burp intruder until we find the right IP

   ![Basic Other Backend SSRF 01](/assets/basic-other-backend-ssrf-01.png)

   From the above image we can see that the right IP is `http://192.168.0.209:8080/admin` then we can also see the delete link for carlos which is `http://192.168.0.209:8080/admin/delete?username=carlos`

4. Change the `stockApi` value with it then send. The challenge is now solved.

   ![Basic Other Backend SSRF 02](/assets/basic-other-backend-ssrf-02.png)
