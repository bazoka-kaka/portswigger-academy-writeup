# Lab Writeup: 2FA simple bypass

URL: https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/authentication-apprentice/authentication/multi-factor/lab-2fa-simple-bypass#

## Description

This lab's two-factor authentication can be bypassed. You have already obtained a valid username and password, but do not have access to the user's 2FA verification code. To solve the lab, access Carlos's account page.

Your credentials: `wiener:peter` <br />
Victim's credentials `carlos:montoya`

## Solution

1. Login with `wiener:peter`, see the email, and enter the 2FA verification code. We can see that we're redirected to `/my-account?id=wiener` page

2. Now, login with `carlos:montoya`, without seeing the email, try to go to `/my-account?id=carlos` then the lab is solved
