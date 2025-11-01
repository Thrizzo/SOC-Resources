# Forensic Collection Playbook

## Guiding Principles
- **Consistency**: Follow the same documented workflow, tools, and naming conventions every time.
- **Repeatability**: Record each action, tool version, and setting so a peer can reproduce the collection.
- **Customary Practice**: Align with industry standards (SWGDE, NIST SP 800-101, ISO/IEC 27037) and applicable legal requirements.

---

## 1. Scene Documentation & Preservation

### 1.1 Initial Entry
1. Capture the date, time, and team members on-site using a standardized 24-hour timestamp.
2. Note weather conditions, physical access controls, and any deviations from standard procedures.
3. Establish a perimeter; restrict access to authorized personnel only.

### 1.2 Visual Documentation
1. Photograph the area from wide to detail shots: room, workstation, peripheral devices, cable connections, screen state.
2. Include scale references (e.g., ruler) where appropriate and maintain photo logs (photo number, description, photographer, timestamp).
3. If active monitors exist, photograph displays before interacting with keyboards/mice.

### 1.3 Current State Capture
1. Record system state without altering it: running services, logged-in users, visible error messages.
2. If permissible, record short video walkthroughs to capture dynamic elements (e.g., blinking indicators).
3. Document observed volatile indicators (network cables connected, USB devices, wireless adapters).

---

## 2. Chain of Custody Preparation

### 2.1 Forms & Labels
1. Pre-fill chain-of-custody (CoC) forms with case ID, evidence descriptor, and unique evidence number.
2. Prepare tamper-evident seals and barcoded tags; verify their serials are logged in the CoC register.
3. Print or preload standardized CoC templates to ensure consistent data capture.

### 2.2 Documentation Standards
1. Ensure CoC entries include: collector, date/time, location, description, condition, transfer details.
2. Adopt a single time source (e.g., UTC via time.gov) for all entries to maintain chronological accuracy.
3. Train team members on signature requirements and custodial transfer protocols ahead of time.

---

## 3. Forensic Workstation & VM Preparation

### 3.1 Workstation Baseline
1. Use a dedicated, clean forensic workstation if possible with write-blocked.
2. Document hardware specs, operating system build, and patch level before each use.
3. Verify endpoint protection is configured to avoid interference with forensic tools.

### 3.2 Virtual Machine (VM) Setup
1. Maintain gold images for specialized tools (memory acquisition, mobile triage, network captures).
2. Snapshot VMs prior to case use and record snapshot IDs in the case log.
3. Confirm licensing and hash values of forensic applications (e.g., FTK Imager, X-Ways, Magnet RAM Capture).

### 3.3 Tool Validation
1. Log tool versions and configuration files in the case notebook.
2. Prepare external storage (encrypted drives) labeled with evidence IDs and pre-generated hashes.

---

## 4. Evidence Collection Workflow (Order of Volatility)

> **Reminder**: Work from most volatile evidence (easily lost) to least volatile (persistent) to maximize data preservation.
Use the tools available for extraction in our case Velociraptor, the Forensic Station with Flare and Remnux. Before doing anything, think about how you are going to do it. Not every system and case are the same, use common sense.

### 4.1 Volatile Data
1. **CPU Registers / Cache**: If specialized tools and authorizations are available, capture via hardware-specific utilities.
2. **RAM**: Use validated memory acquisition tool; dump to encrypted external media; record starting/stopping times.
3. **Network State**: Capture active connections, ARP tables, routing tables (`netstat`, `arp`, `route`) ensuring command outputs are redirected to write-blocked media.
4. **Running Processes/Services**: Export process lists, open handles, scheduled tasks (e.g., `tasklist /svc`, `wmic process` on Windows).

### 4.2 Semi-Volatile Data
1. **Temporary Files & Swap**: Acquire pagefile, hibernation file, temp directories via logical collection.
2. **Logs & Queues**: Copy event logs, application logs, print queues, spooler directories.
3. **Peripheral States**: Document attached storage, mounted shares, connected mobile devices.

### 4.3 Non-Volatile Data
1. **Primary Storage**: Acquire bit-for-bit images using write blockers. Prefer hardware write blockers; fall back to software blockers only if documented and allowed.
2. **Secondary Media**: Image USB drives, memory cards, optical discs; record serial numbers, make/model.
3. **Backups & Cloud Artifacts**: Coordinate with custodians to export server backups, cloud snapshots (preserve provider metadata and timestamps).

### 4.4 Network & Off-Site Collections
1. Capture relevant network logs (firewall, IDS/IPS, VPN) using standardized request forms.
2. If collecting virtual infrastructure (e.g., cloud VMs), use guidelines of the respective vendor on collecting forensic artifacts
3. Preserve configuration backups (switch configs, router snapshots) ensuring minimal operational impact.

---

## 5. Hashing & Integrity Verification

### 5.1 Initial Hashing
1. Calculate cryptographic hashes (SHA-256 or stronger) immediately after each acquisition completes.
2. Use at least two independent tools (e.g., `sha256sum` and `Get-FileHash`) to confirm matching results.
3. Record hash values in the case log, CoC, and evidence label; include tool name, version, and hash algorithm.

### 5.2 Ongoing Verification
1. Re-verify hashes whenever evidence is transferred, accessed, or processed.
2. Document verification events with date/time, personnel, and results.
3. If a hash mismatch occurs, stop work, isolate the media, and escalate per incident response SOP.

---

## 6. Documentation & Quality Assurance

### 6.1 Collection Log
1. Maintain a chronological log of actions (who, what, when, where, why, how).
2. Reference evidence numbers consistently in all notes, photographs, and digital records.
3. Attach relevant system outputs (command logs, acquisition reports) to the case file.

### 6.2 QC Checks
1. Have a second responder review logs, hashes, and CoC entries for completeness.
2. Verify evidence labels against CoC to ensure traceability.
3. Store all documentation in the designated case repository with controlled access.



