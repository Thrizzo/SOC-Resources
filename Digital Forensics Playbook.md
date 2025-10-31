Digital Forensics Playbook — Step-by-Step

Goal: Preserve and collect digital evidence that is forensically sound, reproducible, and defensible in court.

1. Preparation (Before You Touch Anything)

Put on PPE (gloves) and open your forensic notebook/case file.

Prepare tools: write-blocker(s), forensic workstation (SIFT), acquisition tools (dd, dc3dd, Guymager, FTK Imager, OSForensics), hashing utilities, evidence bags, tamper seals, camera.

Assign a Case ID (unique) and label convention (e.g., CASE2025-001_HOST-01).

Confirm legal authority (warrant, owner consent, or corporate authorization) and document it in the case file.

SIFT-specific: prepare the case folder on the SIFT workstation before acquisition.

2. Photograph & Document the Medium “As Found”

Take photos from multiple angles and closeups before moving anything.

Photograph the whole scene, device orientation, connected cables, power state, peripherals, serial numbers, model numbers, visible stickers, and any open windows on-screen (if live).

Include a scale (ruler) and a timestamp (sync camera time to NTP if possible).

Record environment notes: room, owner present, who collected photos, device location.

Save photos to secure media and calculate hashes for the photo files.

Photo checklist

Device front, back, left, right

Closeups: serial number, labels, physical damage, removable media slots

Cabling: what’s connected (network, USB, external drives)

Screen contents (single snapshot) — avoid unnecessary interaction

Unique marks, stickers, fingerprints (if relevant to physical chain)

3. Prepare Chain of Custody (CoC) — Record Before Transfer

Keep a CoC for every item. Record:

Case ID, Item ID, Type (HDD, USB, Mobile), Manufacturer/Model/Serial

Location found, date/time found, who found it, authority

Condition (on/off, locked, damaged)

Storage location, bag/seal ID

Signatures & timestamps for every handoff

Use NIST template; prepare and check metadata integrity.

4. Order of Volatility (Collect Most Volatile First)

Memory (RAM) — most volatile

CPU registers / caches / ephemeral OS state

Network connections, ARP cache, routing table

Processes & open handles (process list, open files)

Logs (e.g., syslog, Windows Event Logs in RAM before flush)

Disk (mounted file systems, slack space)

Removable media (USB, external disks)

Backups / archived media / cloud snapshots — least volatile

5. Live Response Collection (If Host Is Powered On)

Principles: Minimize commands that alter the system. Prefer read-only tools and capture full memory first.

Recommended volatile captures

Memory image (LiME, winpmem, DumpIt, AVML)

Network info: connections, listeners, routes, ARP

Process list and open files/handles

Logged-in users/sessions

DNS cache, schedules/startup items

List of mounted filesystems/devices

Windows Event Logs (export EVTX if feasible)

Windows example commands

netstat -ano > C:\forensics\netstat.txt
tasklist /V > C:\forensics\tasklist.txt
whoami /all > C:\forensics\whoami.txt
quser > C:\forensics\quser.txt
systeminfo > C:\forensics\systeminfo.txt
ipconfig /all > C:\forensics\ipconfig.txt
arp -a > C:\forensics\arp.txt
certutil -hashfile C:\forensics\memory.img SHA256


Linux example commands

ss -tulpn > /mnt/forensics/ss.txt
ps auxww > /mnt/forensics/ps_aux.txt
who > /mnt/forensics/who.txt
ip addr show > /mnt/forensics/ip_addr.txt
arp -n > /mnt/forensics/arp.txt
lsof -nP > /mnt/forensics/lsof.txt


Memory capture

Linux: LiME (kernel module) writing RAM image to remote/write-protected storage.

Windows: winpmem or DumpIt (or AVML) to acquire physical memory.

Always note the tool name, version, options, local time, and operator for provenance.

6. Removing & Securing the Medium (For Offline Imaging)

Re-photograph device and connections prior to movement.

Remove removable media (label and bag separately).

If powering down is required, record shutdown method and time.

Transport device in tamper-evident bag to a secure forensic workstation.

7. Forensic Imaging (Bit-for-Bit)

Principles: Use write-blocking for storage devices. Create a complete bitstream (raw or E01/AFF4). Compute hashes before/after.

Recommended hashing algorithms

Primary: SHA-256

Secondary (legacy compatibility): MD5 (note collision risk)

Linux imaging examples

sudo dd if=/dev/sdb of=/mnt/forensic/CASE2025-001_HOST-01_image.dd bs=4M conv=sync,noerror status=progress

sudo dc3dd if=/dev/sdb hash=sha256 hashlog=/mnt/forensic/CASE2025-001_hashlog.txt of=/mnt/forensic/CASE2025-001_image.dd

sha256sum /mnt/forensic/CASE2025-001_image.dd > /mnt/forensic/CASE2025-001_image.sha256
md5sum    /mnt/forensic/CASE2025-001_image.dd > /mnt/forensic/CASE2025-001_image.md5


Windows imaging + verification

Use FTK Imager (GUI) to create an E01 or raw image and generate hashes, or use dd ports/Guymager (via Linux).

Verify hashes:

CertUtil -hashfile C:\forensic\CASE2025-001_image.dd SHA256
CertUtil -hashfile C:\forensic\CASE2025-001_image.dd MD5


Imaging tips

Prefer E01/AFF when metadata & compression are desired (tool support permitting).

Capture the entire device (including unallocated and slack).

Log imaging start/end time, operator, tool & version, host system IDs.

Create and store a hash of the original device if possible (some tools compute on-the-fly).

8. Verify & Match Hashes

After imaging, compute hashes of the image (SHA-256, MD5).

If you captured the original device hash prior to imaging, compare.

Store hash values in CoC and in the forensic case file.

Verification example

sha256sum /mnt/forensic/CASE2025-001_image.dd > image.sha256
diff image.sha256 recorded_original.sha256


Record any mismatch and do not proceed with analysis until resolved (document everything).

9. Evidence Handling & Storage

Place original evidence in a tamper-evident bag. Seal and record seal ID.

Store originals in a secure evidence locker (locked, access logged).

Work from copies (forensic images) only. Never modify originals.

Maintain CoC entries for every person who touches the evidence.

10. Analysis (On Copies Only)

Mount forensic images read-only.

Document tools, versions, commands/options, and hashes of the image used for analysis.

Use timeline tools (plaso/Timesketch), carving (photorec/scalpel), full filesystem exploration, and artifact parsing (e.g., Windows Registry, Prefetch, browser history, email).

Keep an analysis log: queries run, search terms, results, timestamps.

Export exhibits as separate files and compute & record a hash for each exhibit.

11. Reporting

Produce a forensic report with:

Executive summary (concise)

Scope / authority / purpose

Chain of custody

Methodology (tools & versions)

Findings with timelines & artifacts

Hashes and verification statements

Limitations / assumptions

Appendices: full CoC, raw logs, commands used

Ensure the report is signed & dated by the examiner.

12. Legal & Privacy Considerations

Respect privacy laws (e.g., GDPR). Limit analysis to the scope of warrant/consent.

If encountering privileged content (attorney-client), isolate and seek legal counsel.

Keep logs and CoC defensible.
