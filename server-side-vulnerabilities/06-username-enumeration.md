# Lab Writeup: Username enumeration via different responses

Lab URL: https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/authentication-apprentice/authentication/password-based/lab-username-enumeration-via-different-responses#

## Description

This lab is vulnerable to username enumeration and password brute-force attacks. It has an account with a predictable username and password, which can be found in the following wordlists:

[Candidate Usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames) <br />
[Candidate Passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)

To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.

## Solution

1. Open burpsuite and access the web page using proxy
2. Open the `/login` page then try to do the POST login request, then send the captured request to intruder also add the sign to `username`

   ![Username Enum 01](/assets/username-enum-01.png)

3. Copy the payload from `Candidate Usernames` above as payload, then start the attack
4. Search for the response that returns `Incorrect password`

   ![Username Enum 02](/assets/username-enum-02.png)

   In this case, the username is `apache`

5. Using the above username, change the sign from `username` to `password` then don't forget to change the value of username to the above username (`apache`), copy the payload from `Candidate Passwords` above, then start the attack

   ![Username Enum 03](/assets/username-enum-03.png)

   From the above image, we can see that the response is unique (`302`) we know now that the auth is `apache:jordan`

   We can try to login

   ![Username Enum 04](/assets/username-enum-04.png)
