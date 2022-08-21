### Despre SSH:
  
    - Secure Shell Protocol
    - creat pentru a accesa, controla si modifica servere remote
    - a fost dezvoltat ca o alternativa sigura a protocolului Telnet (Telnet nu este criptat)
    - serviciul SSH foloseste tehnici de criptare pentru a facilita comunicarea sigura dintre client si server
    - portul pe care il foloseste un serviciu SSH este 22
    - utilizare: ssh {user}@{host} pentru Mac si Linux, iar pentru Windows este nevoie de un SSH client precum PuTTY
          - user <-> contul pe care vrei sa-l accesezi (de exemplu, daca vrei sa folosesti contul de root, atunci {user} = root)
          - host <-> computer-ul pe care vrei sa-l accesezi (poate fi o adresa IP sau un domain name)
          - ex: ssh root@192.168.56.102 sau ssh root@metasploitable
    - foloseste 3 tehnologii de criptare:
          - criptare simetrica (symmetrical encryption)
          - criptare asimetrica (asymmetrical encryption)
          - hashing
    - 
