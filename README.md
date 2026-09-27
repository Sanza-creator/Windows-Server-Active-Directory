# Windows Server Infrastructure — Multi-Office AD/DNS/DHCP/IIS Pilot

### Scenario
Meridian Knowledge Partners, a research and advisory firm operating a central office and a satellite office, had inconsistent, manually-configured systems: no central identity management, uneven file access control, and no policy enforcement. I built a Windows Server 2019 pilot environment to demonstrate a centralised, secured, production-ready alternative across three divisions (Governance, Client Support, Data Services).

### What I did
- **Infrastructure design:** Deployed two Windows Server 2019 VMs with roles split across an infrastructure server (AD DS, DNS, DHCP, GPO) and a services server (File Services, IIS, AD CS) — separating core infrastructure from service delivery for cleaner future scaling
- **Domain & identity:** Promoted the infrastructure server to a Domain Controller for a new forest (`meridian.local`), designed an OU structure by division/computers/users, created staff and computer accounts under a consistent naming convention, and domain-joined three-plus client machines
- **Network services:** Configured DNS (forward and reverse lookup zones, host records) and DHCP (scoped to `10.10.50.0/24`, authorised in AD) including static reservations for specific workstations; verified resolution with `nslookup` and confirmed lease allocation
- **Controlled resource access:** Created a restricted Governance-only file share with permissions verified for both authorised and non-authorised users
- **Group Policy:** Built and linked GPOs enforcing: USB storage restriction for Governance users, Command Prompt/Remote Desktop access for Data Services, a locked-down standard user experience (disabled Control Panel, redirected Documents, standard wallpaper), and a domain-wide password policy (history, age, minimum length, complexity)
- **Internal PKI & secure web delivery:** Installed AD CS and configured an Enterprise Root CA, enabled certificate auto-enrolment for domain-joined machines, and issued a CA-backed (not self-signed) certificate for an internal HTTPS portal hosted on IIS
- **Hardening & monitoring:** Enabled Windows Firewall (permitting only RDP/DNS/DHCP/HTTP(S)), disabled unnecessary services, and enabled auditing for logon events, account management, and object access — reviewed via Event Viewer

### Why this design
An internal CA was used instead of a self-signed certificate so that domain-joined clients would automatically trust the portal without manual certificate exceptions — reflecting how a real production environment establishes trust. Splitting infrastructure and service roles across two servers reflected best practice for future scaling beyond a single all-in-one box.

### Skills demonstrated
`Active Directory Domain Services` · `Group Policy Management` · `DNS/DHCP` · `AD Certificate Services (Enterprise CA)` · `IIS (HTTPS)` · `Windows Firewall & auditing` · `Access control design`


