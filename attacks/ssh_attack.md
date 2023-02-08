### Atac SSH:

   - [Despre SSH](https://github.com/Dani780-C/Cyber-security/blob/main/learn/_ssh.md)
   - versiune: *OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)*
   - Pasii atacului:
         
         nmap -sSV 192.168.56.102 -p22
     ##### Explicatii comanda:
      - nmap command <!-- (https://github.com/Dani780-C/Cyber-security/blob/main/tools/nmap.md) -->
      - 192.168.56.102 <-> adresa IP a tintei (Metasploitable 2)
      - -p22 <-> scanam doar portul 22 (SSH foloseste portul 22 pentru server)
     
      ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/nmap-ssh-p22.png)
   
      Pentru atacul asupra serviciului SSH am folosit metoda brute-force cu ajutorul tool-ului `hydra` <!--(https://github.com/Dani780-C/Cyber-security/blob/main/tools/hydra.md).-->
         
         hydra -t 4 -L users.txt -P passwords.txt 192.168.56.102 ssh
     ##### Explicatii comanda:
      - hydra tool <!-- (https://github.com/Dani780-C/Cyber-security/blob/main/tools/hydra.md) -->
      - users.txt <-> fisier in care sunt scrise diferite nume de useri
      - passwords.txt <-> fisier in care sunt scrise diferite parole
      - 192.168.56.102 <-> adresa IP a tintei (Metasploitable 2)
      - ssh <-> serviciul pentru care se incearca metoda brute-force
      
      ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/ssh-brute-force.png)
      
      Dupa executarea comenzii, au fost gasite credentialele: *user:user* si *msfadmin:msfadmin*.  
      Acum putem folosi serviciul SSH pentru a ne conecta la serverul remote cu ajutorul credentialelor gasite.
      
      ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/msfadmin-ssh-login.png)

   - Analiza trafic:
      - [Captura traficului pentru serviciului SSH in timpul atacului](https://github.com/Dani780-C/Cyber-security/blob/main/captures/ssh-traffic-while-attack.pcapng)
