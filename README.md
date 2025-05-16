# FINAL BOSS - The Ultimate Corporate Challenge

In this lab, you will face a seemingly large and vulnerable website belonging to the fictional **Umbrella Corporation**. Although it is full of false leads (SQLi, LFI, etc.), you must thoroughly analyze its structure, discover an exposed backup file, and exploit a misconfiguration in scheduled tasks to escalate privileges on a Windows system.

In this lab you will learn:

- Analyzing websites with multiple decoys
- Directory fuzzing and credential extraction
- Remote access via Evil-WinRM
- Privilege escalation in Windows using scheduled tasks
- Decoding base64-encrypted flags

<how-to-start>
   
## 🌱 How to start this lab

Follow these instructions to get started:

1. **Download the virtual machine** from this [link](https://storage.googleapis.com/cybersecurity-machines/final-boss-lab.ova).
2. **Import the machine** into your preferred virtualization manager (VirtualBox, VMware, etc.).
3. Once the machine is running, you can start the lab!
</how-to-start>

## 📄 Instructions

You are facing a web server belonging to **Umbrella Corporation**, a company with questionable cybersecurity practices. Your goal is to access the system with administrator privileges and obtain a hidden flag on the `Administrator` user's desktop.

1. **Discover the IP address of the Final Boss machine.**

2. **Investigate the website.**
   - Access it from your browser at `http://<IP>`.
   - Explore routes such as:
     - `index.php?page=home`
     - `index.php?page=about`
     - `index.php?page=contact`

3. **Fuzz for hidden directories.** Use tools like `gobuster` or `dirb`.

4. **Extract the credentials.**

5. **Connect to the machine using Evil-WinRM.** Use the discovered credentials to obtain a shell.

6. **Escalate privileges by editing a misconfigured script.**

7. **Find the final flag.** The flag is base64-encrypted. Use [CyberChef](https://gchq.github.io/CyberChef/) to decode it.

**Remember:** Not everything that looks vulnerable actually is. Learn to follow the real clues among the decoys.

Good luck, agent!
