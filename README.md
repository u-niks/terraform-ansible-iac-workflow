# 🚀 Terraform + Ansible End-to-End IaC Workflow

This project demonstrates how to combine **Terraform** and **Ansible** to build a complete Infrastructure as Code (IaC) workflow.

- ✅ Terraform → Provision infrastructure (AWS EC2 instances)
- ✅ Ansible → Configure software on provisioned instances
- ✅ Clean separation of concerns (best practice)

---

## Use:
- **Terraform** to provision infrastructure
- **Ansible** to configure and deploy software

⚠️ Avoid using Terraform provisioners to run Ansible (not recommended except for bootstrap cases)

---

## 🏗️ Architecture

Terraform → AWS Infrastructure → Outputs (Public IPs)
↓
Ansible Inventory
↓
Ansible Playbooks (Configuration)

---

## 🛠️ Tech Stack

- Terraform (IaC)
- Ansible (Configuration Management)
- AWS (EC2)
- SSH (Access mechanism)

---

## 📂 Project Structure
```
├── terraform/
│   ├── main.tf
│   ├── variables.tf
│   └── outputs.tf
│
├── ansible/
│   ├── inventory.ini
│   └── install_htop.yaml
│
└── README.md
```

---

## ⚙️ Prerequisites

- Terraform installed
- Ansible installed
- AWS CLI configured
- SSH key pair

---

## 🚀 Step-by-Step Setup

### 1️⃣ Provision Infrastructure with Terraform

```bash
cd terraform
terraform init
terraform apply
```

Terraform will create:

EC2 instances
SSH key mapping
Output public IPs


2️⃣ Create Ansible Inventory
Use Terraform output to populate:
[all]
<EC2_PUBLIC_IP_1>
<EC2_PUBLIC_IP_2>
<EC2_PUBLIC_IP_3>


3️⃣ Run Ansible Playbook
cd ansible
ansible-playbook -i inventory.ini -u ubuntu install_htop.yaml


📜 Example Playbook
```
---
- name: Install htop
  hosts: all
  become: yes
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install htop
      apt:
        name: htop
        state: present
```

---

✅ Key Concepts
Terraform

Declarative Infrastructure as Code
State management
Modular and reusable

Ansible

Agentless (SSH-based)
Idempotent execution
YAML-based playbooks

---

⚠️ Best Practices

✅ Keep Terraform and Ansible separate
✅ Use Terraform outputs for dynamic inventory
✅ Avoid provisioners unless necessary
✅ Use private networking + bastion host in production

---

🔮 Future Enhancements

Dynamic inventory using Terraform output JSON
Integration with CI/CD pipelines
Spacelift orchestration
Auto-trigger Ansible after Terraform apply
Use private subnets + bastion host

---

📌 Use Case
This project is ideal for:

DevOps engineers learning IaC
Automation workflows demonstration
AWS infrastructure + config setup labs
