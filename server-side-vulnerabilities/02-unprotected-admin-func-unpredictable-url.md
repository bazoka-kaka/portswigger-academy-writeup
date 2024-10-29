# Unprotected Admin Functionality with Unpredictable URL

Resource: https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/access-control-apprentice/access-control/lab-unprotected-admin-functionality-with-unpredictable-url#

1. View page source
2. Go to Javascript section

   ```jsx
   <script>
   var isAdmin = false;
   if (isAdmin) {
      var topLinksTag = document.getElementsByClassName("top-links")[0];
      var adminPanelTag = document.createElement('a');
      adminPanelTag.setAttribute('href', '/admin-hs2fdt');
      adminPanelTag.innerText = 'Admin panel';
      topLinksTag.append(adminPanelTag);
      var pTag = document.createElement('p');
      pTag.innerText = '|';
      topLinksTag.appendChild(pTag);
   }
   </script>
   ```

3. Go to `/admin-hs2fdt`
4. Delete `carlos`
