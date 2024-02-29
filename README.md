# snarkOS Ansible Deployment

This repository contains Ansible scripts for deploying snarkOS Aleo node as a systemd service on Ubuntu servers. It automates the process of installing required dependencies, setting up the Rust environment, building snarkOS from source, and configuring it to run as a validator node service.

## Prerequisites

Before you begin, ensure you have the following prerequisites met:

- **Ansible Installed**: You need Ansible installed on your control machine (the machine from which you are running the Ansible commands). For installation instructions, refer to the [official Ansible documentation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).
- **SSH Access**: SSH access to your target host(s) with an SSH key. The user should have `sudo` privileges without a password prompt. Ensure your SSH public key is added to the `~/.ssh/authorized_keys` file on the target host(s).
- **Target Hosts**: One or more Ubuntu servers where you wish to deploy snarkOS. Ensure these hosts have internet access for downloading necessary packages.

## Project Structure

```
snarkos-ansible/
│
├── inventory.ini                 # Inventory file with target host(s) information
│
├── vars/
│   └── snarkos_vars.yml          # Variable file with snarkOS configurations
│
└── playbooks/
    └── setup_snarkos.yml         # Main playbook for setting up snarkOS
```

## Configuration

1. **Inventory File**: Update the `inventory.ini` file with the IP addresses and SSH users of your target hosts. For example:

   ```
   [snarkos_hosts]
   192.168.1.100 ansible_user=ubuntu
   ```

2. **Variable File**: Customize `vars/snarkos_vars.yml` with your specific configurations, such as the validators list and any other parameters relevant to your deployment.

3. **SSH Configuration**: Ensure you can SSH into your target host(s) using the specified user without a password prompt. This usually involves setting up SSH keys and configuring `sudo` privileges.

## Deployment

To deploy snarkOS, follow these steps:

1. **Navigate to the Project Directory**: Open a terminal on your control machine and navigate to the root of the `snarkos-ansible` project.

2. **Execute the Playbook**: Run the following command to start the deployment:

   ```bash
   ansible-playbook -i inventory.ini playbooks/setup_snarkos.yml
   ```

3. **Monitor the Deployment**: Ansible provides real-time feedback during the deployment. Monitor the output for any errors or warnings.

## Post-Deployment

After successfully deploying snarkOS, you can manage the snarkOS service using systemd commands. For example:

- To check the status of the service: `sudo systemctl status validator`
- To start the service: `sudo systemctl start validator`
- To stop the service: `sudo systemctl stop validator`
- To enable the service to start on boot: `sudo systemctl enable validator`

## Troubleshooting

- **Permission Issues**: If you encounter permission issues, ensure the SSH user on your target hosts has `sudo` privileges without a password prompt.
- **Deployment Errors**: Increase the verbosity of the Ansible output with `-v`, `-vv`, or `-vvv` flags for more detailed information.

For more assistance, refer to the Ansible documentation and the snarkOS GitHub repository.