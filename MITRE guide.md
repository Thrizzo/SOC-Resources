# Using MITRE ATT&CK & MITRE D3FEND

## What They Are
**MITRE ATT&CK**
- Framework of real-world attacker behaviors (TTPs)
- Used to understand, detect, and communicate adversary techniques

**MITRE D3FEND**
- Framework of defensive techniques mapped to attacker behaviors
- Used to choose and describe defensive controls / countermeasures

---

## When to Use

### ✅ Use MITRE ATT&CK to:
- Map alerts and incidents to tactics & techniques
- Identify TTPs for Threat Actors
- Build detections and threat hunts
- Plan red/purple team exercises
- Communicate findings with standard technique IDs (e.g., T1059)

**Example:**  
Suspicious PowerShell → `Execution` tactic → `T1059.001 PowerShell`

---

### ✅ Use MITRE D3FEND to:
- Identify defensive actions for specific attacker techniques
- Improve logging, detection, and control coverage
- Prioritize defensive improvements and hardening

**Example:**  
T1059.001 → Apply script-execution monitoring & credential protection controls

---

## Practical Workflow
1. See suspicious activity / intel
2. Map to ATT&CK technique
3. Identify detection gaps
4. Use D3FEND to find counter-controls
5. Improve detections / hardening
6. Validate coverage

> ATT&CK = what attackers do  
> D3FEND = how we stop them

---

## Links
- ATT&CK Matrix: https://attack.mitre.org/
- D3FEND Framework: https://d3fend.mitre.org/

