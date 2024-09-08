# `01` Broken Access Control - Insecure DOR (Change Secret)

**Broken Access Control** vulnerabilities occur in web applications when the controls that restrict access to resources or functionalities are not properly implemented. This allows attackers to bypass access restrictions, giving them the ability to view, modify, or interact with data or functionalities they should not have access to. In this exercise, we will attempt to exploit the **Insecure DOR** hack to modify the user parameter value in the request to change the secret of another account.


### **Create a New User**

1. Start the beebox virtual machine.
2. Access the bWAPP web interface from your browser using the IP address of the beebox machine.
3. **Create a new user**:
  - Create a user named geeks with the secret: secret test.  
  ![image 1](../../.learn/assets/usergeeks.png)
4. Log in to bWAPP:

```bash
- Username: bee
- Password: bug
```

### **Verification in MySQL**

1. Open the terminal in the Beebox VM.
2. Access MySQL using the following command:

```bash
mysql -u root -p
```

> 💡 The default password: `bug`

3. Select the bWAPP database:

```sql
USE bWAPP;
```

4. Verify that the user `geeks` and their "secret" have been created:

```sql
SELECT * FROM users;
```
  
![image 2](../../.learn/assets/mysqlsecrettest.png)

### **Modifying Another User's Secret**

1. Log back in as the default user `bee`.
2. Select the **Insecure DOR (Change Secret)** vulnerability and click "Hack".

   ![image 3](../../.learn/assets/hack.png)

3. Inspect the HTML Form.

   - Once on the "secret" change page, right-click on the field where the new "secret" is entered and select "Inspect" (or use the browser's developer tools).

   ![image 4](../../.learn/assets/htmlbeeuser.png)

4. Modify the Form Value.

   - In the inspected HTML code, locate the value of the hidden input field containing the value "bee".
   - Change this value to "geeks" so that when the form is submitted, it modifies the "secret" of the user geeks instead of the user bee.

   ![image 5](../../.learn/assets/htmlvalue.png)

5. Submit the Form:

   - Change the "secret" to hello geeks in the form and submit it.


### **Checking in the Database:**

1. Return to the MySQL terminal.
2. Verify that the "secret" of the user geeks has been modified:

    ```bash
    SELECT * FROM users;
    ```

> You should see that the "secret" has changed to hello geeks.

![image 6](../../.learn/assets/secretgeeks.png)


