# Lab: User role controlled by request parameter

## Description

This lab has an admin panel at `/admin`, which identifies administrators using a forgeable cookie.

Solve the lab by accessing the admin panel and using it to delete the user `carlos`.

You can log in to your own account using the following credentials: `wiener:peter`

## Solution

1. Login first with creds `wiener:peter`
2. If we go to `/admin` we're gonna see **"Admin interface only available if logged in as an administrator"**
3. Inspect the web page, go to cookies, change the value of `Admin` from `false` to `true`

   ![Website Cookies](/assets/user-role-controlled-params-01.png)

4. Reload the page, now you're able to see the admin page and delete user `carlos`
