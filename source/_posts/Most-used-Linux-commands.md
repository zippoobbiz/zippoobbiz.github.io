---
title: Most used Linux commands
date: 2017-05-13 12:22:32
tags: [Linux, CLI]
categories: [Tools, Linux]
---
Unzip bz2 keep the original file
`bzip2 -dk filename.bz2`

Find out the current Linux version
`cat /etc/*-release`

`ssh-keygen -f id_rsa -p`

Check hardware
`lshw`

Change java version
`update-alternatives -config java`

Change mode
`chmod + xxx.sh`

`ls -lah`
`bzgrep / zgrep / grep “something” xxx.log | xmlprettify | less ( xmlbroswerfy > xxx.html)`

`zgrep RES xxxx.log | grep -v SUCCESS | less (what is grep -v)`

`tail -2 xxx.log | xmlprettify`
`cat xxx.log | xmlprettify`

bring job to foreground
`fg`

put thread to background
`bg`

setup public key on server
`cat ~/.ssh/id_rsa.pub | ssh user@hostname 'cat >> .ssh/authorized_keys'`

`find . -type f -name '*.bz2' -size +0c | while read line; do /bin/bzip2 -dc $line |/usr/bin/xz --best -c > "../xz/${line%.bz2}.xz"; cat /dev/null > $line ; done`

`zgrep something log_name | cut -d "/" -f 2-4 | sort | uniq`

`tar ????`

$$ is the process ID (PID) of the script itself.

`echo ${HOSTNAME%%.*}` 两个百分号移除结尾的.后面的东西

“2> /dev/null” 代表忽略掉错误提示信息。
* 0 -- stdin
* 1 -- stdout
* 2 -- stderr

change onwership
```bash
sudo chown -R phillipxu: /usr/local/lib
```
![cli](/cli.png "cli")