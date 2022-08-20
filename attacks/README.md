### Atac FTP:

   - versiune: *vsftpd 2.3.4*
   [In 2011, in arhiva de pe site-ul oficial al serviciului FTP a fost atasat un virus backdoor care executa un shell pe portul 6200. Pentru a executa virusul, username-ul folosit la conectarea serviciului FTP putea fi oricare sir de caractere urmat de un ":)"]

   - Pasii atacului:
      
         nmap -sSV 192.168.56.102 -p21,6200
     ##### Explicatii comanda:
            nmap <-> tool pentru a scana servicii
            -sSV <-> Stealth scan version
            192.168.56.102 <-> adresa IP a tintei (Metaplsoitable 2)
            -p21,6200 <-> scanam doar porturile 21 si 6200
         
   ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ftp-nmap-1.png)
