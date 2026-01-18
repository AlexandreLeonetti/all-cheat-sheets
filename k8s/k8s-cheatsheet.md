# 0 Kubernetes speedrun

| Key                  | Meaning                                             |
| -------------------- | --------------------------------------------------- |
| `apiVersion`         | Which Kubernetes API version                        |
| `kind`               | What object this is (**Deployment, Service, Pod…**) |
| `metadata.name`      | Object name                                         |
| `metadata.namespace` | Where it lives                                      |



| Keyword               | Why it matters       |
| --------------------- | -------------------- |
| `containers`          | What actually runs   |
| `image`               | Docker image         |
| `ports.containerPort` | Exposed inside pod   |
| `env`                 | Configuration        |
| `resources`           | CPU / memory limits  |
| `command` / `args`    | Overrides entrypoint |


| Keyword                | Meaning               |
| ---------------------- | --------------------- |
| `replicas`             | Number of pods        |
| `selector.matchLabels` | How pods are selected |
| `template`             | Pod definition        |
| `labels`               | Glue of Kubernetes    |



| Keyword      | Meaning                             |
| ------------ | ----------------------------------- |
| `type`       | ClusterIP / NodePort / LoadBalancer |
| `selector`   | Which pods get traffic              |
| `port`       | Service port                        |
| `targetPort` | Pod port                            |


| Keyword            | Meaning         |
| ------------------ | --------------- |
| `host`             | DNS name        |
| `path`             | URL path        |
| `ingressClassName` | nginx / traefik |
| `tls`              | HTTPS           |


| Object      | Used for             |
| ----------- | -------------------- |
| `ConfigMap` | Non-sensitive config |
| `Secret`    | Passwords / tokens   |


| Probe            | Purpose             |
| ---------------- | ------------------- |
| `livenessProbe`  | Restart container   |
| `readinessProbe` | Remove from traffic |
| `startupProbe`   | Slow startups       |

| Keyword        | Meaning              |
| -------------- | -------------------- |
| `volumes`      | Storage definition  |
| `volumeMounts` | Mount inside container |

commands :

## 🔹 Cluster & context

```bash
kubectl config get-contexts
kubectl config use-context
kubectl cluster-info
```

---

## 🔹 Inspect resources (MOST USED)

```bash
kubectl get pods
kubectl get svc
kubectl get deploy
kubectl get all
```

With namespace:

```bash
kubectl get pods -n kube-system
```

---

## 🔹 Deep inspection (debugging)

```bash
kubectl describe pod my-pod
kubectl logs my-pod
kubectl logs my-pod -c container-name
```

🚨 **If something is broken → `describe` FIRST**

---

## 🔹 Apply & delete (YAML lifecycle)

```bash
kubectl apply -f app.yaml
kubectl delete -f app.yaml
```

Dry run:

```bash
kubectl apply -f app.yaml --dry-run=client
```

---

## 🔹 Exec into containers (VERY IMPORTANT)

```bash
kubectl exec -it my-pod -- sh
```

This is how you **debug live production containers**.

---

## 🔹 Scaling & rollout

```bash
kubectl scale deployment my-app --replicas=5
kubectl rollout status deployment my-app
kubectl rollout undo deployment my-app
```
kubectl get pods -o wide
kubectl get pods -w

---

## 🔹 Networking quick tests

```bash
kubectl port-forward pod/my-pod 8080:80
kubectl get ingress

---

# 🧠 1. Kubernetes YAML — **keywords you MUST recognize instantly**

When you open a YAML file, your brain should do this automatically:

> **What object is this? What does it create? How does traffic reach it? How does it run?**

---

## 🔹 Universal fields (in **almost every** YAML)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
  namespace: default
```

### Know these **by reflex**

| Key                  | Meaning                                             |
| -------------------- | --------------------------------------------------- |
| `apiVersion`         | Which Kubernetes API version                        |
| `kind`               | What object this is (**Deployment, Service, Pod…**) |
| `metadata.name`      | Object name                                         |
| `metadata.namespace` | Where it lives                                      |

If you **don’t understand these**, stop reading — nothing else makes sense.

---

## 🔹 Pod / Container level (this is CORE)

```yaml
spec:
  containers:
    - name: app
      image: nginx:1.25
      ports:
        - containerPort: 80
      env:
        - name: ENV
          value: prod
```

### 🚨 **Vital keywords**

| Keyword               | Why it matters       |
| --------------------- | -------------------- |
| `containers`          | What actually runs   |
| `image`               | Docker image         |
| `ports.containerPort` | Exposed inside pod   |
| `env`                 | Configuration        |
| `resources`           | CPU / memory limits  |
| `command` / `args`    | Overrides entrypoint |

If you understand **containers + image + env**, you already understand **50% of Kubernetes**.

---

## 🔹 Deployment (MOST COMMON object)

```yaml
kind: Deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
```

### 🔑 Critical concepts

| Keyword                | Meaning               |
| ---------------------- | --------------------- |
| `replicas`             | Number of pods        |
| `selector.matchLabels` | How pods are selected |
| `template`             | Pod definition        |
| `labels`               | Glue of Kubernetes    |

⚠️ **Labels are EVERYTHING**
Services, Deployments, Autoscalers all rely on them.

---

## 🔹 Service (networking 101)

```yaml
kind: Service
spec:
  type: ClusterIP
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 80
```

### Know these **cold**

| Keyword      | Meaning                             |
| ------------ | ----------------------------------- |
| `type`       | ClusterIP / NodePort / LoadBalancer |
| `selector`   | Which pods get traffic              |
| `port`       | Service port                        |
| `targetPort` | Pod port                            |

🧠 Mental model:

> **Service = stable IP → forwards traffic to Pods**

---

## 🔹 Ingress (how traffic enters cluster)

```yaml
kind: Ingress
spec:
  rules:
    - host: app.example.com
      http:
        paths:
          - path: /
```

### Must-know

| Keyword            | Meaning         |
| ------------------ | --------------- |
| `host`             | DNS name        |
| `path`             | URL path        |
| `ingressClassName` | nginx / traefik |
| `tls`              | HTTPS           |

---

## 🔹 Config & Secrets (REAL DevOps stuff)

### ConfigMap

```yaml
kind: ConfigMap
data:
  APP_ENV: prod
```

### Secret

```yaml
kind: Secret
type: Opaque
data:
  PASSWORD: cGFzcw==
```

| Object      | Used for             |
| ----------- | -------------------- |
| `ConfigMap` | Non-sensitive config |
| `Secret`    | Passwords / tokens   |

---

## 🔹 Health & reliability (INTERVIEW GOLD)

```yaml
livenessProbe:
  httpGet:
    path: /health
    port: 8080
readinessProbe:
```

| Probe            | Purpose             |
| ---------------- | ------------------- |
| `livenessProbe`  | Restart container   |
| `readinessProbe` | Remove from traffic |
| `startupProbe`   | Slow startups       |

---

# ⚙️ 2. Kubernetes **VITAL COMMANDS** (minimal & powerful)

You do **NOT** need 100 commands.

These **15** cover 90% of real work.

---

## 🔹 Cluster & context

```bash
kubectl config get-contexts
kubectl config use-context
kubectl cluster-info
```

---

## 🔹 Inspect resources (MOST USED)

```bash
kubectl get pods
kubectl get svc
kubectl get deploy
kubectl get all
```

With namespace:

```bash
kubectl get pods -n kube-system
```

---

## 🔹 Deep inspection (debugging)

```bash
kubectl describe pod my-pod
kubectl logs my-pod
kubectl logs my-pod -c container-name
```

🚨 **If something is broken → `describe` FIRST**

---

## 🔹 Apply & delete (YAML lifecycle)

```bash
kubectl apply -f app.yaml
kubectl delete -f app.yaml
```

Dry run:

```bash
kubectl apply -f app.yaml --dry-run=client
```

---

## 🔹 Exec into containers (VERY IMPORTANT)

```bash
kubectl exec -it my-pod -- sh
```

This is how you **debug live production containers**.

---

## 🔹 Scaling & rollout

```bash
kubectl scale deployment my-app --replicas=5
kubectl rollout status deployment my-app
kubectl rollout undo deployment my-app
```

---

## 🔹 Networking quick tests

```bash
kubectl port-forward pod/my-pod 8080:80
kubectl get ingress
```

---

# 🧠 3. Mental model you should internalize

```
Deployment → creates Pods
Pods → run Containers
Service → exposes Pods
Ingress → exposes Services
ConfigMap / Secret → config
```

If you can **draw this from memory**, you’re already junior-level.

---

# 🎯 4. What to memorize FIRST (priority order)

### Tier 1 (non-negotiable)

* `apiVersion / kind / metadata / spec`
* Deployment / Service / Pod
* `kubectl get / describe / logs / apply`
* Labels & selectors

### Tier 2 (very strong signal)

* ConfigMap / Secret
* Probes
* Resource limits
* Ingress basics

### Tier 3 (later)

* Volumes / PVC
* HPA
* RBAC
* Helm

---

# 🚀 Suggested **7-day fast-track**

If you want, I can give you:

* ✅ **Daily YAML drills**
* ✅ **Mini-projects (Deploy + expose + debug)**
* ✅ **Interview questions mapped to YAML lines**

Just tell me 👇
**“I want a 7-day Kubernetes speedrun”**
