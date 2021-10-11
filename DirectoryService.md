# Directory Service

## Active Directory (AD) 

- developed by Microsoft
- manages Data across multiple services
   - e.g. moodle, mail, hub, School WLAN
- Servers communicate with each other
- Users, PCs and Groups
    - A group can contain PCs and/or Users
    - Security Groups, Distribution Groups (email)

### How it works

1. Database with users, passwords etc. is created initially
2. Once another server joins the system, the database is replicated onto it
3. Changes are immediately replicated onto all other servers

- Changes cannot be done at the same time. 

### Domain Controller (DC)

- Uses AD-DS (domain service)
- Install a Role with AD-DS 
- AD-DS needs DNS to work

- domain name consists of at least 2 domain components (DC)
    - e.g. htl-wien5.schule, 4ehif.local
- Organizational Units (OU)
    - Groups or PCs can be part of an OUw
- Group Policy Objects (GPO) can be assigned to OUs, locally, sites or on the whole domain
    - e.g. Exam Labs: certain functionality can be en/disabled (internet access)

#### Example structure of a domain 

- schule (DC)
    - htl-wien5 (DC)
        - schueler (OU)
            - HIF (OU)
        - lehrer (OU)
    
#### DNS
www.spengergasse.at = fully qualified domain name
www = host
spengergasse.at = domain name

DNS Resource Records
   - A = IPv4 (32 bit)
   - AAAA = IPv6 (128 bit)
   - PTR = reverse DNS (IP address returns a domain)
   - CNAME = alias (points to other hosts)
   
#### vhost
inspects the HTTP header to determine, which starting page is needed
   - all requests are received on port 80/443 (HTTP GET)
   - two domain names: gaming.at , spengergasse.at
   - vhost inspects the given domain name (gaming.at / spengergasse.at)
   - returns the correct starting page over port 80
   - > makes port dependency redundant
