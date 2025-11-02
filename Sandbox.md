#Using the Sandbox

To savely detonate malware and or analyze files in a secure environemtn, utilize the forensic workstation.
1. Move the files for analysis in the shared folder on the Desktop-
2. Start virtual box
     -For Windows analysis use Flare VM
     -For Linux use Remnux
3. Conduct your analysis and record findings
        -Utilize Yara or Snort to check for Malware signatures
        -DAST Tools for runtime assessments
        -SAST for code review if possible
   Be a smart cookie and go to Flares or Remnux webpages for detailed how to guides.
   https://docs.remnux.org/discover-the-tools/investigate+system+interactions
   https://cloud.google.com/blog/topics/threat-intelligence/flarevm-open-to-public/
###I could not find a lot on Flare VM, but it is probaly worth it to do the THM room for both solutions
5. Purge data on host system with Systools Datawipe

 Remember the VMs are snapshotted and use a clean snapshot for each engagement
