# NetSage-X

### Evidence-Driven AI Network Troubleshooting & Verification System

NetSage-X is an AI-assisted troubleshooting system designed for Cisco-style networking labs and Packet Tracer scenarios.

The system combines **network evidence extraction, deterministic configuration checks, AI-based root-cause reasoning, confidence scoring, competing hypotheses, and mandatory human verification** to help junior network engineers troubleshoot network faults systematically.

> **NetSage-X does not automatically apply fixes. Every AI diagnosis must be reviewed and accepted, edited, or rejected by a human.**

---

## 🎯 Problem

Junior network engineers often know individual networking commands but struggle to connect observed symptoms with the actual root cause.

For example:

> A PC receives an IP address but cannot reach a server.

The fault could involve:

* VLAN configuration
* Inter-VLAN routing
* DHCP
* DNS
* ACL
* NAT
* Routing
* Gateway configuration
* Wireless configuration

NetSage-X addresses this problem by combining network evidence with deterministic validation and AI reasoning.

---

## 💡 Solution

NetSage-X follows an evidence-first troubleshooting workflow:

```text
Network Symptom
      │
      ▼
Topology + Show Commands
      │
      ▼
Evidence Extraction
      │
      ├───────────────┐
      ▼               ▼
Rule Engine       AI Reasoning
      │               │
      └───────┬───────┘
              ▼
     Evidence Correlation
              │
              ▼
    Confidence Assessment
              │
              ▼
    Competing Hypotheses
              │
              ▼
       Human Review
       /     |      \
  Accept   Edit    Reject
              │
              ▼
      Fix Recommendation
              │
              ▼
        Verification
```

---

## ⭐ Key Features

### 1. Evidence-Driven Diagnosis

The system does not rely only on the reported symptom.

It analyzes:

* Symptoms
* Topology information
* Cisco `show` command output
* Deterministic rule results
* Expected network behavior

The diagnosis references the actual evidence used to reach the conclusion.

---

### 2. Deterministic Rule Engine

The Python rule engine performs predictable checks for common configuration mistakes.

Examples include:

* Duplicate IP addresses
* Incorrect subnet masks
* Gateway mismatch
* Interface shutdown
* Missing VLAN
* Missing routes
* Trunk configuration inconsistencies
* Basic ACL inconsistencies

This provides an independent validation layer alongside AI reasoning.

---

### 3. AI Reasoning Engine

The AI is prompted to return structured diagnostic information:

```json
{
  "root_cause": "",
  "confidence": 0,
  "osi_layer": "",
  "evidence": [],
  "alternative_causes": [],
  "next_command": "",
  "fix_steps": [],
  "verification_command": ""
}
```

---

### 4. Competing Hypotheses

Instead of immediately selecting a single explanation, NetSage-X can rank multiple possible causes.

Example:

```text
1. ACL configuration problem       72%
2. Missing route                   18%
3. VLAN configuration problem       7%
4. NAT configuration problem        3%
```

This helps prevent premature diagnosis.

---

### 5. Evidence Confidence

NetSage-X combines multiple signals to estimate diagnostic confidence.

The confidence model considers:

* Command evidence
* Rule-engine agreement
* Symptom consistency
* Topology consistency
* Contradicting evidence

The resulting score is used as a decision-support indicator rather than an automatic authorization to apply a fix.

---

### 6. Human-in-the-Loop Review

Every diagnosis requires human review.

A reviewer can:

```text
ACCEPT
EDIT
REJECT
```

Corrections are recorded for responsible-AI analysis.

---

### 7. Before/After Verification

After a proposed fix, the system can record:

```text
Before:
PC → Gateway       PASS
PC → Server        FAIL

After:
PC → Gateway       PASS
PC → Server        PASS

Resolution:
VERIFIED
```

---

## 📊 Dataset

The project contains troubleshooting cases covering:

* VLAN
* Gateway
* DHCP
* DNS
* Routing
* ACL
* NAT
* Wireless

Each case contains structured evidence and an expected diagnosis.

### Case schema

```text
case_id
symptom
topology
device
show_outputs
expected_fault
alternative_faults
osi_layer
concept
severity
evidence_required
recommended_command
expected_fix
verification_command
```

---

## 🧠 Troubleshooting Workflow

### Step 1 — Collect the case

The user provides:

* Network symptom
* Relevant topology information
* Device information
* Available `show` command output

### Step 2 — Extract evidence

Relevant configuration and operational evidence is identified.

### Step 3 — Run deterministic checks

The rule engine checks common configuration errors.

### Step 4 — Generate AI diagnosis

The AI evaluates the symptom and evidence.

### Step 5 — Compare hypotheses

Potential root causes are ranked.

### Step 6 — Calculate confidence

Evidence and rule-engine agreement are used to estimate confidence.

### Step 7 — Human review

The reviewer accepts, edits, or rejects the diagnosis.

### Step 8 — Apply the recommended fix

The system provides remediation steps but does not autonomously modify network devices.

### Step 9 — Verify

Connectivity and configuration are checked again.

---

## 🏗️ Project Architecture

```text
                    ┌───────────────────┐
                    │ Network Case      │
                    │ Symptom + Topology│
                    │ + Show Commands   │
                    └─────────┬─────────┘
                              │
                              ▼
                    ┌───────────────────┐
                    │ Evidence Engine   │
                    └─────────┬─────────┘
                              │
                ┌─────────────┴─────────────┐
                ▼                           ▼
       ┌────────────────┐          ┌────────────────┐
       │ Rule Engine    │          │ AI Reasoning   │
       │ Python Checks  │          │ Engine         │
       └────────┬───────┘          └───────┬────────┘
                │                          │
                └───────────┬──────────────┘
                            ▼
                  ┌────────────────────┐
                  │ Evidence           │
                  │ Correlation Engine │
                  └──────────┬─────────┘
                             ▼
                  ┌────────────────────┐
                  │ Confidence &       │
                  │ Hypothesis Ranking │
                  └──────────┬─────────┘
                             ▼
                  ┌────────────────────┐
                  │ Human Review       │
                  └──────────┬─────────┘
                             ▼
                  ┌────────────────────┐
                  │ Fix + Verification │
                  └────────────────────┘
```

---

## 📁 Repository Structure

```text
NetSage-X/
│
├── cases/
│   └── cases.csv
│
├── checker/
│   ├── rule_checker.py
│   └── sample_output.txt
│
├── engine/
│   ├── evidence_engine.py
│   ├── confidence_engine.py
│   └── diagnosis.py
│
├── prompts/
│   ├── diagnose_prompt.md
│   ├── evidence_prompt.md
│   └── review_prompt.md
│
├── dashboard/
│   └── app.py
│
├── review/
│   └── review_log.csv
│
├── responsible_ai/
│   └── correction_log.md
│
├── results/
│   └── sample_diagnosis.json
│
├── demo/
│   └── demo_script.md
│
└── docs/
    ├── architecture.md
    └── methodology.md
```

---

## 🛠️ Technology Stack

| Component            | Technology                     |
| -------------------- | ------------------------------ |
| Programming Language | Python                         |
| Data Processing      | Pandas                         |
| Rule Engine          | Python                         |
| AI Reasoning         | LLM-based structured prompting |
| Dashboard            | Streamlit                      |
| Data Format          | CSV / JSON                     |
| Network Environment  | Cisco Packet Tracer            |
| Version Control      | Git / GitHub                   |

---

## 🚀 Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/NetSage-X.git
cd NetSage-X
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it on Linux:

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## ▶️ Run the Rule Checker

```bash
python checker/rule_checker.py
```

---

## 📊 Run the Dashboard

```bash
streamlit run dashboard/app.py
```

---

## 🔐 Responsible AI

NetSage-X follows a human-in-the-loop design.

The system:

* Does not automatically apply configuration changes.
* Requires human review of every AI diagnosis.
* Records accepted, edited, and rejected diagnoses.
* Documents cases where AI reasoning was corrected.
* Uses network evidence to support conclusions.
* Reports uncertainty when evidence is insufficient.

---

## 📈 Evaluation

The project evaluates:

* Case coverage
* Evidence usage
* Rule-engine accuracy
* AI diagnosis agreement
* Human correction rate
* Confidence quality
* Verification success

---

## 🎥 Demonstration

The final demonstration follows this workflow:

```text
Broken Packet Tracer Network
          ↓
Collect Symptoms
          ↓
Collect Show Commands
          ↓
Run Rule Checker
          ↓
Generate AI Diagnosis
          ↓
Rank Possible Causes
          ↓
Human Review
          ↓
Apply Recommended Fix
          ↓
Verify Connectivity
```

---

## ⚠️ Disclaimer

NetSage-X is an educational troubleshooting assistant intended for Cisco-style networking laboratories and Packet Tracer scenarios.

It is designed to support human decision-making and should not be treated as an autonomous network configuration system.

---

## 👨‍💻 Project

**NetSage-X — Evidence-Driven AI Network Troubleshooting & Verification System**

Developed as part of an Applied AI + Network Troubleshooting project.
