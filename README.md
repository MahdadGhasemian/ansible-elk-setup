# Ansible ELK Setup

This repository provides a **fully automated Ansible playbook** to set up the ELK stack (Elasticsearch, Logstash, and Kibana) along with Docker prerequisites.

It is inspired by the [docker-elk](https://github.com/deviantony/docker-elk) project, which provides Docker Compose files and configurations for ELK. This repository makes the deployment **variable-driven and fully automated using Ansible**, making it easier to deploy ELK on any Linux server.

## Features

- Automated installation of Docker and Docker Compose requirements.
- Configurable ELK stack setup using Ansible variables.
- Supports multiple environments through inventory variables.
- Reusable and easily extendable for custom ELK configurations.

## Usage

**1. Clone this repository:**

```bash
git clone https://github.com/MahdadGhasemian/ansible-elk-setup.git
cd ansible-elk-setup
```

**2. Create your inventory file:**

Copy the example inventory file and customize it for your environment:

```bash
cp inventory-example.yml inventory.yml
```

Edit `inventory.yml` and configure:
- **Host settings**: Update `ansible_host`, `ansible_user`, and `ansible_ssh_private_key_file` to match your server
- **Passwords**: Generate secure passwords for all ELK components using the command below
- **Encryption keys**: Generate encryption keys for Kibana using the command below
- **Proxy settings** (optional): Configure if your environment requires a proxy

### Generating Secure Passwords and Keys

For password fields (elastic_password, logstash_internal_password, etc.), generate random 64-character strings:

```bash
tr -cd a-zA-Z0-9 </dev/urandom | head -c "64" ; echo ""
```

For encryption key fields (xpack_security_encryptionKey, xpack_encryptedSavedObjects_encryptionKey, xpack_reporting_encryptionKey), generate 32-byte hex strings:

```bash
openssl rand -hex 32
```

Run each command multiple times to generate unique values for each field.

**3. Check connectivity to your hosts:**

```bash
ansible-playbook playbooks/check_connection.yml -i inventory.yml
```

**4. Run the setup playbook three times:**

```bash
# First run: Setup Docker
ansible-playbook playbooks/setup.yml -i inventory.yml --tags docker-setup
# Second run: Run ELK initial setup
ansible-playbook playbooks/setup.yml -i inventory.yml --tags elk-setup
# Third run: Start all ELK services
ansible-playbook playbooks/setup.yml -i inventory.yml --tags elk-main
```

**5. Access Kibana in your browser:**

<http://192.168.1.100:5601/>