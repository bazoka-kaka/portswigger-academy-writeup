# Unprotected Admin Functionality

Resource: https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/access-control-apprentice/access-control/lab-unprotected-admin-functionality

1. Go to `/robots.txt`

   ```txt
   User-agent: *
   Disallow: /administrator-panel
   ```

2. Go there

   ![Unprotected Admin Func 01](/assets/unprotected-admin-func-01.png)

3. Delete carlos
