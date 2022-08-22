### Atac SMB:
  
  - [Despre SMB](https://github.com/Dani780-C/Cyber-security/blob/main/learn/_smb.md)
  - versiune: *Samba 3.0.20*
  - Pasii atacului:
               
         nmap -sSV 192.168.56.102 -p139,445
         
    ![My Image](https://github.com/Dani780-C/Cyber-security/blob/main/attacks/imgs/nmap-scan-samba.png)

    Pentru a descoperi versiunea finala a serviciului, putem folosi tool-ul [smbclient](https://github.com/Dani780-C/Cyber-security/blob/main/tools/smbclient.md).
