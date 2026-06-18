# Mr. Robot CTF
**Platform:** TryHackMe | **Difficulty:** Medium

## Summary
A classic CTF room inspired by the Mr. Robot TV series involving web enumeration, WordPress exploitation, password cracking, reverse shells, and Linux privilege escalation to secure three hidden keys.

## What I Did
* Performed reconnaissance using Nmap to discover open web ports (80/443).
* Enumerated directories with Gobuster and extracted a custom wordlist (`fsocity.dic`) and the first flag from `robots.txt`.
* Used Hydra with the custom wordlist to isolate a valid WordPress username (`Elliot`).
* Discovered and decoded a hidden Base64 string within the `/license` source code to obtain the login password.
* Gained an initial foothold as the `daemon` user by dropping a PHP reverse shell into the WordPress Theme Editor (`footer.php`).
* Upgraded the shell environment via Python and harvested an MD5 password hash from the `/home/robot` directory.
* Cracked the MD5 hash offline using John the Ripper and the `rockyou.txt` wordlist to elevate privileges to the `robot` user.
* Conducted a local SUID binary search and identified an outdated, vulnerable Nmap executable.
* Exploited Nmap's legacy interactive mode (`--interactive` and `!sh`) to break out into a root shell and extract the final flag.

## Tools Used
Nmap, Gobuster, Hydra, John the Ripper, Netcat, Python, WordPress Editor, Linux CLI

## Key Takeaways
* **Web Recon is Vital:** Critical assets like custom dictionaries or credentials can be hidden in standard endpoints like `robots.txt` or tucked inside source code comments.
* **Leaked Error Messages:** WordPress login panels are vulnerable to username enumeration if error messages differentiate between a bad username and a bad password.
* **SUID Enumeration First:** When trying to elevate privileges on Linux, checking for SUID binaries should always be one of the very first manual checks. Older versions of common tools (like Nmap 3.81) often have built-in shell escapes.
