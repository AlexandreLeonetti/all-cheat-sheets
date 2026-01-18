keywords :


FastAPI
from fastapi import Header, HTTPException
@app.get("/path")
def handler():
uvicorn main:app --host 0.0.0.0 --port 8000

“FastAPI handles request routing and authentication logic”
“Dependency injection via function parameters”
“ASGI, async-ready”


Infrastructure as Code

 3 keywords
Declarative
Idempotent
Versioned
One  sentence
“Infrastructure as Code means the infrastructure is reproducible, reviewable, and version-controlled like application code.”

Terraform.
terraform init
terraform plan
terraform apply

resource/module/state


Cloud & Réseau
Top 3 concepts
VPC (network boundary)
Ingress / Egress
Layer 4 vs Layer 7
Interview phrase
“Networking defines how traffic enters, moves inside, and exits the cloud.”



Cloudflare
⚡ Cloudflare
Top 3 keywords
Reverse proxy
CDN
Edge security



Top 3 features
DNS
WAF
DDoS protection
“Cloudflare sits in front of applications as an edge security and performance layer.”

Cloud Armor (waf)

Top 3 keywords
Layer 7 protection
Google Load Balancer integration
IP / rate-based rules

allow if request.path == "/"
deny if SQLi pattern detected

“Cloud Armor is GCP’s WAF attached to HTTP(S) Load Balancers.”


Firewall Rules
⚡ Firewall Rules
Top 3 concepts
Allow / deny
Source IP ranges
Least privilege
GCP example keywords
ingress
egress
health check ranges
Interview phrase
“Firewall rules restrict traffic at the network level.”

DNS Public

Top 3 record types
A / AAAA
CNAME
TXT (ACME, verification)

Top 3 keywords
Zone
Record
TTL


Certificats TLS/ACME
Top 3 keywords
HTTPS
Public key / private key

ACME

ACME example:
Let's Encrypt
DNS-01 challenge
HTTP-01 challenge

“ACME automates certificate issuance and renewal.”

Load Balancers

Top 3 concepts
Traffic distribution
Health checks
TLS termination
Top 3 types
L4 (TCP)
L7 (HTTP)
Global vs Regional


WAF

Top 3 attack types
SQL injection
XSS
Path traversal
Top 3 keywords
Rate limiting
Signature-based rules
Layer 7
Interview phrase
“A WAF protects applications from common HTTP-level attacks.”


Github Actions & Workflows.
Top 3 keywords
Workflow
Job
Step
Top 3 YAML elements
on: [push]
jobs:
  build:
uses: actions/checkout@v4
run: terraform apply
Interview phrase
“GitHub Actions automates CI/CD pipelines.”

Cloud Run Jobs ou GKE)

mécanismes d’authentification/autorisation
Fédération d’identité
Vault,
RBAC,
OPA)




notes :
A Pod is a running instance.
A Deployment is a controller that manages Pods.
