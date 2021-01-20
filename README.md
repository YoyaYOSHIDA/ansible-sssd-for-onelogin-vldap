# [ansible-sssd-for-onelogin-vldap](https://github.com/YoyaYOSHIDA/ansible-sssd-for-onelogin-vldap)

Ansible tasks to setup and enable SSSD client for OneLogin VLDAP(Virtual LDAP)

# Remark

Currently supporting `CentOS7` and `AmazonLinux2`. `CentOS8` will be supported in time.

# Preparation

## Create var file

```bash
# Host name specified on inventory file
INVENTORY_HOSTNAME=''

# Create var file from template
cp vars/onelogin_vldap/template.yaml vars/onelogin_vldap/${INVENTORY_HOSTNAME}.yaml

# Input parameters. Refer to comments for details.
vim vars/onelogin_vldap/${INVENTORY_HOSTNAME}.yaml
```

## Specify ldap_default_authtok

`ldap_default_authtok` : The authentication token of the default bind DN. Only clear text passwords are currently supported.

Refer to [sssd-ldap(5) - Linux man page](https://linux.die.net/man/5/sssd-ldap) for details.

```bash
vim vars/onelogin_vldap/ldap_default_authtok.yaml

# Input ldap_default_authtok
LDAP_DEFAULT_AUTHTOK: "<ldap_default_authtok>"
```

You should encrypt the file by `ansible-vault` for security.

```bash
ansible-vault encrypt vars/onelogin_vldap/ldap_default_authtok.yaml
```

# Run Playbook

```bash
# Example
ansible-playbook playbook/onelogin_vldap/onelogin_vldap_client_setup.yaml -i <INVENTORY> -l <SUBSET>
```

# After running Playbook

Test wether setup are done well. See [here](https://gist.github.com/YoyaYOSHIDA/fdd14c712aa0e308b5a3fd72722a02a0#tests) for example.

# Reference

- [amazonlinux2_sssd_configurations_for_onelogin_vldap.md](https://gist.github.com/YoyaYOSHIDA/3e6ce4a961533152f13fd11e6b3bee40)
    - AmazonLinux2 SSSD Configurations for OneLogin VLDAP(Virtual LDAP)
- [centos7_sssd_configurations_for_onelogin_vldap.md](https://gist.github.com/YoyaYOSHIDA/fdd14c712aa0e308b5a3fd72722a02a0)
    - CentOS7 SSSD Configurations for OneLogin VLDAP(Virtual LDAP)
- [centos8_sssd_configurations_for_onelogin_vldap.md](https://gist.github.com/YoyaYOSHIDA/c421313a762d553999e51e74f7b5e4cc)
    - CentOS8 SSSD Configurations for OneLogin VLDAP(Virtual LDAP)

