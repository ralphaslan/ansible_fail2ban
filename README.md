# Ansible Fail2ban Automation

This project automates the installation and configuration of **Fail2ban** on Ubuntu servers using **Ansible**.  
It sets up SSH protection with the following defaults:

- **Max retries:** 5 failed login attempts  
- **Ban time:** 1 day (86400 seconds)  
- **Service:** SSH  

---

## Directory Structure
    ansible-fail2ban/
    ├── README.md
    ├── ansible.cfg
    ├── inventory/
    │   └── hosts.ini
    ├── playbooks/
    │   └── fail2ban.yml
    └── roles/
        └── fail2ban/
            ├── tasks/
            │   └── main.yml
            ├── templates/
            │   └── jail.local.j2
            ├── handlers/
            │   └── main.yml
            └── defaults/
                └── main.yml

---

## Prerequisites

- Ansible installed on your control machine  
- SSH access to your Ubuntu target hosts  
- Python installed on target machines (default for Ubuntu)

---

## Setup

1. **Clone this repository:**
   ```bash
   git clone https://github.com/your-username/ansible-fail2ban.git
   cd ansible-fail2ban

---

2. **Update your inventory file:**

- Edit inventory/hosts.ini and add your target server(s):
    ```ini
    [ubuntu_servers]
    server1 ansible_host=192.168.1.100 ansible_user=ubuntu

---

3. **Check Ansible connection:**
    ```bash
    ansible -i inventory/hosts.ini all -m ping

---

4. **Run the playbook:**
    ```bash
    ansible-playbook -i inventory/hosts.ini playbooks/fail2ban.yml

## Customization

- You can modify default variables in roles/fail2ban/defaults/main.yml:
    ```yaml
    fail2ban_maxretry: 5
    fail2ban_bantime: 86400
    fail2ban_ignoreip: 127.0.0.1/8

## Verification

- After running the playbook, verify Fail2ban status on the target server:
    ```bash
    sudo systemctl status fail2ban
    sudo fail2ban-client status sshd