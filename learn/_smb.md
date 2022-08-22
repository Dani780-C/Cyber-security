### Despre SMB:
    - Server Message Block
    - este un protocol de retea care faciliteaza comunicarea unui user cu host-uri remote (computere sau servere)
    - este un network file sharing protocol
    - user-ul poate folosi resursele host-ului remote, sa distribuie, sa deschida si sa editeze fisiere
    - se bazeaza pe o schema de protocol client-server
    - foloseste portul 139 pentru a comunica host-uri de pe aceeasi retea (run over NetBIOS)
    - foloseste portul 445 + protocolul TCP pentru a comunica host-uri din retele diferite (over the internet)
    - ex: avem un printer care e conectat la un host remote, atunci un client (alt device) poate folosi acel printer prin portocolul SMB
    - autentificarea SMB:
        - autentificare la nivel de user (user level): SMB cere un username si o parola pentru a-ti permite accesul pe server
        - autentificare la nivel de distribuire (share level): user-ul trebuie sa introduca o parola pentru a accesa un fisier sau chiar un server, dar nu este ceruta nicio identitate
    - in 1996, Microsoft a incercat sa redenumeasca SMB ca CIFS (Common Internet File System) (CIFS este o versiune updatata si cu functionalitati aditionale)
    - in 1992, Samba a aparut pe piata ca un produs gratuit care copia protocolul SMB pentru a fi folosit de sistemele de operare Unix
    - versiuni:
        - SMB 1.0 (CIFS): comunicarea s-a realizat cu ajutorul interfetei NetBIOS si cu ajutorul altor intefete de retea care foloseau porturile 137 si 138 pentru UDP si portul 139 pentru TCP
        - SMB 2.0, 2.1, 3.0, 3.1.1 au adus performanta sporita si o serie de protocoale de autentificare
    
   [What is SMB](https://mac.eltima.com/what-is-smb.html)  
   [How does SMB work](https://nordvpn.com/ro/blog/what-is-smb/)  
   [SMB Info](https://www.educba.com/what-is-smb/)  
   [NetBIOS](https://www.lifewire.com/netbios-software-protocol-818229)  
   [NetBIOS](https://miloserdov.org/?p=4261)  
   [Samba - Wiki](https://ro.wikipedia.org/wiki/Samba_(software))  
   [Samba - redhat docs](https://web.mit.edu/rhel-doc/5/RHEL-5-manual/Deployment_Guide-en-US/ch-samba.html)  
