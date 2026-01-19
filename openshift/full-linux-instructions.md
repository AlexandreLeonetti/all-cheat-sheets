Absolutely — here’s your **updated `.md` file** with the two real-world gotchas we hit:

✅ **RBAC gotcha** (developer can’t list nodes / cluster resources → switch to kubeadmin)
✅ **nginx gotcha** (standard `nginx` image crashes on OpenShift due to SCC/random UID → use `nginx-unprivileged`)

I kept it short, practical, and “copy-paste friendly”.

---

````md
For local OpenShift on Linux (x86_64) in 2026, the most reliable option **without using the Red Hat website** is **OKD via OpenShift Local (CRC)**.

OKD is the **upstream community distribution of OpenShift**, using the **same `oc` CLI, APIs, Routes, Projects, and SCC security model**, but **without requiring a Red Hat pull secret**.

---

# 🚀 OpenShift / OKD Ultra-Fast Tutorial (Linux, CRC)

✅ super simple  
✅ hands-on  
✅ 1–2 hours  
✅ focuses on *what matters in interviews*  
✅ includes UI + CLI (`oc`)  
✅ includes OpenShift-specific concepts (Projects / Routes / SCC)  
✅ **NO Red Hat website required**

You’ll finish with this sentence (and mean it):

> “I can deploy and operate apps on OpenShift using `oc` and the Web Console, I understand Projects, Routes, SCC, and I can debug rollouts and pod issues.”

---

# ✅ What you’ll learn (Minimum Viable OpenShift)

### ✅ OpenShift concepts (vs Kubernetes)

* **Project** = OpenShift “namespace + policies”
* **Route** = OpenShift way to expose HTTP apps (instead of Ingress)
* **Deployment / Rollouts** = controlled updates + rollback
* **SCC (Security Context Constraints)** = OpenShift security model (VERY interview)

### ✅ Skills you’ll actually use

* Deploy a web app
* Expose it with a **Route**
* Scale it
* Rollout / rollback
* Debug pods + events
* Understand why “random UID” containers fail on OpenShift

---

# 🧱 Part 0 — Install OpenShift Local (CRC) on Linux (20–30 min)

This guide assumes:
- Linux **x86_64** (Intel / AMD)
- Debian / Ubuntu / similar
- Hardware virtualization enabled (KVM)

## 0.1 Verify CPU architecture

```bash
uname -m
````

You **must** see:

```
x86_64
```

(OKD preset is not supported on ARM.)

---

## 0.2 Install virtualization dependencies (Debian)

```bash
sudo apt update
sudo apt install -y \
  qemu-kvm libvirt-daemon-system libvirt-clients \
  bridge-utils virt-manager dnsmasq-base \
  network-manager curl wget tar xz-utils
```

Enable libvirt:

```bash
sudo systemctl enable --now libvirtd
```

Add your user to required groups:

```bash
sudo usermod -aG libvirt,kvm $USER
newgrp libvirt
```

Verify libvirt works:

```bash
virsh list --all
```

---

## 0.3 Download CRC directly (NO Red Hat login)

Download CRC **directly from the public mirror**:

```bash
cd ~/Downloads
wget https://developers.redhat.com/content-gateway/rest/mirror/pub/openshift-v4/clients/crc/2.57.0/crc-linux-amd64.tar.xz
```

Install it:

```bash
tar -xf crc-linux-amd64.tar.xz
sudo mv crc-linux-*/crc /usr/local/bin/crc
sudo chmod +x /usr/local/bin/crc
crc version
```

---

## 0.4 Configure CRC to use OKD (no pull secret)

```bash
crc config set consent-telemetry no
crc config set preset okd
```

Run setup:

```bash
crc setup
```

You should see:

```
Your system is correctly setup for using CRC.
```

---

## 0.5 Debian-specific fix (IMPORTANT)

On Debian, **AppArmor blocks libvirt from reading VM disks inside `/home`**.

Move CRC storage once (recommended):

```bash
crc stop || true
crc delete -f

sudo mkdir -p /var/lib/crc
sudo mv ~/.crc /var/lib/crc/.crc
sudo chown -R $USER:$USER /var/lib/crc/.crc
ln -s /var/lib/crc/.crc ~/.crc
```

Fix SUID bit (required by CRC):

```bash
sudo chmod u+s ~/.crc/bin/crc-admin-helper-linux-amd64
```

---

## 0.6 Start the cluster (first boot is slow)

```bash
crc start
```

First boot can take **10–20 minutes**.
This is normal (certs, operators, etc.).

When finished, CRC prints:

* console URL
* kubeadmin password
* developer credentials

---

# 🌐 Part 1 — Access the OpenShift UI + Login (5 min)

Open the console:

```bash
crc console
```

Login as:

* **kubeadmin** (admin)
* or **developer / developer** (for practice)

---

# 🧠 Part 2 — Connect your CLI (`oc`) to the cluster (5 min)

Set up environment:

```bash
eval $(crc oc-env)
```

Login as developer:

```bash
oc login -u developer https://api.crc.testing:6443
# password: developer
```

---

## ⚠️ GOTCHA #1 — RBAC (developer cannot see cluster resources)

If you run:

```bash
oc get nodes
```

You may get:

```
Forbidden: User "developer" cannot list resource "nodes"
```

✅ That is normal: **developer is scoped to Projects only**.

**Fix (switch to admin when needed):**

```bash
oc login -u kubeadmin https://api.crc.testing:6443
# use password printed by `crc start`
oc get nodes
```

Then switch back to developer for app work:

```bash
oc login -u developer https://api.crc.testing:6443
```

---

# 🏗️ Part 3 — Your first OpenShift app (Projects + Deploy + Route)

## 3.1 Create a Project

```bash
oc new-project demo
```

**Interview sentence:**

> “A Project is a namespace plus OpenShift RBAC and policies.”

---

## 3.2 Deploy an app (IMPORTANT IMAGE CHOICE)

### ✅ Recommended nginx for OpenShift (works with SCC)

OpenShift runs containers with a **random UID** by default (restricted SCC).
Some Docker images (like the official `nginx`) can crash with permission errors.

Use the OpenShift-friendly image:

```bash
oc new-app docker.io/nginxinc/nginx-unprivileged:latest --name web
oc get pods -w
```

---

## ⚠️ GOTCHA #2 — Official nginx can CrashLoop on OpenShift (SCC / random UID)

If you deploy:

```bash
oc new-app docker.io/library/nginx:latest --name web
```

You might see:

* `CrashLoopBackOff`
* permission denied in logs

✅ Reason: the image expects to write to privileged paths that are not writable when running as a random non-root UID.

Debug quickly:

```bash
POD=$(oc get pod -l app=web -o name | head -n1)
oc logs $POD
oc describe $POD | tail -n 30
```

Fix (recommended): use `nginx-unprivileged` (above).

(Alternative admin fix: assign `anyuid` SCC to a service account — not recommended for real prod.)

---

# 🌍 Part 4 — Expose it (Routes = OpenShift core concept)

```bash
oc expose svc/web
oc get route
```

Test it:

```bash
curl http://$(oc get route web -o jsonpath='{.spec.host}')
```

**Key idea:**

> Route = OpenShift’s built-in HTTP entrypoint (Ingress alternative).

---

# 📈 Part 5 — Scale + Rollouts

Scale:

```bash
oc scale deploy/web --replicas=3
```

Rollout:

```bash
oc rollout status deploy/web
```

Upgrade:

```bash
oc set image deploy/web web=nginx:1.25
oc rollout status deploy/web
```

Rollback:

```bash
oc rollout undo deploy/web
```

---

# 🧯 Part 6 — Debugging (memorize these)

```bash
oc get pods
oc describe pod <pod>
oc logs <pod>
oc get events --sort-by=.metadata.creationTimestamp | tail -n 20
oc get route,svc,deploy
```

---

# 🔒 Part 7 — OpenShift Security (SCC)

List SCCs (admin recommended):

```bash
oc login -u kubeadmin https://api.crc.testing:6443
oc get scc
oc describe scc restricted
```

**Mental model:**

> OpenShift runs containers with a random UID enforced by SCC.
> Images that assume root often fail.

---

# 🧠 What OpenShift is (one-liner)

> **OpenShift is Kubernetes plus a platform layer: built-in routing, stricter security, image builds, and a full web console.**

---

# 🧹 Cleanup

```bash
oc delete project demo
crc stop
```

Restart anytime:

```bash
crc start
```

---

# ✅ You are done (Minimum Viable OpenShift)

If you can say these, you’re interview-ready:

* “Projects are namespaces plus policies + RBAC”
* “Routes expose apps instead of Ingress”
* “SCC explains why some containers fail”
* “As developer I’m project-scoped; kubeadmin can see nodes”
* “I can deploy, scale, rollback, and debug with `oc`”

---

**Next steps (optional):**

* Active recall Q&A for OpenShift
* Helm + ArgoCD on OpenShift
* OpenShift vs Kubernetes interview comparison

```

---

If you want, I can also add a tiny **“admin vs developer quick table”** at the top (who can run which commands) to make it even easier to remember.
::contentReference[oaicite:0]{index=0}
```
