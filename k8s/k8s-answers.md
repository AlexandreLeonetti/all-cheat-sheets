

# 🧠 Kubernetes Speedrun — **Active Recall Question Set**

---

## 🔹 YAML — recognize instantly - 30

> **Which four top-level fields appear in almost every Kubernetes YAML?**
> → `apiVersion`, `kind`, `metadata`, `spec`

> **Which field defines the Kubernetes API version used by this resource?**
> → `apiVersion`

> **Which field defines the type of Kubernetes object?**
> → `kind`

> **Which field contains identifying information about the object?**
> → `metadata`

> **Which field defines the desired state of the object?**
> → `spec`

---

## 🔹 Containers (runtime core)

> **Which keyword defines what actually runs inside a Pod?**
> → `containers`

> **Which keyword specifies the Docker image to run?**
> → `image`

> **Which keyword defines environment variables for a container?**
> → `env`

> **Which keyword defines the port exposed inside the container?**
> → `ports.containerPort`

> **Which keyword defines CPU and memory requests and limits?**
> → `resources`

> **Which keywords override the container entrypoint and arguments?**
> → `command` / `args`

> **Which keyword mounts storage inside a container filesystem?**
> → `volumeMounts`

---

## 🔹 Deployment (lifecycle)

> **Which keyword controls how many Pods should be running?**
> → `replicas`

> **Which keyword defines the Pod specification inside a Deployment?**
> → `template`

> **Which keyword attaches key-value identifiers to resources?**
> → `labels`

> **Which keyword tells a Deployment which Pods it manages?**
> → `selector.matchLabels`

---

## 🔹 Service (networking)

> **Which keyword defines how a Service is exposed?**
> → `type`

> **Which keyword connects a Service to matching Pods?**
> → `selector`

> **Which keyword defines the port exposed by the Service?**
> → `port`

> **Which keyword defines the port traffic is forwarded to inside the Pod?**
> → `targetPort`

---

## 🔹 Ingress (entry point)

> **Which keyword defines the DNS name used to access the application?**
> → `host`

> **Which keyword defines the URL path routing rule?**
> → `path`

> **Which keyword specifies which Ingress controller handles this resource?**
> → `ingressClassName`

> **Which keyword enables HTTPS configuration?**
> → `tls`

---

## 🔹 Configuration

> **Which Kubernetes object stores non-sensitive configuration data?**
> → `ConfigMap`

> **Which Kubernetes object stores sensitive data such as passwords or tokens?**
> → `Secret`

---

## 🔹 Health & reliability

> **Which probe restarts a container if it becomes unhealthy?**
> → `livenessProbe`

> **Which probe removes a Pod from traffic if it is not ready?**
> → `readinessProbe`

> **Which probe handles slow-starting applications?**
> → `startupProbe`

---

# ⚙️ kubectl — Active Recall - 20

---

## 🔹 Inspect

> **Which command lists all Pods in the current namespace?**
> → `kubectl get pods`

> **Which command lists Services?**
> → `kubectl get svc`

> **Which command lists Deployments?**
> → `kubectl get deploy`

> **Which command lists Ingress resources?**
> → `kubectl get ingress`

> **Which command lists most resources at once?**
> → `kubectl get all`

> **Which command lists Pods in a specific namespace?**
> → `kubectl get pods -n <namespace>`

> **Which command shows extended Pod information like node and IP?**
> → `kubectl get pods -o wide`

> **Which command watches Pod changes in real time?**
> → `kubectl get pods -w`

---

## 🔹 Debug

> **Which command shows detailed information and events for a Pod?**
> → `kubectl describe pod my-pod`

> **Which command shows logs for a Pod?**
> → `kubectl logs my-pod`

> **Which command shows logs for a specific container inside a Pod?**
> → `kubectl logs my-pod -c container`

> **Which command opens a shell inside a running container?**
> → `kubectl exec -it my-pod -- sh`

---

## 🔹 Lifecycle

> **Which command creates or updates resources from a YAML file?**
> → `kubectl apply -f app.yaml`

> **Which command deletes resources defined in a YAML file?**
> → `kubectl delete -f app.yaml`

> **Which command validates a YAML file without applying it?**
> → `kubectl apply -f app.yaml --dry-run=client`

---

## 🔹 Rollout

> **Which command changes the number of replicas in a Deployment?**
> → `kubectl scale deployment my-app --replicas=5`

> **Which command checks the rollout status of a Deployment?**
> → `kubectl rollout status deployment my-app`

> **Which command rolls back a Deployment to a previous version?**
> → `kubectl rollout undo deployment my-app`

---

## 🔹 Networking

> **Which command forwards a local port to a Pod port for testing?**
> → `kubectl port-forward pod/my-pod 8080:80`

---

