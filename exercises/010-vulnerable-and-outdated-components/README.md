# `10` Vulnerable and outdated components

The purpose of this exercise is to demonstrate how **outdated and vulnerable components** can be exploited to perform attacks such as Persistent Cross-Site Scripting (XSS). Using old or unpatched versions of software libraries, like an outdated version of jQuery or a poorly implemented input management system, makes it easier to exploit known vulnerabilities.

In this exercise, we will use the **Stored Blog** module in bWAPP to simulate how a vulnerable component allows for the injection and execution of malicious code, demonstrating the impact of not keeping software components up to date.

### Instructions

1. Select the **Cross Site Scripting Stored (Blog)** vulnerability and click "Hack." You will be redirected to a page with a field where users can leave comments.
2. Write the following JavaScript code to simulate an XSS attack:

    ```bash
    <script>alert('Persistent XSS works')</script>
    ```

3. Click **Publish** to save the comment.

![image 1](../../.learn/assets/script.png)

4. After publishing the comment, return to the blog page. Upon reloading the page, you will see that the malicious script is automatically executed, showing an alert with the message "Persistent XSS in Stored Blog". This behavior occurs because the comment was not properly validated or escaped before being stored and displayed, exposing the vulnerability.

![image 2](../../.learn/assets/scriptFunciona.png)

5. To assess the extent of the attack, create two or three new users in bWAPP. For example, create users named user, user1, and user2.

Each of these users can post their own malicious comment using code similar to the following:

```bash
<script>alert('XSS from user')</script> hello, I left a JS script
These malicious comments will be stored in the database and will be executed every time the blog page is accessed.
```

6. Verification as an administrator. Log in again as the administrator bee.
7. Go back to the blog page and review the comments posted by users user, user1, and user2. You will notice that each time the administrator views the comments, the injected JavaScript code is executed, displaying alerts corresponding to each comment.


If you achieved the expected results, congratulations! Proceed to the next lesson -->


