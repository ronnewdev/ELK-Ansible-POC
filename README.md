# ELK‑Ansible‑POC 🎯

Ansible-based Proof-of-Concept playbook to simplify deploying an ELK (Elasticsearch, Logstash, Kibana) stack quickly on remote hosts.

---

## 🔍 Project Overview

This repository contains an Ansible playbook and supporting inventory to install and configure an ELK stack in a single command. Ideal for testing, learning, or lightweight ELK setups:

- **Elasticsearch**: Installs and configures the cluster node.
- **Logstash**: Optional data processing pipeline.
- **Kibana**: Data visualization front end.
- Modularized into roles under `roles/`.

---

## 🚀 Prerequisites

Before use, ensure:

- Ansible is installed on your control machine.
- SSH access configured to target nodes.
- Python present on target hosts.
- Hosts defined in `inventory.ini` with correct SSH credentials.

---

## 🧩 Repository Structure

```
├── ansible.cfg         # Config file pointing to inventory and settings
├── inventory.ini       # Hosts/groups for ELK installation
├── site.yml            # Master playbook calling all roles
└── roles/              # Role-based structure for modular tasks
    ├── elasticsearch/  # Installs & configures Elasticsearch
    ├── logstash/       # Optional Logstash setup
    └── kibana/         # Installs Kibana
```

---

## ⚙️ How to Run

1. **Clone the repository**

```bash
git clone https://github.com/ronnewdev/ELK-Ansible-POC.git
cd ELK-Ansible-POC
```

2. **Adjust inventory**

Open `inventory.ini` and ensure hosts are correctly defined under `elk`, `logstash`, and `kibana` groups.

3. **Run the playbook**

```bash
ansible-playbook -i inventory.ini site.yml
```

You may prefix with `sudo` or use `--ask-become-pass` if elevated privileges are needed.

4. **Verify deployment**

- Elasticsearch should be accessible on port `9200`.
- Kibana on port `5601`.
- If Logstash is enabled, ensure it's listening or processing sample logs.

---

## 🛠️ Customization Tips

- Edit `ansible.cfg` to adjust SSH or become settings.
- Modify role defaults (`roles/*/defaults/main.yml`) to change versions, install paths, or config templates.
- To disable Logstash, comment out or remove it from `site.yml`.
- Ngrok, TLS certs, replication, and firewall rules can be added via additional role tasks.

---

## ✅ Sample Commands

```bash
# Install ELK stack using default config
ansible-playbook -i inventory.ini site.yml

# Install only Elasticsearch and Kibana (no Logstash)
ansible-playbook -i inventory.ini site.yml --skip-tags=logstash

# Run with verbose output
ansible-playbook -i inventory.ini site.yml -vv
```

---

## 📝 License & Contributions

- **License**: MIT
- Contributions & feedback welcome. Feel free to fork, raise issues, or submit PRs.

---

## ℹ️ Contact

Maintained by Ronald Newman (@ronnewdev) and contributors.

---

### 📘 Example `inventory.ini`

```ini
[elk]
elk-node1 ansible_host=192.168.1.10 ansible_user=ubuntu

[logstash]
logstash-node1 ansible_host=192.168.1.11 ansible_user=ubuntu

[kibana]
kibana-node1 ansible_host=192.168.1.12 ansible_user=ubuntu
```

---