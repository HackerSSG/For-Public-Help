# Step-by-Step Guide to Setting Up a VPS, Cockpit, and Kali Linux

## Step 1: Buy VPS
Purchase a VPS from Contabo:
- [Contabo VPS](https://contabo.com/en/vps/)

---

## Step 2: Install Cockpit
1. Install Cockpit and its modules:
    ```bash
    apt install cockpit
    apt install cockpit-podman
    systemctl start cockpit
    systemctl enable cockpit
    ss -antpl | grep 9090
    ```
2. Configure UFW (Uncomplicated Firewall):
    ```bash
    apt install ufw
    ufw status
    ufw enable
    ufw allow 9090
    ufw allow 80
    ufw allow 22
    ufw allow 3389
    ufw allow ssh
    ufw reload
    ufw status verbose
    ```

3. Edit the Cockpit configuration file:
    ```bash
    sudo nano /etc/cockpit/cockpit.conf
    ```
    Add the following:
    ```
    [WebService]
    AllowUnencrypted = true
    Login = root
    ```

4. Restart Cockpit:
    ```bash
    systemctl restart cockpit
    apt-get upgrade cockpit
    sudo apt-get install sscg
    sudo systemctl restart cockpit
    ```

5. Additional configurations:
    - Remove users from disallowed list:
      ```bash
      sudo nano /etc/cockpit/disallowed-users
      ```
    - Comment out restrictions in PAM:
      ```bash
      sudo nano /etc/pam.d/cockpit
      ```
      Find the line:
      ```
      pam_listfile.so item=user sense=deny
      ```
      and comment it out.

6. Add a new user:
    ```bash
    sudo adduser cyberssg
    sudo usermod -aG sudo cyberssg
    ```

7. Check Cockpit status:
    ```bash
    sudo systemctl status cockpit
    ```

8. Install Cockpit Navigator:
    ```bash
    sudo mkdir -p /etc/cockpit/ws-certs.d
    sudo rm /etc/cockpit/ws-certs.d/0-self-signed.cert
    sudo systemctl restart cockpit
    sudo ufw allow 9090/tcp
    sudo ufw allow 22/tcp
    sudo ufw reload
    wget https://github.com/45Drives/cockpit-navigator/releases/download/v0.5.10/cockpit-navigator_0.5.10-1focal_all.deb
    dpkg -i cockpit-navigator_0.5.10-1focal_all.deb
    ```

9. Access Cockpit Navigator:
    - Visit `https://<your-vps-ip>:9090/navigator`
![image](https://github.com/user-attachments/assets/a56e16b9-8de9-4006-bb58-67b78cc0b7e9)

---

## Step 3: Install Kali Linux
1. Add Kali Linux repository:
    ```bash
    nano /etc/apt/sources.list
    ```
    Add the following line:
    ```
    deb http://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware
    ```

2. Add the Kali Linux key:
    ```bash
    wget -q -O - https://archive.kali.org/archive-key.asc | gpg --dearmor > /etc/apt/trusted.gpg.d/kali-archive-keyring.gpg
    ```

3. Update and upgrade the system:
    ```bash
    apt update
    apt upgrade
    apt full-upgrade
    apt dist-upgrade
    ```

4. Install Kali Linux packages:
    ```bash
    apt -y install kali-linux-everything
    apt install kali-desktop-gnome
    sudo apt install -y kali-linux-default
    apt update --fix-missing
    apt --fix-broken install
    sudo apt-get install -f
    sudo dpkg --configure -a
    sudo apt -y install kali-root-login
    sudo passwd
    ```

5. Clean up unnecessary packages:
    ```bash
    apt autoremove
    apt clean
    apt --fix-broken install
    ```

---

## Step 4: Install and Configure RDP
1. Fix broken packages and install xrdp:
    ```bash
    apt --fix-broken install
    sudo apt install xrdp -y
    ```

2. Add user to necessary groups:
    ```bash
    sudo usermod -aG ssl-cert cyberssg
    sudo usermod -aG adm cyberssg
    sudo usermod -aG www-data cyberssg
    sudo usermod -aG sudo cyberssg
    sudo usermod -aG root cyberssg
    sudo usermod -aG systemd-journal cyberssg
    sudo usermod -aG users cyberssg
    ```

3. Configure firewall and iptables for RDP:
    ```bash
    sudo ufw allow 3389/tcp
    sudo ufw allow 22/tcp
    sudo ufw reload
    sudo iptables -A INPUT -p tcp --dport 3389 -j ACCEPT
    sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
    ```

4. Restart and enable xrdp:
    ```bash
    sudo systemctl restart xrdp
    sudo systemctl enable xrdp
    ```

---

If you need any help or have any questions, feel free to reach out to me on [LinkedIn](https://www.linkedin.com/in/muhammad-usman-481876252/). 

Also, don't forget to tag or credit me, **Hackerssg**, if this guide helped you in any way!

Thanks for reading and happy hacking!

---
