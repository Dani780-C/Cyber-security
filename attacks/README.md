### Atac FTP:

    - versiune: vsftpd 2.3.4
      [In 2011, in arhiva de pe site-ul oficial al serviciului FTP a fost atasat un virus backdoor care executa un shell pe portul 6200. Pentru a executa virusul, username-ul folosit la conectarea serviciului FTP putea fi oricare sir de caractere urmat de un ":)"]

    - Pasii atacului:
      
      1. nmap -sSV 192.168.56.102 -p21,6200
         []
         
         ![My Image](imgs/ftp-nmap-1.png)
