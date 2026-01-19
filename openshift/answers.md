Absolutely — here’s a **Survival OpenShift / OKD Active Recall Set** in the **same style** as your Kubernetes one: short, sharp, interview-focused, and “muscle memory” commands.

---

# 🧠 OpenShift / OKD Speedrun — **Active Recall Question Set (Survival)**

*(Designed for interviews: concepts + commands + debugging + OpenShift-specific gotchas.)*

---

## 🔥 OpenShift Core Concepts — 25

> **What is OpenShift (1 sentence)?**
> → Kubernetes + a developer platform layer (Projects, Routes, SCC, Console, Operators)

> **What is OKD?**
> → The upstream community distribution of OpenShift (same `oc`, same APIs)

> **What is a Project in OpenShift?**
> → A namespace + policies/RBAC defaults around it

> **What command creates and switches to a new project?**
> → `oc new-project demo`

> **What command switches to an existing project?**
> → `oc project demo`

> **What command shows your current project?**
> → `oc project`

> **What is a Route?**
> → OpenShift’s built-in HTTP exposure mechanism (Ingress alternative)

> **What command exposes a Service as a Route?**
> → `oc expose svc/web`

> **What command lists Routes?**
> → `oc get route`

> **Why can a Route show “Application is not available”?**
> → The service has no healthy endpoints (pods down / CrashLoop / not Ready)

> **What is SCC (Security Context Constraints)?**
> → OpenShift security policy system controlling what pods are allowed to do

> **What is the #1 SCC behavior that breaks containers?**
> → Random UID / non-root execution by default (restricted SCC)

> **Typical symptom of SCC issues?**
> → `permission denied` writing to filesystem (e.g. `/var/cache`, `/var/run`)

> **Best fix for SCC permission issues (recommended)?**
> → Use an image designed for non-root (e.g. unprivileged images)

> **Alternate fix for SCC issues (admin decision)?**
> → Assign a different SCC (e.g. `anyuid`) to the ServiceAccount

> **What is ImageStream (OpenShift term)?**
> → A named abstraction that tracks image tags and can trigger deployments

> **Why can `oc new-app nginx` surprise you?**
> → It may use an OpenShift ImageStream / builder image instead of Docker Hub nginx

> **Builder image vs runtime image — difference?**
> → Builder images build then exit; runtime images run continuously

> **What is an Operator (OpenShift term)?**
> → A controller that installs/manages a platform component (like “apps managing apps”)

> **Where do you check if the cluster is healthy (operators)?**
> → `oc get clusteroperators` (admin)

> **What is “developer” user meant for?**
> → App work inside projects (project-scoped)

> **Why can developer not run `oc get nodes`?**
> → RBAC: nodes are cluster-scoped resources

> **What user can see nodes and SCCs on CRC?**
> → `kubeadmin` (cluster admin)

> **What is the OpenShift Web Console?**
> → Built-in UI to manage projects, workloads, routes, operators, etc.

---

## 🧠 RBAC Survival — 8 (you WILL get asked)

> **Why does `oc get nodes` return Forbidden for developer?**
> → Nodes are cluster-scoped; developer is project-scoped by RBAC

> **How do you switch to admin on CRC/OKD?**
> → `oc login -u kubeadmin https://api.crc.testing:6443`

> **How do you switch back to developer?**
> → `oc login -u developer https://api.crc.testing:6443`

> **What’s a “role” vs “clusterrole”?**
> → Role = namespace/project scoped; ClusterRole = cluster scoped

> **What’s the fastest way to grant access to a project?**
> → `oc adm policy add-role-to-user <role> <user> -n <project>` (admin)

> **What command shows who you are currently logged in as?**
> → `oc whoami`

> **What command shows which projects you can access?**
> → `oc get projects`

> **What does “No resources found” for projects usually mean?**
> → You don’t have access to any projects yet (RBAC)

---

## ⚙️ oc CLI — Survival Commands — 25

### 🔹 Cluster / identity

> **Connect your shell to CRC oc/kubeconfig context?**
> → `eval $(crc oc-env)`

> **Login quickly as developer?**
> → `oc login -u developer https://api.crc.testing:6443`

> **Who am I?**
> → `oc whoami`

> **Cluster info (API URL)?**
> → `oc cluster-info`

---

### 🔹 Project workflow

> **Create a project**
> → `oc new-project demo`

> **Switch project**
> → `oc project demo`

> **List projects you can access**
> → `oc get projects`

---

### 🔹 Deploy app quickly

> **Deploy from an image (recommended unprivileged nginx)**
> → `oc new-app docker.io/nginxinc/nginx-unprivileged:latest --name web`

> **List all core resources**
> → `oc get all`

> **Watch pods live**
> → `oc get pods -w`

> **Expose service via route**
> → `oc expose svc/web`

> **Get the route URL**
> → `oc get route`

> **Test route quickly**
> → `curl http://$(oc get route web -o jsonpath='{.spec.host}')`

---

### 🔹 Scale / rollout

> **Scale a deployment**
> → `oc scale deploy/web --replicas=3`

> **Check rollout status**
> → `oc rollout status deploy/web`

> **Change container image**
> → `oc set image deploy/web web=nginx:1.25`

> **Rollback deployment**
> → `oc rollout undo deploy/web`

---

### 🔹 Delete / cleanup

> **Delete everything in a project (safe lab reset)**
> → `oc delete all --all`

> **Delete project**
> → `oc delete project demo`

---

## 🧯 Debugging & Troubleshooting — 20 (most important section)

> **What is your “first command” when something fails?**
> → `oc get pods`

> **How do you see why a pod failed (events + details)?**
> → `oc describe pod <pod>`

> **How do you get logs from a pod?**
> → `oc logs <pod>`

> **How do you see recent cluster events in a project?**
> → `oc get events --sort-by=.metadata.creationTimestamp | tail -n 30`

> **What does CrashLoopBackOff usually mean?**
> → App starts then exits repeatedly (bad config, permissions, missing deps)

> **What’s the OpenShift-specific top cause of CrashLoop for “normal images”?**
> → SCC / random UID permissions issue

> **How do you quickly confirm SCC/permission issues?**
> → `oc logs <pod>` (look for `permission denied`)

> **What does “Application is not available” Route page usually mean?**
> → No healthy endpoints behind the Service (pods down / not ready)

> **How do you check if a Service has endpoints?**
> → `oc get endpoints web` (or `oc describe svc web`)

> **What if route exists but curl returns OpenShift error page?**
> → Fix the pod first; route is fine

> **How do you verify your service selector matches pods?**
> → `oc describe svc web` (check `Selector:` + pod labels)

> **How do you see the deployment configuration quickly?**
> → `oc describe deploy web`

> **How do you restart pods after a fix?**
> → `oc delete pod -l app=web`

> **Why would a pod be stuck Pending?**
> → Not enough resources / scheduling issues / node not ready / constraints

> **How do you see image pull errors?**
> → `oc describe pod <pod>` (look for ImagePullBackOff)

> **How do you check readiness failures?**
> → `oc describe pod <pod>` (readiness probe events)

> **Quick “is my app listening” debug approach?**
> → `oc rsh <pod>` then `curl localhost:<port>`

> **How do you open a shell in a container?**
> → `oc rsh <pod>`

> **What’s the OpenShift equivalent of `kubectl exec`?**
> → `oc rsh` (or `oc exec` also works)

> **What’s the fastest way to get “everything relevant” to your app?**
> → `oc get deploy,rs,po,svc,route -l app=web`

---

## 🔒 SCC & “nginx crash” — Active Recall — 10

> **Why does `docker.io/library/nginx` often crash on OpenShift?**
> → It assumes root/writable system dirs; OpenShift runs random non-root UID

> **What nginx image works reliably on OpenShift restricted SCC?**
> → `docker.io/nginxinc/nginx-unprivileged:latest`

> **What is the safe production fix: change SCC or change image?**
> → Change image (run as non-root)

> **What is the risky admin fix (for labs only)?**
> → Assign `anyuid` SCC to the ServiceAccount

> **Command to grant anyuid to default SA (admin)?**
> → `oc adm policy add-scc-to-user anyuid -z default -n demo`

> **After changing SCC, what do you do?**
> → Restart pods: `oc delete pod -l app=web`

> **How do you list SCCs?**
> → `oc get scc` (admin)

> **What’s the default SCC name in most clusters?**
> → `restricted`

> **What does “random UID” protect against?**
> → Containers relying on root, privilege escalation, unsafe filesystem writes

> **One-liner SCC explanation for interviews**
> → “OpenShift defaults to restricted SCC, runs pods as random non-root UID, so some images fail unless designed for it.”

---

## 🌐 Routes — Active Recall — 10

> **What OpenShift object exposes HTTP apps externally?**
> → Route

> **Command to expose a Service as a Route?**
> → `oc expose svc/web`

> **Command to list routes?**
> → `oc get route`

> **What does a Route point to?**
> → A Service

> **If Route exists but app not reachable, what do you check first?**
> → Pods health / endpoints behind Service

> **How do you test a Route quickly?**
> → `curl http://$(oc get route web -o jsonpath='{.spec.host}')`

> **Why is Route “OpenShift-native”?**
> → It integrates tightly with OpenShift router + platform defaults

> **How to delete a route?**
> → `oc delete route web`

> **What’s the Kubernetes equivalent concept?**
> → Ingress (but Route is built-in OpenShift approach)

> **One-liner Route explanation for interviews**
> → “Routes expose HTTP services externally, similar to Ingress but OpenShift-native.”

---

## 🧑‍💼 Admin vs Developer — 8 (quick memory)

> **Which user is project-scoped in CRC?**
> → `developer`

> **Which user is cluster-admin in CRC?**
> → `kubeadmin`

> **Developer can deploy apps in a project?**
> → Yes

> **Developer can list nodes?**
> → No

> **Developer can list SCCs?**
> → No

> **kubeadmin can see operators & nodes?**
> → Yes

> **Command to check operator health (admin)**
> → `oc get clusteroperators`

> **Command to view SCCs (admin)**
> → `oc get scc`

---

## ✅ “Say it in interviews” — 8 ready sentences

> **What is OpenShift?**
> → “OpenShift is Kubernetes plus a developer platform layer with built-in routing, stricter security, and a full web console.”

> **Projects vs namespaces?**
> → “Projects are namespaces plus OpenShift RBAC/policies and defaults.”

> **Routes vs Ingress?**
> → “Routes are OpenShift’s built-in way to expose HTTP services externally.”

> **Why do some images fail on OpenShift?**
> → “OpenShift runs containers as random non-root UID by default via SCC; images assuming root often fail.”

> **How do you debug an app not reachable via Route?**
> → “Check pods status, logs, events, and ensure the Service has endpoints.”

> **How do you rollback a bad deployment?**
> → “I use `oc rollout undo deploy/<name>`.”

> **Why developer can’t list nodes?**
> → “RBAC: nodes are cluster-scoped; developer is project-scoped.”

> **How do you prove you used OpenShift?**
> → “I used `oc new-project`, deployed apps, exposed with Routes, and debugged SCC-related permission crashes.”

---

If you want, I can also generate a **mini “OpenShift speedrun lab script”** (10 commands end-to-end) so you can re-run it in 2 minutes before an interview.
