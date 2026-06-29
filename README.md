# ET_Hack_2.0 - Rakshak SOC

**AI Cyber Resilience Platform for Critical National Infrastructure**

Rakshak SOC is an AI-powered security intelligence layer for critical infrastructure. It detects unusual behavior across IT and OT systems, connects weak signals into an attack story, maps the attack to MITRE ATT&CK, and recommends safe containment actions with a full audit trail.

## Problem Statement - Hinglish Brief

Critical national infrastructure jaise power grids, government systems, hospitals, transport networks, water plants, aur education platforms cyber attacks ke major targets ban chuke hain.

Problem sirf malware detect karna nahi hai. Real attackers kaafi time tak silently system ke andar move karte hain: ek account compromise hota hai, phir lateral movement hota hai, phir attacker engineering workstation ya OT gateway tak pahunchne ki koshish karta hai. Traditional tools mostly known signatures ya fixed rules pe depend karte hain, isliye low-and-slow attacks easily miss ho sakte hain.

Hume ek AI layer build karni hai jo normal user/device/network behavior samjhe, anomalies detect kare, weak signals ko correlate kare, attack ka current stage bataye, next probable move predict kare, aur safe response actions suggest/execute kare. Goal: breach detection ko weeks/months se reduce karke hours/minutes tak lana.

## Core Idea

We will build a simulated AI SOC for a **state electricity control center / substation network**.

This gives us a strong IT + OT setup:

- IT: users, workstations, servers, identity systems, admin accounts.
- OT: engineering workstation, OT gateway, PLC/substation devices, telemetry.
- Attack path: credential misuse -> lateral movement -> OT discovery -> possible disruption.

## MVP

| Module | What It Does |
| --- | --- |
| Event Simulator | Generates normal and attack logs for users, devices, network flows, endpoint activity, and OT events. |
| Behavioural Anomaly Engine | Learns normal behavior and scores unusual activity without relying only on known malware signatures. |
| Attack Graph | Connects weak signals across users, hosts, servers, OT gateways, and critical devices. |
| MITRE Mapping | Maps detected activity to MITRE ATT&CK tactics and techniques with evidence. |
| AI Reasoning Agent | Explains the current attack chain, likely intent, next probable step, and recommended response. |
| SOAR Orchestrator | Simulates containment actions like blocking IPs, isolating hosts, revoking tokens, and preserving evidence. |
| Audit Trail | Stores every alert, recommendation, action, timestamp, confidence score, and reason. |
| Dashboard | Shows live risk score, attack timeline, graph view, MITRE stages, and response actions. |

## Demo Flow

1. System starts in normal state.
2. A user logs in at an unusual time/location.
3. The same user accesses an uncommon internal server.
4. Suspicious lateral movement starts toward an engineering workstation.
5. Engineering workstation communicates with the OT gateway unexpectedly.
6. Risk score rises as signals connect.
7. Attack graph shows the IT-to-OT path.
8. MITRE mapping explains the attack stage.
9. SOAR recommends containment.
10. Low-risk actions execute in simulation; high-risk OT actions need human approval.
11. Final incident summary and audit trail are generated.

## Suggested Tech Stack

| Layer | Options |
| --- | --- |
| Frontend | React / Next.js, Tailwind CSS, React Flow or Cytoscape.js |
| Backend | Python FastAPI or Node.js Express |
| ML | Scikit-learn, Isolation Forest, LOF, optional Autoencoder |
| Graph | NetworkX, graph-based risk scoring |
| RAG | MITRE ATT&CK docs, response playbooks, CERT-In style advisories |
| Storage | SQLite/PostgreSQL, JSON scenario files, vector store |
| Evaluation | CIC-IDS2017, UNSW-NB15, custom IT/OT simulation data |

## 3-Week Roadmap

### Week 1 - Foundation

- Finalise electricity control center scenario.
- Define IT/OT assets and attack path.
- Build event schema and data simulator.
- Create basic backend APIs.
- Build first dashboard layout.
- Implement basic anomaly scoring.
- Create initial MITRE mapping table.

**End goal:** live event stream + basic risk score + one complete attack scenario.

### Week 2 - Intelligence Layer

- Improve anomaly detection.
- Add user/device/network baselines.
- Build attack graph correlation.
- Map events to MITRE ATT&CK.
- Add AI reasoning for attack explanation and next-step prediction.
- Build simulated SOAR actions.
- Add audit logs.

**End goal:** attack graph + MITRE mapping + response recommendations working together.

### Week 3 - Polish and Submission

- Polish dashboard and demo flow.
- Add timeline playback.
- Add incident report generation.
- Add baseline SOC vs Rakshak SOC comparison.
- Prepare architecture diagram.
- Prepare presentation deck.
- Record demo video.
- Stress-test backup demo data.

**End goal:** working prototype + deck + demo video + clean final pitch.

## Team Work Breakdown

| Member | Main Focus | Responsibilities |
| --- | --- | --- |
| Rana | Backend, integration, product flow | APIs, event pipeline, dashboard integration, SOAR action flow, final system wiring. |
| kk | Cybersecurity realism | Attack scenario, MITRE mapping, IT/OT asset model, response playbooks, containment safety gates. |
| ak1 | AIML and reasoning | Anomaly detection, behavior baselines, risk scoring, graph correlation, RAG/AI explanation support. |

## What We Should Avoid

- Generic cyber dashboard with random alert cards.
- Chatbot-only solution over MITRE/CVE docs.
- Overclaiming exact APT attribution without evidence.
- Fully autonomous shutdown actions for critical OT assets.
- Too many half-built features instead of one strong end-to-end demo.

## Winning Angle

> Rakshak SOC detects low-and-slow attacks in critical infrastructure by correlating weak behavioral signals across IT and OT, mapping attack progression to MITRE ATT&CK, predicting the next move, and safely orchestrating containment with full auditability.

## MVP Scope Priority

**Must-have:** simulator, anomaly scoring, attack graph, MITRE mapping, dashboard, SOAR recommendations, audit log.

**Good-to-have:** RAG explanation agent, CVE prioritisation, incident report export, blast-radius simulation.

**Stretch:** benchmark dataset evaluation, autoencoder model, multiple attack scenarios, advanced digital twin.
