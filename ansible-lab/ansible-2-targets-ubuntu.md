Yes — **this setup is absolutely standard for Ansible learning and demos** 👍
It’s actually one of the **cleanest ways** to practice Ansible without cloud cost or VM overhead.

Below is a **simple, correct, copy-pasteable tutorial** that matches *real Ansible usage*.

---

# ✅ Mini-Tutorial: Ansible with 2 Linux targets via Docker

**Architecture**

```
MacBook Pro (Ansible control node)
        |
        | SSH
        |
+------------------+   +------------------+
|  linux1 (Docker) |   |  linux2 (Docker) |
|  Ubuntu + SSH    |   |  Ubuntu + SSH    |
+------------------+   +------------------+
```

---

## 1️⃣ Create 2 lightweight Linux machines (Docker)

We’ll use **Ubuntu + SSH**, which is very common.

### Step 1 — Run containers

```bash
docker run -d --name linux1 -p 2221:22 ubuntu:22.04 sleep infinity
docker run -d --name linux2 -p 2222:22 ubuntu:22.04 sleep infinity
```

---

### Step 2 — Install SSH + Python (required by Ansible)

```bash
docker exec -it linux1 apt update && apt install -y openssh-server python3 sudo
docker exec -it linux2 apt update && apt install -y openssh-server python3 sudo

# on control node if mac

docker exec -it linux1 sh -c "apt update && apt install -y openssh-server python3 sudo"
docker exec -it linux2 sh -c "apt update && apt install -y openssh-server python3 sudo"

```

Start SSH:

```bash
docker exec linux1 service ssh start
docker exec linux2 service ssh start
```

Set root passwords (lab only):

```bash
# password
docker exec -it linux1 passwd
docker exec -it linux2 passwd
```
# ✅ The cleanest fix: create an `ansible` user + sudo (standard practice)

This is *exactly how real companies run Ansible.*

## 1️⃣ Create the user in BOTH containers

Run these commands:

```bash
docker exec -it linux1 sh -c "useradd -m -s /bin/bash ansible && echo 'ansible:azerty' | chpasswd && usermod -aG sudo ansible"
docker exec -it linux2 sh -c "useradd -m -s /bin/bash ansible && echo 'ansible:azerty' | chpasswd && usermod -aG sudo ansible"
```

Then allow sudo without password (lab convenience):

```bash
docker exec -it linux1 sh -c "echo 'ansible ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/ansible && chmod 440 /etc/sudoers.d/ansible"
docker exec -it linux2 sh -c "echo 'ansible ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/ansible && chmod 440 /etc/sudoers.d/ansible"
```

✅ Now you have a stable user for Ansible.

---

## 2️⃣ Verify SSH works manually

```bash
ssh ansible@127.0.0.1 -p 2221
ssh ansible@127.0.0.1 -p 2222
```

Password: `azerty`

If these work → Ansible will work.
---

### Step 3 — Verify SSH works from your Mac

```bash
ssh root@localhost -p 2221
ssh root@localhost -p 2222
```

If this works, Ansible will work.

---

## 2️⃣ Create Ansible inventory (with SSH credentials)

### `inventory.ini`

```ini
[linux]
linux1 ansible_host=127.0.0.1 ansible_port=2221
linux2 ansible_host=127.0.0.1 ansible_port=2222

[linux:vars]
ansible_user=root
ansible_ssh_pass=YOUR_PASSWORD
ansible_python_interpreter=/usr/bin/python3
```

> ⚠️ Password auth is **OK for labs only**.
> In real life → SSH keys + Ansible Vault.

---

### Test connectivity

```bash
ansible -i inventory.ini linux -m ping -k
```

You should see:

```
SUCCESS => ping: pong
```

---

## 3️⃣ Run a real playbook on BOTH Linux targets

### `playbook.yml`

```yaml
- name: Ansible with 2 Linux targets
  hosts: linux
  become: true

  vars:
    demo_dir: /tmp/ansible-demo

  tasks:
    - name: Create demo directory
      file:
        path: "{{ demo_dir }}"
        state: directory
        mode: "0755"

    - name: Create a file with hostname
      copy:
        content: "Hello from {{ inventory_hostname }}\n"
        dest: "{{ demo_dir }}/hello.txt"
      notify: show handler message

  handlers:
    - name: show handler message
      debug:
        msg: "Handler triggered on {{ inventory_hostname }}"
```

Run it:

```bash
ansible-playbook -i inventory.ini playbook.yml -k
```

---

### Verify on each container

```bash
docker exec -it linux1 cat /tmp/ansible-demo/hello.txt
docker exec -it linux2 cat /tmp/ansible-demo/hello.txt
```

You’ll see different hostnames → **proof of templating + multi-host execution**.

---

## 4️⃣ Verify idempotency (VERY important)

Run the playbook **again**:

```bash
ansible-playbook -i inventory.ini playbook.yml -k
```

You should see:

```
changed=0
```

This confirms **idempotency**.

---

## 🧠 Why this setup is 100% standard

This lab uses **real Ansible fundamentals**:

✔️ Control node (Mac)
✔️ Managed nodes (Linux)
✔️ SSH transport
✔️ Inventory with multiple hosts
✔️ Variables
✔️ Handlers
✔️ Idempotent tasks

The *only* difference from production is:

* Docker containers instead of VMs
* Password instead of SSH key
