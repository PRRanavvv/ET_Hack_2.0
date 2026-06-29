# ET Hack Ai

## Project Codename

**Rakshak SOC: AI Cyber Resilience Digital Twin for Critical Infrastructure**

An AI-powered cyber resilience platform for critical national infrastructure that detects low-and-slow attacks, correlates weak signals across IT and OT systems, maps attack progression to known threat frameworks like MITRE ATT&CK, and recommends or executes safe containment actions with full auditability.

## Problem Statement - Hinglish Brief

Critical national infrastructure, jaise power grids, government systems, transport networks, hospitals, water plants, aur education platforms, aaj cyber attacks ke major targets ban chuke hain. Problem sirf malware detect karna nahi hai. Real issue ye hai ki attackers kaafi time tak system ke andar silently move karte rehte hain, aur organisations ko breach ka pata bahut late chalta hai.

Traditional security tools mostly known signatures ya fixed rules pe depend karte hain. Agar attack naya hai, ya attacker low-and-slow behavior use kar raha hai, to normal SOC tools easily miss kar sakte hain. Critical infra me IT systems ke saath OT systems bhi hote hain, jaise SCADA, PLCs, sensors, gateways, substations, industrial control devices, etc. In dono worlds ke signals ko ek saath samajhna hard hota hai.

Hume ek AI intelligence layer build karni hai jo normal user, device, network aur OT behavior ko samjhe, unusual activity detect kare, weak signals ko connect kare, attack ka stage identify kare, next probable move predict kare, aur safe containment actions suggest/execute kare. Goal ye hai ki detection weeks/months ke badle hours ya minutes me ho, aur response controlled, explainable, aur auditable ho.

## Why This Problem Is Worth Pursuing

- It has strong national and business impact.
- It fits our team well: AIML + cybersecurity + backend/web.
- It is not just another chatbot or dashboard if executed properly.
- It gives us measurable technical depth: anomaly detection, graph correlation, MITRE mapping, RAG, SOAR workflows, and audit trails.
- It can be demoed powerfully using a simulated critical infrastructure attack story.

## Proposed Product

**Rakshak SOC** acts like an AI SOC layer for a critical infrastructure control center.

It continuously observes logs, user behavior, endpoint telemetry, network flows, asset inventory, and OT gateway events. Instead of waiting for known malware signatures, it builds behavioral baselines and detects unusual patterns. It then correlates those anomalies into an attack graph, maps them to MITRE ATT&CK techniques, predicts likely next steps, and triggers safe response actions through a simulated SOAR layer.

## Target Scenario

We will focus the MVP on a **state electricity control center / substation network**.

This is a good fit because it naturally contains:

- IT systems: users, workstations, file servers, identity systems, admin consoles.
- OT systems: engineering workstation, OT gateway, PLC/substation devices, telemetry.
- Critical impact: disruption can affect electricity supply and public services.
- Realistic attack paths: credential theft, lateral movement, OT discovery, command misuse.

## MVP Breakdown

### 1. Behavioural Anomaly Detection Engine

Goal: detect suspicious behavior without relying only on known malware signatures.

What it should do:

- Build baseline profiles for users, devices, and network segments.
- Score deviations from normal behavior.
- Detect weak signals such as unusual login time, rare destination access, abnormal failed login burst, lateral movement attempt, unusual OT gateway communication, or suspicious command execution.

Possible techniques:

- Isolation Forest
- Local Outlier Factor
- Autoencoder-based anomaly detection
- Statistical baselines
- Graph-based risk scoring

### 2. Signal Correlation and Attack Graph

Goal: avoid treating every alert separately.

What it should do:

- Combine anomalies from logs, network flows, endpoint activity, and OT events.
- Create a live attack graph showing entities and relationships.
- Link user -> host -> server -> engineering workstation -> OT gateway -> PLC/substation device.
- Increase risk when multiple weak signals form a meaningful chain.

### 3. MITRE ATT&CK Mapping Layer

Goal: explain what stage of attack is happening in a standard cyber framework.

What it should do:

- Map detected events to MITRE ATT&CK techniques.
- Show attack progression:
  - Initial Access
  - Credential Access
  - Discovery
  - Lateral Movement
  - Command and Control
  - Impact / OT disruption risk
- Provide confidence and evidence for every mapping.

### 4. APT Pattern Reasoning Agent

Goal: reason over the current attack chain and predict likely next steps.

What it should do:

- Use a small RAG layer over MITRE ATT&CK, threat intelligence notes, and response playbooks.
- Explain what the attacker is likely trying to do.
- Predict next probable move.
- Recommend defensive actions based on current evidence.

Important: we should avoid claiming exact nation-state attribution unless evidence is strong. Instead, we can say "campaign pattern similarity" or "APT-like behavior".

### 5. SOAR Containment Orchestrator

Goal: convert detection into response.

What it should do:

- Recommend containment actions based on risk level and asset criticality.
- Auto-execute only low-risk simulated actions.
- Require human approval for high-impact actions.
- Maintain audit logs for every recommendation and action.

Example actions:

- Block suspicious IP.
- Isolate suspicious workstation.
- Revoke user session/token.
- Disable compromised account.
- Snapshot evidence.
- Escalate to human operator.
- Require approval before isolating OT gateway or critical control asset.

### 6. Cyber Resilience Digital Twin

Goal: show the organisation's cyber-physical environment safely.

What it should do:

- Represent IT and OT assets as a network graph.
- Simulate attack paths without touching real systems.
- Show blast radius if an asset is compromised.
- Support red-team scenario playback during the demo.

## Core Demo Story

The demo should tell one strong end-to-end attack story.

1. System starts in normal state.
2. A user account logs in at an unusual time/location.
3. The same account accesses an uncommon internal server.
4. Suspicious lateral movement starts toward an engineering workstation.
5. Engineering workstation communicates with OT gateway unexpectedly.
6. A risky command or abnormal communication is seen near a simulated PLC/substation device.
7. Risk score rises gradually from low to critical.
8. Attack graph maps the path from IT compromise to OT impact risk.
9. MITRE mapping explains each stage.
10. SOAR layer recommends containment.
11. Low-risk actions execute automatically in simulation.
12. High-risk OT actions require human approval.
13. Final incident report and audit trail are generated.

## Suggested Tech Stack

Frontend:

- React / Next.js
- Tailwind CSS or simple component library
- Graph visualization with React Flow, D3, or Cytoscape.js

Backend:

- Python FastAPI or Node.js Express
- REST APIs for events, risk scoring, graph state, actions, and reports

AI/ML:

- Scikit-learn for anomaly detection
- PyTorch/TensorFlow only if needed for autoencoder
- NetworkX for attack graph logic
- Sentence embeddings + vector DB for RAG

Data:

- Simulated IT/OT logs for the core demo
- Optional benchmark datasets for evaluation:
  - CIC-IDS2017
  - UNSW-NB15
  - Custom generated OT/SCADA-like event stream

Threat Intelligence:

- MITRE ATT&CK framework
- CERT-In style advisory summaries
- CVE metadata for vulnerability prioritisation

Storage:

- SQLite/PostgreSQL for events and audit logs
- JSON files for demo scenarios
- Vector store for RAG documents

## Evaluation Metrics

We should align with the hackathon judging criteria.

Technical metrics:

- Anomaly detection precision/recall.
- False positive rate.
- Mean Time To Detect improvement versus baseline rule-based SOC.
- Mean Time To Respond improvement using automated playbooks.
- MITRE technique mapping accuracy.
- Percentage of playbook steps automated.
- Auditability: every action should have evidence, reason, timestamp, and actor.

Product metrics:

- Time from signal to recommendation.
- Clarity of attack graph.
- Operator trust in recommendations.
- Safety of containment actions.
- Ease of demo understanding.

## 3-Week Roadmap

### Week 1 - Foundation and Scenario

Main objective: build the base simulation and data pipeline.

- Finalise target scenario: electricity control center / substation network.
- Define assets: users, workstations, servers, engineering workstation, OT gateway, PLC/substation device.
- Create normal and attack event schemas.
- Generate/simulate realistic logs:
  - authentication logs
  - network flows
  - endpoint events
  - OT gateway events
  - asset inventory
- Build basic backend APIs.
- Build first dashboard skeleton.
- Implement baseline anomaly scoring using simple statistical methods or Isolation Forest.
- Draft MITRE mapping table for demo events.

Deliverable by end of Week 1:

- Data simulator running.
- Backend receiving events.
- Basic dashboard showing live events and risk scores.
- One complete attack path defined.

### Week 2 - Intelligence Layer

Main objective: make the system actually reason across signals.

- Improve anomaly detection models.
- Add entity profiles for users, devices, and network zones.
- Build attack graph correlation logic.
- Map events to MITRE ATT&CK techniques.
- Add risk scoring that increases based on correlated weak signals.
- Implement RAG-based reasoning over MITRE/playbook docs.
- Add next-step prediction and recommended response.
- Build SOAR action engine in simulation mode.
- Add audit log for recommendations and executed actions.

Deliverable by end of Week 2:

- Attack graph works.
- MITRE mapping works.
- AI reasoning agent explains the attack chain.
- SOAR recommendations appear with confidence and blast-radius gate.

### Week 3 - Polish, Evaluation, and Presentation

Main objective: make it demo-ready and judge-friendly.

- Polish UI and demo flow.
- Add timeline playback for attack scenario.
- Add incident report generation.
- Add before/after comparison:
  - baseline SOC detects late
  - Rakshak SOC detects earlier
- Add metrics dashboard.
- Prepare architecture diagram.
- Prepare presentation deck.
- Record demo video.
- Stress-test demo with team members.
- Keep backup static demo data in case live simulation fails.

Deliverable by end of Week 3:

- Working prototype.
- Final README.
- Architecture diagram.
- Presentation deck.
- Demo video.
- Clear role-wise explanation.

## Team Work Breakdown

### Me

Focus: backend, integration, and product flow.

- Build backend APIs for events, graph state, risk scores, and SOAR actions.
- Connect ML outputs to dashboard.
- Handle data simulator and event pipeline.
- Own final system integration.
- Help with dashboard logic and demo orchestration.

### kk

Focus: cybersecurity realism and response logic.

- Design realistic attack scenario.
- Define IT/OT assets and possible attack paths.
- Map events to MITRE ATT&CK techniques.
- Create response playbooks.
- Define containment safety gates.
- Validate whether the demo feels credible from a cyber perspective.

### ak1

Focus: AIML, anomaly detection, and reasoning layer.

- Build anomaly detection models.
- Create behavioral baselines for users/devices/network segments.
- Develop risk scoring logic.
- Work on graph-based correlation.
- Build or assist with RAG layer for MITRE/playbook reasoning.
- Help evaluate model performance and false positives.

## What We Should Avoid

- Do not build only a generic cyber dashboard.
- Do not build only a chatbot over MITRE documents.
- Do not overclaim exact APT attribution.
- Do not make response actions fully autonomous for high-risk OT assets.
- Do not spread ourselves across all features; one excellent end-to-end demo is better.

## Winning Angle

Our winning angle is not "AI detects cyber attacks".

Our winning angle is:

> We built an AI SOC layer for critical infrastructure that detects low-and-slow attacks by correlating weak behavioral signals across IT and OT, maps the attack progression to MITRE ATT&CK, predicts the next likely move, and safely orchestrates containment with full auditability.

## Initial MVP Scope

Must-have:

- Event simulator
- Behavioral anomaly scoring
- Attack graph
- MITRE mapping
- Risk score timeline
- SOAR recommendation engine
- Audit log
- Dashboard

Good-to-have:

- RAG explanation agent
- CVE prioritisation
- Digital twin blast radius simulation
- Incident report export
- Demo video with narration

Stretch:

- Real benchmark dataset evaluation
- Autoencoder-based anomaly detection
- More than one attack scenario
- Multi-organisation comparative dashboard

## Final Product Vision

Rakshak SOC should feel like a command center for cyber resilience, not just an alert viewer. It should help operators understand:

- What is abnormal?
- Why does it matter?
- Which assets are involved?
- Which MITRE techniques are likely active?
- What could happen next?
- What can we safely contain now?
- What evidence supports every decision?

If we execute this cleanly, the project can show strong innovation, real-world impact, technical depth, scalability, and a polished user experience.
