Perfect — this is **exactly the right way** to approach it 👍
You already did the hard work; now we **optimize for ROI**.

Below is a **curated “Survival List” of 25 questions** that a **senior OpenShift / DevOps** candidate should absolutely be comfortable with.
If you know **these**, you will survive **90% of OpenShift interviews**.

Think of this as **Tier-1 memory**.
Everything else from your big set becomes **Tier-2 / reference**.

---

# 🧠 OpenShift / OKD — **SURVIVAL Active Recall (Top 25, Highest ROI)**

## 🔥 Platform fundamentals (mental model)

> **What is OpenShift (one sentence)?**
> → Kubernetes **plus a platform layer**: Projects, Routes, SCC, Web Console, Operators

> **What is OKD?**
> → The upstream community distribution of OpenShift (same `oc`, same APIs)

> **What is a Project in OpenShift?**
> → A namespace **plus RBAC, policies, and defaults**

> **Why is OpenShift stricter than Kubernetes?**
> → Security-first defaults (SCC, non-root, RBAC)

---

## 🌍 Networking / exposure (Routes = interview gold)

> **What object exposes HTTP apps in OpenShift?**
> → **Route**

> **Route vs Ingress (one line)?**
> → Route is OpenShift-native HTTP exposure (Ingress equivalent)

> **Command to expose a Service as a Route?**
> → `oc expose svc/web`

> **What does “Application is not available” mean on a Route page?**
> → No healthy endpoints behind the Service (pods down / not Ready)

> **First thing you check when a Route doesn’t work?**
> → Pod status + logs (not the Route itself)

---

## 🔒 Security (SCC — the #1 differentiator)

> **What is SCC?**
> → Security Context Constraints: policies controlling what pods are allowed to do

> **Default SCC behavior that breaks containers?**
> → Pods run as **random non-root UID**

> **Typical symptom of SCC issues?**
> → `permission denied` writing to filesystem

> **Why does `docker.io/nginx` often crash on OpenShift?**
> → Assumes root / writable system paths → blocked by SCC

> **Best production fix for SCC-related crashes?**
> → Use images designed for non-root (unprivileged images)

> **Admin-only workaround (labs only)?**
> → Assign `anyuid` SCC to the ServiceAccount

---

## 🧑‍💼 RBAC / access (you *will* be asked this)

> **Why can developer not run `oc get nodes`?**
> → Nodes are cluster-scoped; developer is project-scoped (RBAC)

> **Which user is cluster-admin on CRC/OKD?**
> → `kubeadmin`

> **Which user is meant for app work?**
> → `developer`

> **How do you switch users quickly?**
> → `oc login -u kubeadmin|developer https://api.crc.testing:6443`

---

## ⚙️ Hands-on credibility (must-know commands)

> **Command to create and switch to a project?**
> → `oc new-project demo`

> **Fastest way to deploy an app from an image?**
> → `oc new-app <image> --name app`

> **How do you debug a failing app (order)?**
> → `oc get pods` → `oc logs` → `oc describe pod` → `oc get events`

> **How do you rollback a bad deployment?**
> → `oc rollout undo deploy/<name>`

> **How do you restart pods after a fix?**
> → `oc delete pod -l app=<name>`

---

## 🧠 Image behavior (OpenShift-specific gotcha)

> **Why can `oc new-app nginx` surprise you?**
> → It may use an ImageStream / builder image instead of Docker Hub nginx

> **Builder image vs runtime image?**
> → Builder builds then exits; runtime runs continuously

---

## 🎯 If you can answer THESE, you’re safe

If you can confidently explain:

* **Projects**
* **Routes**
* **SCC / random UID**
* **RBAC difference between developer and admin**
* **Why nginx crashed**
* **How you debug + rollback**

👉 You are **already above average** for OpenShift interviews.

---

## How to use this list (important)

* This **25-question list** = **daily quick review**
* Your **100+ question set** = **deep reference**
* Don’t memorize commands blindly — **say the answers out loud**

A very strong interview sentence for you would be:

> “I’ve used OKD locally with CRC, deployed apps with `oc`, exposed them using Routes, and debugged SCC-related permission crashes.”

That sentence alone signals **real OpenShift experience**.

---

If you want next, I can:

* compress this into a **1-page printable sheet**
* simulate a **real senior OpenShift interview**
* or map **these questions → real interview answers**

Just tell me which one 👌
