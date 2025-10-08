# Ansible ELK Setup

```bash
ansible-playbook playbooks/check_connection.yml -i inventory.yml

# The setup playbook needs to be run twice
# First run performs one-time setup, second run ensures Elasticsearch and other services start properly.
ansible-playbook playbooks/setup.yml -i inventory.yml
ansible-playbook playbooks/setup.yml -i inventory.yml
```

<http://192.168.1.100:5601/>

This repository provides a **fully automated Ansible playbook** to set up the ELK stack (Elasticsearch, Logstash, and Kibana) along with Docker prerequisites.

It is inspired by the [docker-elk](https://github.com/deviantony/docker-elk) project, which provides Docker Compose files and configurations for ELK. This repository makes the deployment **variable-driven and fully automated using Ansible**, making it easier to deploy ELK on any Linux server.

## Features

- Automated installation of Docker and Docker Compose requirements.
- Configurable ELK stack setup using Ansible variables.
- Supports multiple environments through inventory variables.
- Reusable and easily extendable for custom ELK configurations.

## Usage

1. Clone this repository:

```bash
git clone https://github.com/MahdadGhasemian/ansible-elk-setup.git
cd ansible-elk-setup
```

2. Check connectivity to your hosts:

```bash
ansible-playbook playbooks/check_connection.yml -i inventory.yml
```

3. Run the setup playbook twice:

```bash
# First run performs one-time setup
# Second run ensures Elasticsearch and other services start properly
ansible-playbook playbooks/setup.yml -i inventory.yml
ansible-playbook playbooks/setup.yml -i inventory.yml
```

4. Access Kibana in your browser:

<http://192.168.1.100:5601/>