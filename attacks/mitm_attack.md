### Atac MITM (Man-in-the-middle):
  - [Despre MITM](https://github.com/Dani780-C/Cyber-security/blob/main/learn/mitm.md)
  - Scopul atacului: dobandirea credentialelor unui user care se conecteaza de pe masina cu Windows 11 la masina Metasploitable 2 folosind protocolul *telnet*
  - Pasii atacului:
    - Vom folosi tool-ul [ettercap](https://github.com/Dani780-C/Cyber-security/blob/main/tools/ettercap.md)(*ettercap-graphical*) pentru a redirectiona traficul dintre cele doua host-uri Metasploitable 2 si Windows 11.
    - Atacul facut de mine se bazeaza pe tehnica [ARP poisoning](https://github.com/Dani780-C/Cyber-security/blob/main/learn/arp_poisoning.md).
    - Primul pas este sa permitem masinii noastre(cea de pe care efectuam atacul) sa trimita mai departe pachetele primite chiar daca nu sunt pentru ea.
          
          sysctl net.ipv4.ip_forward=1
          
    - Putina analiza a tabelelor ARP(ARP cache):  
          - folosind comanda *arp -a* vom putea vedea tabela ARP cu informatiile despre mapping-ul adreselor IP a masinilor de pe retea cu adresele lor MAC.  
          - **Pe masina cu Windows 11**:  
            
         ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/arp_cache_win11.png)  
          - **Pe masina Metasploitable 2**:  
           
         ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/arp_cache_meta2.png)  
          
          Observam ca 192.168.56.101 (Kali) are adresa fizica(MAC) 08:00:27:95:bd:54  
          Observam ca 192.168.56.102 (Metasploitable 2) are adresa fizica(MAC) 08:00:27:c1:21:7a 
          Observam ca 192.168.56.103 (Windows 11) are adresa fizica(MAC) 08:00:27:3f:f0:6b
      
    - Vom deschide ettercap-graphical pentru a incepe atacul. 
    
          Scanam cu ettercap pentru host-urile active pe retea.  
          Vom fixa 192.168.56.102(Metasploitable 2) ca Target 1  
          Vom fixa 192.168.56.103(Windows 11) ca Target 2  
            
         ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/add-targets-ettercap.png)  
         
          Vom intra in meniul tool-ului ettercap si vom selecta metoda de atac ARP poisoning  
            
         ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/start_arp_poisoning.png)  
    - Inca putina analiza a tabelelor ARP(ARP cache):  
          - **Pe masina cu Windows 11**:  
            
         ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/arp_cache_win11_poisoned.png)  
          - **Pe masina Metasploitable 2**:  
           
         ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/arp_cache_meta2_poisoned.png)  
            
          Masina Metasploitable 2 crede ca la adresa MAC ~95:bd:54 se afla masina Windows 11 cu adresa 192.168.56.103  
          Masina Windows 11 crede ca la adresa MAC ~95:bd:54 se afla masina Metasploitable 2 cu adresa 192.168.56.102  
          ARP cache-ul celor doua masini tinta(Windows 11 si Metasploitable 2) a fost alterat  
      
    - Sa incercam sa ne conectam cu protocolul *telnet* de pe masina Windows 11 la Metasploitable 2 cu credentialele *msfadmin:msfadmin*:
          
          telnet 192.168.56.102
          
    - Pe masina Kali vom intercepta traficul pentru a obtine credentialele:  
        
      ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/mitm_get_credentials.png)
  - Analiza trafic:
     - [Captura traficului in tipul atacului de tip man-in-the-middle(MITM)](https://github.com/Dani780-C/Cyber-security/blob/main/captures/mitm_attack_traffic.pcapng)  
