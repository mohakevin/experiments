# Ansible account bootstrap

This folder contains a minimal playbook for creating a user, setting a predefined
password, and installing SSH credentials for login from another server.

## Files

- `site.yml`: main playbook.
- `vars/users.yml`: example variables for the account and SSH key.

## Usage

1. Generate a password hash (never store plaintext passwords in playbooks):

   ```bash
   python -c "import crypt, getpass; print(crypt.crypt(getpass.getpass(), crypt.mksalt(crypt.METHOD_SHA512)))"
   ```

2. Copy the hash into `vars/users.yml` under `account_password_hash`.
3. Replace `account_public_key` with the SSH public key from the server that
   should be able to log in (typically the contents of `~/.ssh/id_rsa.pub`).
4. Run the playbook:

   ```bash
   ansible-playbook -i <inventory> ansible/site.yml
   ```

## Notes

- The playbook sets the password with a hashed value and installs an SSH
  public key for key-based login.
- If you need certificate-based SSH authentication (SSH certificates), add a
  task to install the signed certificate file in the user's `.ssh` directory
  and update `AuthorizedKeysFile` in `sshd_config` as needed.
