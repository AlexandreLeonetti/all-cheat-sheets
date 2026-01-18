

### YAML — recognize instantly

```text
apiVersion | kind | metadata | spec
```

### Containers (runtime core)

| Keyword               | Why it matters         |
| --------------------- | ---------------------- |
| `containers`          | What runs              |
| `image`               | Docker image           |
| `env`                 | Config                 |
| `ports.containerPort` | Internal port          |
| `resources`           | CPU / RAM              |
| `command` / `args`    | Override entrypoint    |
| `volumeMounts`        | Files inside container |

---

### Deployment (lifecycle)

| Keyword                | Meaning       |
| ---------------------- | ------------- |
| `replicas`             | Pod count     |
| `template`             | Pod spec      |
| `labels`               | Glue          |
| `selector.matchLabels` | Pod selection |

---

### Service (networking)

| Keyword      | Meaning                   |
| ------------ | ------------------------- |
| `type`       | ClusterIP / NodePort / LB |
| `selector`   | Target pods               |
| `port`       | Service port              |
| `targetPort` | Pod port                  |

---

### Ingress (entry point)

| Keyword            | Meaning         |
| ------------------ | --------------- |
| `host`             | DNS             |
| `path`             | URL             |
| `ingressClassName` | nginx / traefik |
| `tls`              | HTTPS           |

---

### Config

| Object      | Purpose           |
| ----------- | ----------------- |
| `ConfigMap` | Non-secret config |
| `Secret`    | Credentials       |

---

### Health

| Probe            | Purpose         |
| ---------------- | --------------- |
| `livenessProbe`  | Restart         |
| `readinessProbe` | Traffic control |
| `startupProbe`   | Slow start      |

---

## kubectl — irreducible command set

### Inspect

```bash
kubectl get pods
kubectl get svc
kubectl get deploy
kubectl get ingress
kubectl get all
```

```bash
kubectl get pods -n kube-system
kubectl get pods -o wide
kubectl get pods -w
```

---

### Debug

```bash
kubectl describe pod my-pod
kubectl logs my-pod
kubectl logs my-pod -c container
kubectl exec -it my-pod -- sh
```

---

### Lifecycle

```bash
kubectl apply -f app.yaml
kubectl delete -f app.yaml
kubectl apply -f app.yaml --dry-run=client
```

---

### Rollout

```bash
kubectl scale deployment my-app --replicas=5
kubectl rollout status deployment my-app
kubectl rollout undo deployment my-app
```

---

### Networking

```bash
kubectl port-forward pod/my-pod 8080:80
```

---


keyword questions :


Which field defines the Kubernetes API version used? → apiVersion
Which field defines the resource type? → kind
Which field contains identifying information about the object? → metadata
In which namespace does the object live? → metadata.namespace
What is the name of the object? → metadata.name
Where is the desired state of the object defined? → spec
metadata ? identity
spec     ? desired state
status   ? current state (read-only)





which keyword tells us the version of the k8 api version ? (apiVersion)
which keyword tells us the type of object defined ? (kind)
which keyword gives us the metadata about an object? (metadata)
where does the object live ? (metadata.namespace)
what is the object name ? (metadata.name)
whart are the object's specifications ? (spec)


command questions : 
