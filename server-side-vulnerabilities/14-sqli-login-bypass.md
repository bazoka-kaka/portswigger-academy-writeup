# Lab Writeup: SQL injection vulnerability allowing login bypass

URL: https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/sql-injection-apprentice/sql-injection/lab-login-bypass#

## Description

This lab contains a SQL injection vulnerability in the login function.

To solve the lab, perform a SQL injection attack that logs in to the application as the `administrator` user.

## Solution

1. Go to login page `/login`
2. Enter the following payload as username `administrator' OR 1=1 --` and you can enter anything as password this will bypass the password so the user don't need a password. Here's the complete query would look like `SELECT * FROM users WHERE username = 'administrator'--' AND password = ''`
3. Login and the problem should be solved
