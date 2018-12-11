# auto-email-mikrotik-backup
Auto Email Mikrotik Backup 

[https://wiki.mikrotik.com/wiki/Send_Backup_email](https://wiki.mikrotik.com/wiki/Send_Backup_email)


## Enable Allow less secure apps [Gmail]
enable "Allow less secure apps" Gmail melalui link berikut

[https://myaccount.google.com/security?utm_source=OGB&utm_medium=act&pli=1#connectedapps](https://myaccount.google.com/security?utm_source=OGB&utm_medium=act&pli=1#connectedapps)

![Allow less secure apps](https://raw.githubusercontent.com/laksa19/auto-email-mikrotik-backup/master/img/1.png)

## Setting Email Mikrotik [Tool --> Email]
![Setting Email Mikrotik](https://raw.githubusercontent.com/laksa19/auto-email-mikrotik-backup/master/img/2.png)

## Add Backup Script [System --> Script]
![Add Backup Script](https://raw.githubusercontent.com/laksa19/auto-email-mikrotik-backup/master/img/3.png)
### Detail
Name : backupEmail

Source : 
```

:log info "backup beginning now"
:global backupfile ("Backup-Mikrotik-Kemangi-" . [/system clock get time])
/system backup save name=$backupfile
:log info "backup pausing for 10s"
:delay 10s
:log info "backup being emailed"
/tool e-mail send to="email.penerima@gmail.com" subject=([/system identity get name] . \
" Backup") from=MikrotikKemangi file=$backupfile server=74.125.136.109
:log info "backup finished"

```
## Add Scheduler [System --> Scheduler]
On Event : backupEmail

![Add Scheduler](https://raw.githubusercontent.com/laksa19/auto-email-mikrotik-backup/master/img/4.png)

## Review
![Review](https://raw.githubusercontent.com/laksa19/auto-email-mikrotik-backup/master/img/5.png)
