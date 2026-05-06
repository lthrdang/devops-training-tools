# DevOps & Cloud Team — New Member Training

> **Practice over theory. Doing over memorizing. AI as a tool, not a shortcut.**

> 🌐 **Open [`index.html`](index.html) in a browser** for the visual landing page. This README is the same content for GitHub viewers.

This repository is a complete onboarding system for new DevOps and Cloud team members — from their first day to their first real task. Everything lives here: the learning path, the story-driven labs, the pre-assessment, and the trainer's evaluation guide.

---

## How to use this

```
New joinee arrives
       │
       ▼
① Take the pre-test → find out where to start
       │
       ▼
② Follow the EcoTrack story → solve one real problem per day
       │
       ▼
③ Use the roadmap as a reference alongside each chapter
       │
       ▼
④ Day 10 capstone → trainer assessment
```

---

## The Files

### 🚦 [Pre-Assessment](devops-pretest.html)
**Open this first.**

24 scenario-based questions across 8 skill areas. Takes ~15 minutes. Results tell you exactly which days of the roadmap to do in full, which to skim, and which you can skip — so you don't waste time on things you already know.

> Covers: Linux · Networking · Docker · Kubernetes · Cloud (AWS/GCP) · Terraform · Monitoring · Problem-solving mindset

---

### 🌿 [EcoTrack Story Training](ecotrack-story-training.html)
**Your main training journey.**

You've just joined EcoTrack — a 4-person startup that built a CO₂ tracking SaaS platform. They built it fast. It has 7 things wrong with it. Your job is to fix them, one per day, over 10 days.

Each chapter is a real incident triggered by the previous one. The skills you learn on Day 3 are what you need to solve Day 4. By Day 10, you deploy a fix to a live customer escalation using everything you've built.

| Chapter | Incident | Skill |
|---|---|---|
| Day 1 | "The server keeps crashing" | Linux & Shell |
| Day 2 | "A researcher found our open database" | Networking |
| Day 3 | "It works on my laptop" | Docker |
| Day 4 | "We're on TechCrunch. We're also down." | Kubernetes |
| Day 5 | "Sara deployed to prod again" | Helm + K8s Advanced |
| Day 6 | "Investors want a security audit" | Cloud Foundations |
| Day 7 | "I accidentally deleted staging" | Terraform / IaC |
| Day 8 | "Nobody should SSH to deploy" | CI/CD Pipeline |
| Day 9 | "We found out from a tweet" | Monitoring & Alerting |
| Day 10 | "Fix it or lose the customer" | Capstone |

Each chapter includes: the incident story, a step-by-step mission, a success criterion, and an AI challenge prompt you use with Claude or ChatGPT.

---

### 📋 [Day-by-Day Roadmap](devops-cloud-onboarding-roadmap.md)
**Your reference guide.**

Keep this open alongside the story training. It covers:
- The theory minimum for each day (≤ 30 min)
- The hands-on lab tasks
- The AI prompt for that day
- Checkpoint questions before you move on
- Resource links

Also includes: a full [AI usage guide](#) showing which prompts to use for each learning situation, and a [DSA & Problem-Solving](#) section on building the debugging mindset.

---

### 📋 [Trainer Assessment Rubric](trainer/assessment-rubric.html)
**For trainers only — used at the Day 10 capstone.**

A structured evaluation guide the trainer fills in during the final presentation. Covers all 8 skill areas with specific probe questions and a 0–3 rating scale. Includes a live demo checklist and a final recommendation (ready for independent work / needs pairing / second sprint).

Scores auto-calculate, state saves in the browser, and there's a Print to PDF button for the trainee's record.

---

### 📊 [Trainer Dashboard](trainer/dashboard.html)
**For trainers — cohort overview across all trainees.**

Open the `progress/` folder to instantly see every trainee's pre-test score, chapter progress, top skill gap, and assessment result in one table. Click any row for a full breakdown. Supports drag-and-drop of individual files too.

---

## Progress Tracking

Each trainee's progress is stored as a single JSON file in the `progress/` folder. No database, no server — just files you can read, diff, and version-control like any other code.

### How it works

**For trainees:**
1. Open the pre-test → enter your name → complete it → click **💾 Save Progress File**
2. Save the file into the `progress/` folder of this repo (name it `your-name.json`)
3. Open the story training → click **📂 Load** to restore your progress anytime
4. After each chapter, click **💾 Save** to update your file
5. `git commit` your progress file so the trainer can see it

**For trainers:**
1. Open [Trainer Dashboard](trainer/dashboard.html)
2. Click **Open progress/ folder** and select the `progress/` folder from this repo
3. See the full cohort at a glance — pre-test scores, chapters done, assessment status
4. After the Day 10 capstone, export the completed [Assessment Rubric](trainer/assessment-rubric.html) and update the trainee's JSON with the results

### JSON schema

Each file follows this structure:

```json
{
  "version": "1.0",
  "trainee":    { "name", "email", "start_date" },
  "pretest":    { "completed", "date", "score_pct", "section_scores", "recommendations" },
  "story":      { "chapters_completed", "chapter_dates", "current_chapter" },
  "assessment": { "completed", "total_score", "recommendation", "section_scores", "notes" },
  "last_updated": "ISO timestamp"
}
```

See [`progress/_template.json`](progress/_template.json) for the full empty schema and [`progress/example-trainee.json`](progress/example-trainee.json) for a filled example.

---

## The Stack Covered

| Area | Tools |
|---|---|
| OS & Shell | Linux (Ubuntu), Bash |
| Containers | Docker, Docker Compose |
| Orchestration | Kubernetes, Helm |
| Cloud | AWS + GCP / Azure |
| IaC | Terraform |
| Monitoring | Prometheus, Grafana, CloudWatch |
| CI/CD | GitHub Actions |
| Problem-Solving | Debugging mindset, incident analysis |

---

## AI Usage Ground Rules

Use AI throughout — but as a senior engineer who asks you guiding questions, not as a solution vending machine.

| ✅ Use AI to | ❌ Don't use AI to |
|---|---|
| Explain an error you don't understand | Get the answer without understanding it |
| Review your code and explain the issues | Write code you can't explain line by line |
| Quiz you at the end of a day | Skip the hands-on lab |
| Simulate an incident for you to diagnose | Do the diagnosis for you |
| Generate boilerplate you then modify | Generate and submit without reading |

**Quick prompts for common situations:**

```
# Stuck on an error
"Explain this error: [paste]. What caused it, how do I fix it, what does it teach me?"

# Don't understand a concept  
"Explain [concept] using a real analogy. Then give me a 5-minute exercise to try it."

# Want to go deeper
"I know [topic] at a basic level. What are the 3 most important things I'm probably missing?"

# Verify your own understanding
"I'm going to explain [topic] to you. Tell me what I got wrong or oversimplified."

# Self-quiz
"Quiz me on [topic]. 5 questions, one at a time. Don't reveal the answer until I answer."

# Simulate an incident
"Simulate a production incident involving [topic]. I'm the on-call engineer. Go."
```

---

## For Trainers

Your role is to **unblock, not to teach**. The story and labs do the teaching. You show up to:

- Check in once per day: *"What broke today? How did you debug it?"*
- Ask "what have you tried?" before giving answers
- Watch for **"it works but I don't know why"** — that's where to probe
- Run the [Day 10 assessment](trainer/assessment-rubric.html) as the final gate

**The 10-minute rule:** trainees struggle alone for 10 minutes before asking. Productive struggle builds the instinct. Immediate answers prevent it.

---

## File Structure

```
training-tools/
├── README.md                           ← you are here
├── index.html                          ← trainee landing page
├── devops-pretest.html                 ← step 1: pre-assessment
├── ecotrack-story-training.html        ← step 2: story-driven labs
├── devops-cloud-onboarding-roadmap.md  ← reference alongside the story
├── trainer/                            ← separate trainer-only site
│   ├── index.html                      ← trainer console landing page
│   ├── dashboard.html                  ← cohort overview
│   └── assessment-rubric.html          ← Day 10 capstone
└── progress/
    ├── _template.json                  ← blank schema for a new trainee
    ├── example-trainee.json            ← filled example
    └── <name>.json                     ← one file per trainee (git-tracked)
```
