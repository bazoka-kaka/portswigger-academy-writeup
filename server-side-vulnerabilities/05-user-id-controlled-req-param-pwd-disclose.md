# Lab Writeup: User ID controlled by request parameter with password disclosure

## Description

This lab has user account page that contains the current user's existing password, prefilled in a masked input.

To solve the lab, retrieve the administrator's password, then use it to delete the user `carlos`.

You can log in to your own account using the following credentials: `wiener:peter`

## Solution

1. Log in with `wiener:peter` see that the URL is now `https://0ae0007c044d36ee83cc797100260095.web-security-academy.net/my-account?id=wiener`
2. Change the ID from the URL to `administrator` then inspect the password input

   ![Image 1](/assets/user-id-controlled-req-param-pwd-disclose-01.png)

   We can see that the password is `obnz9nydsroj7q2prgrg`

3. Logout and login with `administrator:obnz9nydsroj7q2prgrg`
4. Go to `/admin` and delete the user `carlos`
