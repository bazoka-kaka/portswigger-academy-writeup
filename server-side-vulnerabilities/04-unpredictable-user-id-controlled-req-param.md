# Lab Writeup: User ID controlled by request parameter, with unpredictable user IDs

## Description

This lab has a horizontal privilege escalation vulnerability on the user account page, but identifies users with GUIDs.

To solve the lab, find the GUID for `carlos`, then submit his API key as the solution.

You can log in to your own account using the following credentials: `wiener:peter`

## Solution

1. Login to `wiener:peter`
2. Go to one of the pages whose writer is carlos

   ![Unpredictable User ID Controlled Req Param 01](/assets/unpredictable-id-req-param-01.png)

3. click on carlos and you're gonna see the user id in the url param `https://<your_id>.web-security-academy.net/blogs?userId=eb1fa0a1-2a6e-4e0c-a670-05fff1050724`
4. Go to `/my-account` and change the ID to the above one `https://<your_id>.web-security-academy.net/my-account?id=eb1fa0a1-2a6e-4e0c-a670-05fff1050724`
5. Copy the API and submit the solution
