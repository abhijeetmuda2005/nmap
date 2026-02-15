# Nmap Localhost Scan Results

## Objective
Network scan on Windows localhost to identify open ports/services.

## Nmap Command Used
nmap -- version to verify installation
nmap localhost for a quick scan of the top 1000 ports on the machine
nmap -sV -oN nmap_scan_results.txt localhost to detect service versions and save them to a text file

## Key Findings (Updated Scan)
- **Port 135/tcp open: msrpc** - Microsoft Windows RPC endpoint mapper. Essential for Windows operations but high-risk for DCOM exploits and lateral movement attacks.
- **Port 445/tcp open: microsoft-ds** - SMB file/printer sharing. Critical vulnerability target (EternalBlue, WannaCry ransomware). Common attack vector.
- **Ports 25,110,548/tcp filtered** - SMTP, POP3, AFP blocked by firewall. Correct configuration—prevents external access.

**OS Detection**: Confirmed Windows via service fingerprints.

## Security Risk Summary
| Port | Service | State | Risk Level | Recommendation |
|------|---------|-------|------------|----------------|
| 135  | msrpc   | open  | **HIGH**   | Allow only local access via firewall |
| 445  | microsoft-ds | open | **CRITICAL** | Disable SMBv1; block inbound 445 TCP |
| 25   | smtp    | filtered | **LOW**  |  Good - firewall blocking |
| 110  | pop3    | filtered | **LOW**  |  Good - firewall blocking |
| 548  | afp     | filtered | **LOW**  |  Good - firewall blocking |
