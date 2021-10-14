# Directory Service

## Active Directory (AD) 

- developed by Microsoft
- manages Data across multiple services
   - e.g. moodle, mail, hub, School WLAN
- Servers communicate with each other
- Users, Devices and Groups 
    - A group can contain devices and/or Users
    - Security Groups, Distribution Groups (email)

### How it works

1. Database is created initially
    1. If a User is created => Credentials will be stored in the db
    2. Same for devices
2. Multimaster replication
    1. Once another server joins the system, the database is replicated onto it
    2. Changes are immediately replicated onto all other servers

3. Changes cannot be done at the same time. 

### Domain Controller (DC)

Windows server with Active Directory

- Uses AD-DS (domain service)
    - There are also
        - AD-CS (Certificate Service)
        - AD-FS (Federation Service)
        - AD-LDS (Lightweight Directory Services)
        - AD-RMS (Rights Management Services)
- Install a Role with AD-DS 
    - This means: Server role will be installed => Active Directory Domain Service
- AD-DS needs DNS to work
    - Because the host has to know where and how to connect to the Domain Controller

- domain name consists of at least 2 domain components (DC)
    - e.g. htl-wien5.schule, 4ehif.local
        - schule would be the top level domain and the first in a structure of a domain
        - htl-wien5 the second level domain
            - both are domain components
- Organizational Units (OU)
    - Group Policies can be applied to OUs
        - Group Policies exist of many Group Policy Objects (basically the rules)
    - Devices, Users or Groups can be OUs
    - But OUs can also represent locations (sites) or rooms
    
Example: Exam Lab (OU) => Disable Internet (Group Policy)

#### Example structure of a domain 

Domain Name: htl-wien5.schule

- schule (DC)
    - htl-wien5 (DC)
        - schueler (OU)
            - HIF (OU)
        - lehrer (OU)
        - rooms (OU)
            - B3.11 (OU)
    
#### DNS
www.spengergasse.at = fully qualified domain name

www = host

spengergasse.at = domain name

DNS Resource Records
   - A = IPv4 (32 bit)
        - Syntax example:  www.spengergasse.at A 172.18.9.16
   - AAAA = IPv6 (128 bit)
        - Syntax example:  www.spengergasse.at A 2001:db8:ac78:000A::16
   - PTR = reverse DNS lookup (IP address returns a domain)
        - used for security reasons (to check if the ip really belongs to the domain)
        - Syntax example:  172.18.9.16 PTR www.spengergasse.at
   - CNAME = alias (points to other hosts)
        - used to link:
        - Syntax example:
            - spengergasse.at A IPv4 address
            - www.spengergasse.at CNAME spengergasse.at
            - cloud.spengergass.at CNAME spengergasse.at
        - if you change the ip of spengergasse.at the ip will be changed for every CNAME too
        - Same as:
            - spengergasse.at A IPv4 address
            - www.spengergasse.at A same IPv4 address
            - cloud.spengergass.at A same IPv4 address
   - MX(Mail eXchange): 
        - tells a domain name to receive mails from a dedicated mail server
        - links the @xxx part to the mail server
        - the number is the priority (1-10) 1 being high and 10 being low
        - Syntax example:  spengergasse.at MX 5 mail.spengergasse.at
   - SRV(Service Record): 
        - Dynamic Record for locating Domain Controllers within a specified protocoll
        - LINK: https://de.wikipedia.org/wiki/SRV_Resource_Record#Aufbau (recht kompliziert)
        - Basic Syntax for understanding:
            - LDAP SRV DC1
            - `<AD service> SRV <Domain Controller zuständig dafür (meistens der erste DC)>`
               
   
#### vhost
inspects the HTTP header to determine, which starting page is needed
   - all requests are received on port 80/443 (HTTP GET)
   - two domain names: gaming.at , spengergasse.at
   - vhost inspects the given domain name (gaming.at / spengergasse.at)
        - gets the information from the HTTP GET request (HTTP header displays domain)
   - returns the correct starting page over port 80
   - > makes port dependency redundant
