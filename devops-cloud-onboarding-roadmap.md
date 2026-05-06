# DevOps & Cloud — New Member Onboarding Roadmap
### 2-Week Sprint · Practice First · AI-Accelerated

---

## Philosophy

> **Do > Read > Memorize.** Break things. Fix things. Ask AI why it broke.

- Every day = 1 core concept + 1 real hands-on lab + 1 AI challenge
- Theory is the minimum needed to start doing — go deeper only when blocked
- Use AI tools (Claude, Copilot, ChatGPT) as a senior pair-programmer, not as a copy-paste machine
- You must be able to explain what you did and why — not just show it works

**AI Rule of Thumb:**
- ✅ Use AI to explain an error you don't understand
- ✅ Use AI to generate boilerplate — then read every line and modify it
- ✅ Use AI to quiz you at the end of each day
- ❌ Do not use AI to skip the lab — the muscle memory is the point

---

## Skill Map

| Area | Tools | Priority |
|---|---|---|
| OS & Shell | Linux (Ubuntu), Bash | 🔴 Must |
| Containers | Docker, Docker Compose | 🔴 Must |
| Orchestration | Kubernetes, Helm | 🔴 Must |
| Cloud | AWS + GCP/Azure | 🔴 Must |
| IaC | Terraform | 🔴 Must |
| Monitoring | Prometheus, Grafana, CloudWatch | 🟡 Important |
| CI/CD | GitHub Actions | 🟡 Important |
| Problem-Solving | DSA mindset, debugging loops | 🟢 Good to have |

---

## Day-by-Day Sprint

---

### Day 1 — Linux OS & Shell Survival Kit

**Goal:** Navigate any Linux machine confidently. Understand processes, permissions, and logs.

**Core Concepts (30 min)**
- File system hierarchy: `/`, `/etc`, `/var`, `/tmp`, `/home`
- Permissions: `rwx`, `chmod`, `chown`, `sudo`
- Processes: `ps`, `top`, `htop`, `kill`, `systemctl`
- Logs: `journalctl`, `/var/log/`, `tail -f`
- Text tools: `grep`, `awk`, `sed`, `cat`, `less`, `find`

**Hands-on Lab**
1. Spin up a fresh Ubuntu VM (local or cloud)
2. Create a user, assign it a group, restrict sudo access
3. Write a bash script that: monitors disk usage every 10s and logs to a file when usage > 80%
4. Simulate a "high CPU" process, find it with `ps`/`htop`, and kill it gracefully then forcefully
5. Use `grep` + `awk` to extract the last 50 error lines from `/var/log/syslog`

**🤖 AI Challenge**
Paste a real error from your lab into Claude and ask:
> "Explain this Linux error to me. What caused it? How do I fix it? What should I know to prevent it?"
Then fix it yourself — no copy-pasting the solution directly.

**✅ Checkpoint — can you answer these?**
- What's the difference between `kill` and `kill -9`?
- A service is failing at startup. How do you diagnose it?
- You don't have permission to read a file. What are your options?

---

### Day 2 — Networking Fundamentals for DevOps

**Goal:** Understand how traffic flows. Diagnose connectivity issues without guessing.

**Core Concepts (30 min)**
- IP, subnets, CIDR notation (e.g. `10.0.0.0/24`)
- DNS: how resolution works, `/etc/hosts`, `dig`, `nslookup`
- TCP vs UDP, ports, sockets
- HTTP/HTTPS basics: status codes, headers, request/response
- Firewall: `ufw`, `iptables` basics, security groups

**Hands-on Lab**
1. Use `curl -v` to inspect an HTTP request/response end-to-end
2. Set up a simple Python HTTP server (`python3 -m http.server`), hit it with curl, watch with `tcpdump`
3. Configure `ufw` to allow only port 22 and 8080, block everything else — verify it works
4. Use `dig` to trace how `google.com` resolves. Then add a fake DNS entry in `/etc/hosts` and observe the override
5. Map out what happens network-wise when you run `kubectl apply` (conceptual — draw or describe)

**🤖 AI Challenge**
Give Claude this prompt:
> "Quiz me on networking concepts a DevOps engineer must know. Ask 5 questions, one at a time. Tell me if I'm right or wrong and explain why."

**✅ Checkpoint**
- A pod can't reach another service. What are your first 3 debugging steps?
- What does a `502 Bad Gateway` tell you?
- Your DNS change isn't propagating. What do you check?

---

### Day 3 — Docker: Containers from Scratch

**Goal:** Build, run, debug, and compose containers. Understand what Docker actually does under the hood.

**Core Concepts (30 min)**
- Container vs VM — what's actually different
- Image layers, caching, Dockerfile best practices
- Networking: bridge, host, none
- Volumes and bind mounts
- `docker-compose` for multi-container apps

**Hands-on Lab**
1. Pull `nginx`, run it, expose port 80, visit it in browser
2. Write a Dockerfile for a simple Node.js or Python app from scratch — no base bloat, multi-stage build
3. Use `docker exec` to get inside a running container and inspect it
4. Intentionally break the Dockerfile (wrong port, missing dependency) — fix it using logs
5. Write a `docker-compose.yml` with: app + Postgres + Redis. Make them communicate. Verify with `docker network inspect`

**🤖 AI Challenge**
Ask Claude:
> "Review my Dockerfile and tell me: any security issues? Any layer cache inefficiencies? How would you improve it?"
Paste your Dockerfile and apply at least 2 of its suggestions — then explain why those suggestions matter.

**✅ Checkpoint**
- What happens to data when a container is removed? How do you persist it?
- Why use multi-stage builds?
- Your container exits immediately after starting. How do you debug it?

---

### Day 4 — Kubernetes Fundamentals

**Goal:** Deploy and manage workloads on Kubernetes. Understand the control loop model.

**Core Concepts (30 min)**
- Architecture: control plane vs worker nodes, API server, etcd, kubelet
- Core objects: Pod, Deployment, ReplicaSet, Service, Namespace
- `kubectl` essential commands
- Labels, selectors, and why they matter
- Desired state vs actual state — the reconciliation loop

**Hands-on Lab**
Setup: use `minikube` or a free cluster (kind, k3s, or a cloud sandbox)

1. Deploy nginx as a Deployment with 3 replicas. Verify pods are running
2. Expose it as a `ClusterIP` service, then a `NodePort` — test both
3. Scale it to 5 replicas. Then force-delete one pod. Watch what happens
4. Roll out an update (new image tag). Then roll it back
5. Create two Namespaces (`staging`, `production`). Deploy the same app in both with different env vars using ConfigMaps

**🤖 AI Challenge**
Copy a failing `kubectl describe pod` output and ask Claude:
> "This Kubernetes pod is failing. Walk me through what each section of this output means and what the likely cause is."

**✅ Checkpoint**
- What's the difference between a Pod and a Deployment?
- A pod is stuck in `CrashLoopBackOff`. What do you do?
- How does a Service find the right pods?

---

### Day 5 — Kubernetes Advanced + Helm

**Goal:** Manage real-world Kubernetes configs. Package and template with Helm.

**Core Concepts (30 min)**
- ConfigMaps and Secrets (and why you don't commit secrets to git)
- Resource requests and limits
- Liveness and readiness probes
- Helm: charts, values, templates, release lifecycle
- `helm install`, `upgrade`, `rollback`, `uninstall`

**Hands-on Lab**
1. Add liveness and readiness probes to your Day 4 deployment. Intentionally misconfigure one to see what happens
2. Mount a ConfigMap as environment variables AND as a file volume
3. Create a Secret for a database password. Mount it as an env var. Never hardcode it
4. Install a public Helm chart (e.g. `bitnami/postgresql`). Inspect its values, override 2 settings
5. Write your own minimal Helm chart for the app from Day 3 — with configurable replicas and image tag in `values.yaml`

**🤖 AI Challenge**
Ask Claude:
> "Generate a production-ready Helm chart for a Node.js app with: configurable replicas, resource limits, liveness/readiness probes, and a secret for DB password. Then explain what each template file does."
Read the output line by line. Modify the values to match your setup.

**✅ Checkpoint**
- Why are readiness probes critical in production?
- What's the difference between a ConfigMap and a Secret in terms of security?
- Your Helm upgrade broke production. How do you recover in under 2 minutes?

---

### Day 6 — Cloud Foundations (AWS + GCP/Azure)

**Goal:** Understand core cloud primitives. Navigate IAM, networking, compute, and storage without the console.

**Core Concepts (30 min)**
- IAM: users, roles, policies, least privilege principle
- VPC/VNet: subnets, routing tables, NAT gateways, security groups
- Compute: EC2/GCE/VM — instance types, SSH, user data scripts
- Storage: S3/GCS/Blob — buckets, permissions, lifecycle policies
- CLI-first mindset: `aws` CLI, `gcloud` CLI, `az` CLI

**Hands-on Lab**
Pick AWS + one of GCP/Azure (your team's actual stack)

1. Create an IAM user with least-privilege access. Configure CLI. Never use root
2. Launch an EC2 (or GCE) instance via CLI only — no console. SSH into it
3. Create a VPC with public and private subnets. Deploy something in each. Verify the private one can't be reached from outside
4. Create an S3 bucket. Upload a file via CLI. Make it public. Then lock it down and verify access denied
5. Write a user data script that auto-installs nginx on instance launch — verify it's running on boot

**🤖 AI Challenge**
Ask Claude:
> "I'm setting up AWS for a new DevOps team. What IAM policies, VPC design, and S3 configurations would you recommend as a secure baseline? Explain the reasoning behind each decision."
Compare with what you built. What would you change?

**✅ Checkpoint**
- You accidentally expose an S3 bucket publicly. What's your response plan?
- What's the difference between a Security Group and a NACL on AWS?
- A new developer needs read access to S3 and nothing else. How do you set that up?

---

### Day 7 — Infrastructure as Code with Terraform

**Goal:** Provision and manage real infrastructure with code. Understand state, drift, and the plan/apply loop.

**Core Concepts (30 min)**
- Providers, resources, data sources, variables, outputs
- State file: what it is, why it matters, remote backends
- `terraform init`, `plan`, `apply`, `destroy`
- Modules: reusability and structure
- Drift: what happens when someone changes infra manually

**Hands-on Lab**
1. Write Terraform to provision: 1 VPC + 2 subnets + 1 EC2 instance + 1 security group
2. Run `terraform plan` — read the output carefully before applying
3. Change the instance type in code. Run plan. See what changes before applying
4. Manually change a tag in the AWS console. Run `terraform plan` — observe drift
5. Extract the EC2 + security group into a reusable module. Call it twice for two environments

**🤖 AI Challenge**
Ask Claude:
> "Write a Terraform module for a secure EC2 instance with: SSH access restricted to my IP, an attached EBS volume, and outputs for public IP and instance ID."
Read every resource block. Then add: an S3 backend for remote state storage.

**✅ Checkpoint**
- Why should you never edit the state file manually?
- What's the risk of running `terraform apply` without reading `plan` first?
- How do you handle secrets (like DB passwords) in Terraform without committing them?

---

### Day 8 — CI/CD Pipeline with GitHub Actions

**Goal:** Automate build, test, and deploy. Understand the pipeline as infrastructure.

**Core Concepts (30 min)**
- Triggers: `push`, `pull_request`, `schedule`, manual dispatch
- Jobs, steps, runners, environments
- Secrets in GitHub Actions
- Build → Test → Push image → Deploy to K8s flow
- Artifacts and caching

**Hands-on Lab**
1. Create a workflow that runs on every push to `main`: lint + test + build Docker image
2. Push the image to Docker Hub or ECR on successful build — use GitHub Secrets for credentials
3. Add a manual approval gate before deploying to "production"
4. Intentionally break the test step. See the pipeline fail. Fix it
5. Add a Slack (or email) notification on pipeline failure — use a marketplace action

**🤖 AI Challenge**
Give Claude your workflow YAML and ask:
> "Review this GitHub Actions workflow. What are the security risks? Are there any inefficiencies? What would make this production-grade?"
Apply at least 3 suggestions.

**✅ Checkpoint**
- A pipeline has been running for 45 minutes. It's usually done in 5. What do you do?
- How do you prevent secrets from being exposed in pipeline logs?
- What's the difference between a job and a step?

---

### Day 9 — Monitoring & Observability

**Goal:** Know what's happening in production before users tell you something's wrong.

**Core Concepts (30 min)**
- The three pillars: Metrics, Logs, Traces
- Prometheus: scraping, metrics types (counter, gauge, histogram)
- Grafana: dashboards, alerting
- CloudWatch / Cloud Monitoring for cloud-native metrics
- The golden signals: Latency, Traffic, Errors, Saturation (LTES)

**Hands-on Lab**
1. Deploy Prometheus + Grafana on your K8s cluster (use Helm: `kube-prometheus-stack`)
2. Build a Grafana dashboard showing: CPU, memory, pod restarts, request rate
3. Set up an alert that fires when any pod restarts more than 3 times in 5 minutes
4. Deploy a sample app that has a `/metrics` endpoint. Scrape it with Prometheus. Graph it
5. Simulate a problem (high CPU, memory leak, OOM kill). Catch it using your dashboard before "a user reports it"

**🤖 AI Challenge**
Ask Claude:
> "I'm setting up monitoring for a Kubernetes cluster running a Node.js API. What Prometheus metrics should I track? What alert thresholds would you recommend? Build me a Grafana dashboard JSON for the 5 most important panels."

**✅ Checkpoint**
- Latency p99 suddenly spikes. Where do you look first?
- What's the difference between a metric and a log?
- Your alert fires every night at 3am and auto-resolves by 3:10am. What do you investigate?

---

### Day 10 — Capstone: Ship a Real Thing

**Goal:** Integrate everything. Deploy a real app end-to-end with cloud, IaC, containers, CI/CD, and monitoring.

**The Challenge**

Deploy a simple web app (Node.js, Python, or Go) with:

| Requirement | Tool |
|---|---|
| Containerized | Docker + multi-stage build |
| Deployed on K8s | Deployment + Service + Helm chart |
| Infrastructure provisioned | Terraform (VPC, cluster, or VM) |
| Automated deploy | GitHub Actions pipeline |
| Observable | Prometheus metrics + Grafana dashboard + 1 alert |
| Config managed properly | ConfigMap + Secrets (no hardcoded values) |
| Cloud storage | S3/GCS bucket via Terraform |

**Rules**
- Everything as code — nothing clicked manually
- If it breaks, debug it yourself first (10 min rule), then use AI
- Document your runbook: "How to deploy, how to scale, how to roll back"

**🤖 AI Challenge — Problem-Solving Mindset**
After deploying, ask Claude:
> "Here's my architecture [describe it]. What are the top 3 single points of failure? What would happen if the database pod crashes? Walk me through a disaster recovery plan."

Then actually test one failure scenario.

**✅ Final Checkpoint — present to your trainer**
- Walk through the full deployment flow from `git push` to live traffic
- Show a Grafana dashboard with real data
- Simulate one failure and recover from it live
- Explain: what would you do differently in a real production setup?

---

## DSA & Problem-Solving Mindset

You don't need LeetCode hard. You need the thinking pattern.

**What DevOps engineers actually solve:**
- "This pipeline is slow — where's the bottleneck?" → profiling, binary search on steps
- "The cluster is OOM — what's consuming memory?" → top-down elimination
- "Deploy works locally but fails in CI" → environment diff analysis

**Build the habit:**
- When something breaks: form a hypothesis first, then test it
- When debugging: reproduce in isolation before adding complexity
- When optimizing: measure first, never guess

**One exercise per week:**
Pick any real incident from your team (or a public postmortem). Read it. Then answer:
1. What was the root cause?
2. What signals were missed?
3. What would you have done differently?

**🤖 AI for problem-solving:**
> "Walk me through debugging this production issue step by step. I want to think through it — don't give me the answer, ask me guiding questions."

---

## How to Use AI to Speed Up Learning

| Scenario | Prompt to use |
|---|---|
| Stuck on an error | "Explain this error: [paste]. What caused it, how do I fix it, and what does it teach me?" |
| Don't understand a concept | "Explain [concept] using a real-world analogy. Then give me a 5-minute hands-on exercise to try it." |
| Want to go deeper | "I know [topic] at a basic level. What are the 3 most important things I'm probably missing?" |
| Verify your understanding | "I'm going to explain [topic] to you. Tell me what I got wrong or oversimplified." |
| Code review | "Review this [Dockerfile/Terraform/YAML]. Security issues? Improvements? Why?" |
| Quiz yourself | "Quiz me on [topic]. 5 questions, one at a time. Don't reveal the answer until I answer." |
| Prepare for real work | "Simulate a production incident involving [topic]. I'm the on-call engineer. Go." |

---

## Trainer Notes

**Your job is not to teach — it's to unblock.**

- Check in once per day: "What broke today? How did you debug it?"
- Don't give answers immediately — ask "what have you tried?" first
- Encourage the 10-minute rule: struggle alone for 10 minutes, then ask
- After Day 10 capstone: do a short debrief on what they'd do differently
- Watch for the "it works but I don't know why" pattern — that's where to probe

**Good questions to ask trainees:**
- "Walk me through what happens when you run `kubectl apply`"
- "Your Terraform plan shows a resource will be destroyed. Is that expected?"
- "How would you explain this monitoring alert to a non-technical stakeholder?"

---

## Resources

- **Linux**: [linuxcommand.org](https://linuxcommand.org), `man` pages
- **Docker**: [docs.docker.com](https://docs.docker.com)
- **Kubernetes**: [kubernetes.io/docs](https://kubernetes.io/docs), killer.sh for practice
- **Terraform**: [developer.hashicorp.com/terraform](https://developer.hashicorp.com/terraform/docs)
- **AWS**: [docs.aws.amazon.com](https://docs.aws.amazon.com), AWS Free Tier
- **GCP**: [cloud.google.com/docs](https://cloud.google.com/docs), GCP Free Tier
- **Monitoring**: Prometheus docs, Grafana Labs docs
- **Postmortems to read**: [sre.google/sre-book](https://sre.google/sre-book/table-of-contents/), [github.com/danluu/post-mortems](https://github.com/danluu/post-mortems)
