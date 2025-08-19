# Automated Log Cleanup & Service Restart (Ansible)

## Overview

This Ansible project automates the cleanup of old log files and ensures
that critical services remain stable by preventing disk overflows. It
checks disk usage, archives old logs, deletes them, and restarts
services only when necessary.

## Project Structure

    playbooks/
     ├── cleanup.yml
     └── roles/
         └── log_cleanup/
             ├── tasks/main.yml
             ├── handlers/main.yml
             └── vars/main.yml

## How to Run

1.  Clone or copy the project to your local machine.\

2.  Update your Ansible inventory file with target hosts. Example
    `inventory.ini`:

        [servers]
        your_server ansible_host=192.168.1.10 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa

3.  Run the playbook:

        cd playbooks
        ansible-playbook -i inventory.ini cleanup.yml

4.  By default:

    -   Logs older than 7 days from `/var/log/` will be archived into
        `/archive/logs/`.\
    -   Configured services (e.g., nginx) will be restarted only if logs
        were cleaned.

## Configuration

Modify the variables in `roles/log_cleanup/vars/main.yml`: -
`log_retention_days`: Number of days to keep logs (default: 7).\
- `archive_dir`: Directory to archive logs (default: `/archive/logs`).\
- `services_to_restart`: List of services to restart if logs are cleaned
(default: `nginx`).
