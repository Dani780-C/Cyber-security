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
     
