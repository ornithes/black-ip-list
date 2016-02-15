Hi. 

Update : 15/2/2016

IP list:

- My list
- Cinnscore bad guys list : http://cinsscore.com/list/ci-badguys.txt 
- Tor list : https://check.torproject.org/cgi-bin/TorBulkExitList.py?ip=1.1.1.1 
- greensnow : http://blocklist.greensnow.co/greensnow.txt
- openpl : https://www.openbl.org/lists/base.txt
- blocklistde : https://lists.blocklist.de/lists/all.txt
- stopfromspam : https://www.stopforumspam.com/downloads/toxic_ip_cidr.txt

## Install

- UFW settings

```
ufw allow ssh
ufw allow http
ufw allow https
ufw enable
```

- Path to let go

`cd /`

- Let's create our necessary files

`nano updatelist.sh`

- copy + paste

```
#!/bin/bash
cd /
rm -rf black-ip-list
git clone https://github.com/pikshub/black-ip-list.git
cd black-ip-list
while read line; do sudo ufw deny from $line to any; done < iplist.txt
exit
```

- Let's permission

`chmod +x updatelist.sh`

- and finish:

`./updatelist.sh`

Auto update

cronjob edit

`crontab -e`

Add to the bottom

```
MAILTO=”mail@example.com”
#update ip list - monthly
0 0 1 * * /updatelist.sh 
```

ufw cleaner

`while read line; do sudo ufw delete deny from $line; done < iplist.txt`
