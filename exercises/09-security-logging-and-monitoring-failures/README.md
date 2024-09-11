# `09` Security Logging and Monitoring Failures

**Security Logging and Monitoring Failures** refers to the lack of proper logging and monitoring of critical events in an application. When an application does not log important activities, such as attack attempts, or fails to monitor these logs effectively, attackers can go unnoticed. This increases the risk of a security breach without being detected.

Since we have already worked with the vulnerability [SQL Injection (GET/Search)](../08-cryptographic-failures/README.es.md), we will take advantage of this to verify if the application logs SQL injection attempts. The idea is to perform an SQL injection and then investigate whether the application logs these attempts or if it lacks an adequate monitoring system.

## Verifying SQL Injection Attempts in bWAPP

1. Select the vulnerability **SQL Injection (GET/Search)** and click "Hack."
2. Perform an SQL Injection attempt. In the search field, enter the following SQL Injection payload to test if the application is vulnerable:

    ```bash
    ' OR 1=1 #
    ```

3. Click on the Search button. If the application shows a different result or the entire table, it means it is vulnerable to SQL injection.

## Checking if the Application Logs the SQL Injection Attempt

Once the injection is performed, you need to verify if the application logs this attempt in any log files or if there is a monitoring system set up to detect this activity.

1. Check the log files on the server (if accessible). In many Linux systems, Apache server logs are located at:

    ```bash
    /var/log/apache2/access.log
    ```

    or

    ```bash
    /var/log/apache2/error.log
    ```

2. Open these files and look for entries related to your SQL injection attempt. If you find the entry with the SQL injection attempt, the system is logging, but it might not be generating alerts.

    ![image 1](../../.learn/assets/logs-revisition.png)

> ⚠ If you find logs without alerts in the system, this indicates that while the server is logging activities, it is not taking any proactive or preventive action in response to potential attacks. This is a significant issue in the category of Security Logging and Monitoring Failures, as it directly affects the organization’s ability to detect and respond to threats in real time.

If you achieved the expected results, congratulations! Proceed to the next lesson `-->`