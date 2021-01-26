# syncftp
Simple utility in REXX to send all PDS members updates in the last # days to a PDS via FTP

SyncFTP - send selected PDS members based on age from        
          the local system to a remote system via FTP.       
                                                             
The age is the number of days since the member was changed   
and is determined by using the PDS (CBT File 182) command.   
                                                             
Syntax:                                                      
         %syncftp fromds tods target_ip age -p port          
                                                             
         fromds is the source dataset (ps or pds)            
         tods is the target dataset name (same dcb)          
              may be = if same name as fromds                
         target_ip is the IP (or name) of target LPAR        
         age - # of days to use to identify changed          
             members to sync (default is 3)                  
         -p port defines the port to use (default 21)        
                                                             
Notes:                                                       
                                                             
    1. An AGE of 0 will select members updated today.             
                                                                  
    2. To prevent prompting for userid and password a             
       NETRC dataset is required. It must be named:               
       userid.NETRC (e.g. LIONELD.NETRC)                          
                                                                  
    3. The NETRC format is RECFM(V B) LRECL(255) BLKSIZE(0)       
                                                                  
       The records layout is:                                     
                                                                  
       MACHINE ip-address LOGIN userid PASSWORD password          
   or  MACHINE host-name  LOGIN userid PASSWORD password          
                                                                  
    4. The NETRC dataset should be protected using the            
       Security manager installed (RACF,ACF2,TSS) to prevent      
       others from reading it. The installation can generate      
       a rule to do this for all users. Contact your security     
       administrator about this.    
       
    5. This exec requires the PDS command found on the 
       CBTTape (www.cbttape.org) in file 182.          
