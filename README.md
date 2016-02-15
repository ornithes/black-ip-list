Hi. 

IP list:

- My list
- (17 - 1121) Cinnscore bad guys list : http://cinsscore.com/list/ci-badguys.txt 15/2/16

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
#update ip list
0 4 * * 2 /updatelist.sh 
```

ufw cleaner

`while read line; do sudo ufw delete deny from $line; done < updatelist.txt`
