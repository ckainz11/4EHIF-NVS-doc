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


#### DNS Resource Records (bitte an Pauls Abschnitt anhängen @chri)

- MX(Mail eXchange): tells a domain name to receive mails from a dedicated mail server
         Syntax example:  gmail.com MX mail1.gmail.com

- SRV(Service): Dynamic Record for locating Domain Controllers within a specified protocoll
         Syntax: https://de.wikipedia.org/wiki/SRV_Resource_Record#Aufbau (recht kompliziert)
