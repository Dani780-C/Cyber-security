### Despre FTP:
  
    - File Transfer Protocol
    - port-ul default este 21
    - protocol creat pentru a transfera fisiere intre hosturi (se bazeaza pe o arhitectura client-server)
    - datele nu sunt criptate
    - accesarea unui server FTP: intr-un web-browser ftp://<adresa serverului> sau printr-o aplicatie (ex: FileZilla)
    - foloseste doua conexiuni(canale)
          - Control Channel pentru creearea unei conexiuni
          - Data Channel pentru transferul de fisiere (este inchis dupa fiecare transfer [one file per connection])
                - Active Mode: serverul foloseste portul 20 pentru a crea un canal de transfer de fisiere pentru client (probleme cu firewall-ul daca nu este configurat sa lase serverul sa creeze o conexiune catre client)
                               conexiunea se va face de la server catre client (port server: 20 | port client: random)
                - Passive Mode: clientul initiaza sesiunea pentru transferul de date
                               conexiunea se va dace de la client catre server (port server: random | port client: random)
    - some status codes:
          - 125 data connection already open; transfer starting
          - 220 Service ready pentru un nou user
          - 331 username-ul ete ok, se asteapta o parola
          - 425 nu se poate deschide un 'data channel'
          - 553 request-ul facut nu a putut fi realizat de catre server (file name not allowed)
    - nu verifica identitatea server-ului
    - foloseste TCP ca layer de transport
    - de obicei un client FTP trebuie sa se autentifice, dar unele servere fac content public (Anonymous FTP)
    
### Despre FTPS:

    - FTP Secure or FTP SSL(Secure Socket Layer)
    - extensie FTP care suporta utilizarea TLS si SSL encryption
    - datele sunt criptate
    - foloseste portul 21 sau 990
    - verifica identitatea server-ului
    - FTP over TLS Explicit
         - foloseste portul 21
         - clientul trimite o comanda startTLS pentru a incepe o conexiune securizata
    - FTP over TLS Implicit
         - foloseste oprtul 990
         - comunicarea e securizata de la inceput
    
### Despre TFTP:

    - Trivial File Transfer Protocol
    - foloseste UDP ca layer de transport 
    - foloseste portul 69
    - nu se face autentificare
    - in cazul transferului de fisiere de la server catre client (download), serverul trimite de pe alt port datele pe portul clientului care a inceput conexiunea
    - in cazul transferului de fisiere de la client catre server (upload), serverul trimite prima data un ACK clientului pentru a-i spune pe ce port sa trimita datele, iar clientul incepe apoi sa trimita datele
    - https://www.youtube.com/watch?v=NbnSdWUQFhU

### FTPS nu trebuie confundat cu SFTP:

    - SFTP (SSH File Transfer Protocol) este o extensie a serviciului SSH 

#### SSL (Secure Socket Layer)

    - tehnologie folosita pentru securitatea datelor intre doua host-uri
    - foloseste certificate digitale si data encryption pentru a verifica identitatea server-ului si pentru a asigura securitatea datelor
  
#### TLS (Transport Layer Security)
  
    - succesorul lui SSL
    - foloseste algoritmi mai puternici de criptare si este mai sigur decat SSL

