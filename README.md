Here's the README.md for your project:  


# SSH Remote Server Setup

This project demonstrates how to set up a basic remote Linux server and configure it to allow SSH connections using key pairs. Below are the steps I followed to complete this project.

---

## Steps Taken

### 1. Created an EC2 Instance on AWS
- Set up a new Ubuntu EC2 instance using the AWS Management Console.
- Configured the security group to allow inbound SSH connections (port 22).

### 2. Generated SSH Key Pair Locally
- Used the `ssh-keygen` command on my local machine to generate a new SSH key pair:
  ```bash
  ssh-keygen
  
- This generated a private key (`id_rsa`) and a public key (`id_rsa.pub`) stored in `~/.ssh/`.

### 3. Added the Public Key to the Server
- Connected to the EC2 instance using the default key provided by AWS and added my new public key to the server.
- Copied the contents of `id_rsa.pub` to the `~/.ssh/authorized_keys` file on the server:
  ```bash
  cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
  ```
- Set the correct permissions for the `.ssh` directory and `authorized_keys` file:
  ```bash
  chmod 700 ~/.ssh
  chmod 600 ~/.ssh/authorized_keys
  ```

### 4. Created a Configuration File for SSH
- Configured the SSH client on my local machine to simplify the connection process:
  - Created a configuration file `~/.ssh/config` with the following content:
    ```text
    Host ubuntuAWS
        HostName <server-ip>
        User ubuntu
        IdentityFile ~/.ssh/id_rsa
    ```

### 5. Connected to the Server Remotely
- Used the alias defined in the SSH configuration file to connect to the server:
  ```bash
  ssh ubuntuAWS
  ```

---

## Stretch Goal: Fail2Ban Installation
- Installed Fail2Ban to prevent brute-force attacks:
  ```bash
  sudo apt update
  sudo apt install fail2ban
  ```
- Configured Fail2Ban by editing the jail configuration file:
  ```bash
  sudo nano /etc/fail2ban/jail.local
  ```
- Restarted the Fail2Ban service:
  ```bash
  sudo systemctl restart fail2ban
  ```

---

This project is part of [Janis Adhikari's](https://roadmap.sh/projects/ssh-remote-server-setup)  DevOps projects.