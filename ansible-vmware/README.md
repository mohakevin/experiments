# Ansible VMware + Private Cloud Inventory

This folder is configured to pull inventory from VMware and a static private cloud list,
then run commands across all hosts.

## Setup

1. Install the VMware collection:

   ```bash
   ansible-galaxy collection install -r requirements.yml
   ```

2. Export VMware credentials:

   ```bash
   export VMWARE_HOST='vcenter.example.com'
   export VMWARE_USER='administrator@vsphere.local'
   export VMWARE_PASSWORD='your-password'
   ```

3. Update `inventory/private_cloud.ini` with your private cloud hosts and SSH details.

## Inventory

The default inventory is configured in `ansible.cfg` to use both:

- `inventory/vmware.yml` (VMware dynamic inventory plugin)
- `inventory/private_cloud.ini` (static list)

## Run a command

```bash
ansible-playbook playbooks/run-command.yml -e "command=uptime"
```
