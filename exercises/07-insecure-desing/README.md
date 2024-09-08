# `07` Insecure Design - Login Page

This exercise simulates an insecure design using the Broken Authentication vulnerability in bWAPP to demonstrate how a system without adequate security controls can be compromised. Although the **Insecure Design** vulnerability is not explicitly listed in bWAPP, it can be replicated with this vulnerability to illustrate how a lack of security in design can lead to critical issues.

1. Select the **Broken Authentication - Login Page** vulnerability for the guided activity and click "Hack." You will be redirected to a login page without adequate security measures.
2. Inspect the page elements using your browser's developer tools. Open the element inspector and locate the input fields of the authentication form.
3. Change the color of the input field to black to make the hidden authentication data visible.

![imagen 1](../../.learn/assets/editcolor.png)

By modifying the input color, you will see that the credentials for user **tonystark** with the password **"I am Iron Man"** are visible.

![imagen 2](../../.learn/assets/colorform.png)

4. Exploit the insecure design. Try logging in with these credentials. You should be able to access the system without restrictions, demonstrating the lack of security measures such as sensitive data encryption and robust authentication mechanisms.

![imagen 3](../../.learn/assets/successful.png)

With this step-by-step guide, we have learned to identify and exploit a vulnerability related to **Insecure Design** through weak user authentication design. This vulnerability highlights the importance of considering security from the design phase, as poor design cannot be fixed merely by implementing patches.

If you achieved the expected results, congratulations! Move on to the next lesson `-->`