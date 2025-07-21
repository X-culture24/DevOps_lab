
---

# **DevOps Lab Project**

## **Overview**

This project sets up a DevOps pipeline using **Ansible** and **Vagrant/Terraform** to automate:

* Infrastructure provisioning (local or cloud)
* Docker and Kubernetes-in-Docker (**Kind**) setup

> **Current stage:** Infrastructure + Ansible setup only
> Kubernetes deployment and CI pipeline (GitHub Actions) will be added in the next phase.

---

## **Directory Structure**

```
devops-lab/
├── ansible-env/               # Python virtual environment for Ansible (optional)
├── app.js                     # Node.js sample app (future deployment)
├── Dockerfile                 # Dockerfile for the app                  # (typo) duplicate of Dockerfile – consider deleting/fixing
├── Vagrantfile                # Vagrant setup for local testing
├── inventory.ini              # Ansible inventory (Vagrant SSH details)
├── setup.yml                  # Ansible playbook to install Docker & Kind
├── ci.yml                     # Placeholder for CI/CD pipeline (GitHub Actions)
├── deployment.yaml            # Kubernetes deployment manifest (future use)
├── service.yaml               # Kubernetes service manifest (future use)
├── package.json               # Node.js dependencies
├── package-lock.json          # Node.js lock file
├── LICENSE
└── README.md                  # Project documentation
```

---

## **Setup Instructions**

### **1️⃣ Clone the Repository**

```bash
git clone https://github.com/your-username/devops-lab.git
cd devops-lab
```

---

### **2️⃣ Provision Local VM (Vagrant)**

```bash
vagrant up
```

This will create an Ubuntu 18.04 VM with:

* Docker installed
* Kind installed
* `kubectl` installed

---

### **3️⃣ Configure VM with Ansible**

Activate your virtual environment (optional but recommended):

```bash
source ansible-env/bin/activate
```

Run the Ansible playbook:

```bash
ansible-playbook -i inventory.ini setup.yml
```

This will:

* Install **Docker**
* Install **Kind**
* Install **kubectl**
* Add `vagrant` user to the `docker` group

---

## **Inventory Example**

`inventory.ini`:

```ini
[local]
127.0.0.1 ansible_user=vagrant ansible_ssh_private_key_file=./.vagrant/machines/default/virtualbox/private_key ansible_port=2222 ansible_python_interpreter=/usr/bin/python3 ansible_ssh_common_args='-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null'
```

---

## **What’s Installed by Ansible**

| Tool    | Purpose                    |
| ------- | -------------------------- |
| Docker  | Container runtime          |
| Kind    | Kubernetes-in-Docker setup |
| Kubectl | Kubernetes CLI             |

---

## **Current Project Status**

| Stage                           | Status       |
| ------------------------------- | ------------ |
| Infrastructure                  | ✅ Done       |
| Ansible Provisioning            | ✅ Done       |
| Kubernetes Deployment           | ⬜ Next Phase |
| CI/CD Pipeline (GitHub Actions) | ⬜ Next Phase |

---

## **Future Steps**

* Deploy the Node.js app (`app.js`, `Dockerfile`) to Kind cluster
* Use `deployment.yaml` and `service.yaml` for Kubernetes deployment
* Configure **GitHub Actions** using `ci.yml`

---

## **Troubleshooting**

* **Vagrant Issues**:
  Run `vagrant reload` or `vagrant destroy && vagrant up`

* **Python / Ansible Issues**:
  If using Ubuntu 22.04+, use virtual environments to avoid `externally-managed-environment` errors:

```bash
python3 -m venv ansible-env
source ansible-env/bin/activate
pip install ansible
```

* **Docker not running?**

```bash
sudo systemctl start docker
```

---

## **Author**

**Lawrence Imani**

---

## **License**

MIT License

---


