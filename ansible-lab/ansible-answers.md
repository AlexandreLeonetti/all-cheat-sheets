Excellent idea 👍
What you did for Kubernetes is **exactly the right learning strategy**, and Ansible fits **perfectly** with an active-recall format.

Below is a **compact but high-signal Ansible Active Recall set**, designed for:

* **fast memorization**
* **interview questions**
* **freelance DevOps screenings**
* **YAML + commands + concepts**

I’ll keep it **shorter than Kubernetes**, but **dense**.
Agentless means nothing is permanently installed on the target machines.
---

# 🧠 Ansible Speedrun — **Active Recall Question Set**

---

## 🔹 Core Concepts (Fundamentals)

> **What problem does Ansible solve?**
> → Configuration management and automation of systems

> **Is Ansible agent-based or agentless?**
> → Agentless (uses SSH / WinRM)

> **What language are Ansible playbooks written in?**
> → YAML

> **What is the Ansible control node?**
> → The machine where Ansible is executed from

> **What are managed nodes?**
> → The target machines Ansible configures

> **Which protocol does Ansible use by default on Linux?**
> → SSH

---

## 🔹 Inventory (Targets)

> **What is an inventory?**
> → A list of managed hosts and groups

> **Which file commonly defines the inventory?**
> → `inventory.ini` (or dynamic inventory)

> **How do you define a group in an inventory?**
> → `[group_name]`

> **How do you target multiple machines at once?**
> → Using groups

> **Where do host-specific connection details live?**
> → Inventory variables (host vars)

---

## 🔹 Playbooks (Structure)

> **What is a playbook?**
> → A YAML file defining automation logic

> **What is a play?**
> → A mapping between hosts and tasks

> **Which keyword defines which hosts are targeted?**
> → `hosts`

> **Which keyword defines a list of actions?**
> → `tasks`

> **Which keyword enables privilege escalation?**
> → `become`

> **In what order are tasks executed?**
> → Top to bottom

---

## 🔹 Tasks & Modules

> **What is a task?**
> → A single unit of work in a playbook

> **What executes the actual work in a task?**
> → A module

> **Are tasks declarative or imperative?**
> → Declarative (desired state)

> **Which module installs packages on Debian-based systems?**
> → `apt`

> **Which module manages files and directories?**
> → `file`

> **Which module copies static files?**
> → `copy`

> **Which module manages services?**
> → `service`

---

## 🔹 Variables & Templates

> **How are variables referenced in Ansible?**
> → `{{ variable_name }}`

> **What templating engine does Ansible use?**
> → Jinja2

> **What is the difference between `copy` and `template`?**
> → `template` supports variables, `copy` does not

> **Where can variables be defined?**
> → Playbooks, inventories, group_vars, host_vars

---

## 🔹 Handlers

> **What is a handler?**
> → A task triggered only when notified

> **When are handlers executed?**
> → At the end of a play

> **Typical use case for handlers?**
> → Restarting services after config changes

> **Why are handlers important?**
> → Avoid unnecessary restarts

---

## 🔹 Idempotency (VERY IMPORTANT)

> **What is idempotency?**
> → Running automation multiple times produces the same result

> **Why is idempotency important?**
> → Safety, repeatability, predictability

> **Are all Ansible tasks idempotent by default?**
> → No

> **Which tasks often break idempotency?**
> → `shell` and `command`

> **How do Ansible modules preserve idempotency?**
> → By checking current state before changing

---

## 🔹 Shell vs Modules (Interview favorite)

> **Why should `shell` be avoided when possible?**
> → It breaks idempotency

> **When is `shell` acceptable?**
> → When no suitable module exists

> **How can shell tasks be made idempotent?**
> → Using `creates` / `removes`

---

## 🔹 Privilege Escalation

> **How does Ansible run tasks as root?**
> → `become: true`

> **Does Ansible require root SSH login?**
> → No

> **What is the recommended SSH user pattern?**
> → Normal user + sudo

---

## 🔹 Commands (CLI Active Recall)

### Inspect / Test

> **Which command tests connectivity to hosts?**
> → `ansible all -m ping`

> **Which flag specifies an inventory file?**
> → `-i`

> **Which flag prompts for SSH password?**
> → `-k`

> **Which flag enables sudo?**
> → `-b`

---

### Playbooks

> **Which command runs a playbook?**
> → `ansible-playbook playbook.yml`

> **Which option shows detailed execution logs?**
> → `-v`, `-vv`, `-vvvv`

> **Which option runs in check (dry-run) mode?**
> → `--check`

---

## 🔹 Error Handling & Safety

> **What happens if a task fails by default?**
> → Playbook stops

> **Which keyword allows a task to fail without stopping execution?**
> → `ignore_errors: true`

> **Which keyword runs a task only when a condition is met?**
> → `when`

---

## 🔹 Ansible vs Kubernetes vs Terraform (Conceptual)

> **Ansible manages what layer?**
> → OS & application configuration

> **Is Ansible declarative or imperative?**
> → Declarative (state-driven)

> **What makes Ansible different from Terraform?**
> → Terraform manages infrastructure, Ansible manages configuration

---

## 🎯 Interview “killer” answers (memorize)

### What is Ansible?

> “Ansible is an agentless automation tool that uses idempotent playbooks to configure systems over SSH.”

### What is idempotency?

> “Idempotency means I can run the same playbook multiple times and always end up with the same system state.”

### Why avoid shell tasks?

> “Shell tasks are not idempotent by default and can introduce unintended side effects.”

---

## 🧠 Mental model (one-liner)

```
Inventory → who
Playbook → what
Tasks → steps
Modules → how
Variables → flexibility
Handlers → reactions
Idempotency → safety
```

---

## ⏱️ How long to master this set?

* First pass: **30–40 min**
* Second pass (active recall): **20 min**
* Third pass (next day): **10 min**

After that → **interview-ready**.

---

If you want next, I can:

* turn this into a **printable cheat sheet**
* map **each question to a mini lab**
* generate an **advanced Ansible set** (roles, includes, vault)

Just tell me 👌
