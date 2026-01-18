

# 🧠 Kubernetes Speedrun — **Active Recall Question Set**

---

## 🔹 YAML — recognize instantly

> **Which four top-level fields appear in almost every Kubernetes YAML?**

> **Which field defines the Kubernetes API version used by this resource?**

> **Which field defines the type of Kubernetes object?**

> **Which field contains identifying information about the object?**

> **Which field defines the desired state of the object?**

---

## 🔹 Containers (runtime core)

> **Which keyword defines what actually runs inside a Pod?**

> **Which keyword specifies the Docker image to run?**

> **Which keyword defines environment variables for a container?**

> **Which keyword defines the port exposed inside the container?**

> **Which keyword defines CPU and memory requests and limits?**

> **Which keywords override the container entrypoint and arguments?**

> **Which keyword mounts storage inside a container filesystem?**

---

## 🔹 Deployment (lifecycle)

> **Which keyword controls how many Pods should be running?**

> **Which keyword defines the Pod specification inside a Deployment?**

> **Which keyword attaches key-value identifiers to resources?**

> **Which keyword tells a Deployment which Pods it manages?**

---

## 🔹 Service (networking)

> **Which keyword defines how a Service is exposed?**

> **Which keyword connects a Service to matching Pods?**

> **Which keyword defines the port exposed by the Service?**

> **Which keyword defines the port traffic is forwarded to inside the Pod?**

---

## 🔹 Ingress (entry point)

> **Which keyword defines the DNS name used to access the application?**

> **Which keyword defines the URL path routing rule?**

> **Which keyword specifies which Ingress controller handles this resource?**

> **Which keyword enables HTTPS configuration?**

---

## 🔹 Configuration

> **Which Kubernetes object stores non-sensitive configuration data?**

> **Which Kubernetes object stores sensitive data such as passwords or tokens?**

---

## 🔹 Health & reliability

> **Which probe restarts a container if it becomes unhealthy?**

> **Which probe removes a Pod from traffic if it is not ready?**

> **Which probe handles slow-starting applications?**

---

# ⚙️ kubectl — Active Recall

---

## 🔹 Inspect

> **Which command lists all Pods in the current namespace?**

> **Which command lists Services?**

> **Which command lists Deployments?**

> **Which command lists Ingress resources?**

> **Which command lists most resources at once?**

> **Which command lists Pods in a specific namespace?**

> **Which command shows extended Pod information like node and IP?**

> **Which command watches Pod changes in real time?**

---

## 🔹 Debug

> **Which command shows detailed information and events for a Pod?**

> **Which command shows logs for a Pod?**

> **Which command shows logs for a specific container inside a Pod?**

> **Which command opens a shell inside a running container?**

---

## 🔹 Lifecycle

> **Which command creates or updates resources from a YAML file?**

> **Which command deletes resources defined in a YAML file?**

> **Which command validates a YAML file without applying it?**

---

## 🔹 Rollout

> **Which command changes the number of replicas in a Deployment?**

> **Which command checks the rollout status of a Deployment?**

> **Which command rolls back a Deployment to a previous version?**

---

## 🔹 Networking

> **Which command forwards a local port to a Pod port for testing?**


