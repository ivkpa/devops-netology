3.6.1  
  
1. HTTP/1.1 301 Moved Permanently is used for permanent redirecting
2. 307 Internal Redirect  
![F12](https://github.com/ivkpa/devops-netology/blob/main/images/3.6.1-2-1.png)
3. 109.195.102.158
4. CJSC "ER-Telecom Holding" Yekaterinburg branch AS51604 
5. AS51604, AS15169
```
Трассировка маршрута к dns.google [8.8.8.8]
с максимальным числом прыжков 30:

  1    <1 мс    <1 мс    <1 мс  MI-3 [192.168.1.1]
  2    <1 мс    <1 мс    <1 мс  dynamicip-109-195-110-125.pppoe.ekat.ertelecom.ru [109.195.110.125]
  3     2 ms    <1 мс    <1 мс  lag-3-438.bgw01.ekat.ertelecom.ru [109.195.104.30]
  4    23 ms    23 ms    23 ms  72.14.215.165
  5    27 ms    27 ms    27 ms  72.14.215.166
  6    27 ms    27 ms    27 ms  142.251.53.69
  7    24 ms     *        *     108.170.250.113
  8     *        *        *     Превышен интервал ожидания для запроса.
  9    61 ms    32 ms    32 ms  216.239.48.224
 10    33 ms    34 ms    33 ms  172.253.70.49
 11     *        *        *     Превышен интервал ожидания для запроса.
 12     *        *        *     Превышен интервал ожидания для запроса.
 13     *        *        *     Превышен интервал ожидания для запроса.
 14     *        *        *     Превышен интервал ожидания для запроса.
 15     *        *        *     Превышен интервал ожидания для запроса.
 16     *        *        *     Превышен интервал ожидания для запроса.
 17     *        *        *     Превышен интервал ожидания для запроса.
 18     *        *        *     Превышен интервал ожидания для запроса.
 19     *        *        *     Превышен интервал ожидания для запроса.
 20    32 ms    32 ms    32 ms  dns.google [8.8.8.8]

Трассировка завершена.
 ```
6. 216.239.48.224 36.3 ms avg  
7. `dig dns.google ns | grep zdns`  
`dig dns.google | grep 8.8.`
8. `dig -x 8.8.8.8 | grep dns.google.`  
`dig -x 8.8.4.4 | grep dns.google.`

3.5  
1. Файл, в котором последовательности нулевых байтов заменены на информацию об этих последовательностях (список дыр).  
2. Нет. Потому что это один и тот же объект.  
3. done
4. fdisk /dev/sdb  
5. sfdisk -d /dev/sdb | sfdisk --force /dev/sdc
6. `mdadm --create --verbose /dev/md0 --level=mirror --raid-devices=2 /dev/sdb1 /dev/sdc1`  
7. `mdadm --create --verbose /dev/md1 --level=stripe --raid-devices=2 /dev/sdb2 /dev/sdc2`  
8. `pvcreate /dev/md0`  
`pvcreate /dev/md1`  
9. `vgcreate vg01 /dev/md0 /dev/md1`
10. `lvcreate -L 100 -nlvol0 vg01 /dev/md1`  
11. `mkfs.ext4 /dev/vg01/lvol0`  
12. `mkdir /tmp/new`  
`mount /dev/vg01/lvol0 /tmp/new`  
13. `wget https://mirror.yandex.ru/ubuntu/ls-lR.gz -O /tmp/new/test.gz`
14. `lsblk`  
```
NAME                 MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
sda                    8:0    0   64G  0 disk
├─sda1                 8:1    0  512M  0 part  /boot/efi
├─sda2                 8:2    0    1K  0 part
└─sda5                 8:5    0 63.5G  0 part
  ├─vgvagrant-root   253:0    0 62.6G  0 lvm   /
  └─vgvagrant-swap_1 253:1    0  980M  0 lvm   [SWAP]
sdb                    8:16   0  2.5G  0 disk
├─sdb1                 8:17   0    2G  0 part
│ └─md0                9:0    0    2G  0 raid1
└─sdb2                 8:18   0  511M  0 part
  └─md1                9:1    0 1018M  0 raid0
    └─vg01-lvol0     253:2    0  100M  0 lvm   /tmp/new
sdc                    8:32   0  2.5G  0 disk
├─sdc1                 8:33   0    2G  0 part
│ └─md0                9:0    0    2G  0 raid1
└─sdc2                 8:34   0  511M  0 part
  └─md1                9:1    0 1018M  0 raid0
    └─vg01-lvol0     253:2    0  100M  0 lvm   /tmp/new
```
15. 0
16. `pvmove /dev/md1 /dev/md0`  
17. ` mdadm --fail /dev/md0 /dev/sdb1`
18. `dmesg | tail -n 2`  
```
[263060.848042] md/raid1:md0: Disk failure on sdb1, disabling device.
                md/raid1:md0: Operation continuing on 1 devices.
```
19. 0
20. done  


3.4.2  
  
1. done
2. CPU - `node_cpu_seconds_total{cpu="0",mode="system"}`  
Memory - `node_memory_MemTotal_bytes - node_memory_MemFree_bytes`  
Disk - `node_disk_io_time_seconds_total{device="sda"}`  
Network - `node_network_receive_bytes_total{device="enp0s3"}`
3. done
4. y  
CPU MTRRs all blank - virtualized system.  
systemd[1]: Detected virtualization oracle. 
5. `sysctl -a | grep fs.nr_open`  
fs.nr_open = 1048576  
fs.nr_open is a limit for fd open  
`ulimit -n` aswell
6. root@ubuntu:/# `ps aux`  
```
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND  
root           1  0.0  0.0   5476   592 pts/2    S    18:22   0:00 sleep 1h  
root           2  0.2  0.1   8284  5252 pts/2    S    18:23   0:00 -bash  
root          14  0.0  0.0   8892  3288 pts/2    R+   18:23   0:00 ps aux  
```
7. fork bomb  
: - function name  
\[Fri Nov 26 18:35:56 2021\] cgroup: fork rejected by pids controller in /user.slice/user-1000.slice/session-1.scope  
`ulimit -u 50` helps to limit amount of processes per user

3.3.1  

1. `chdir("/tmp")`  
2. `/etc/magic`  
`/usr/share/misc/magic.mgc`  
3. `ls -l /proc/<pid>/fd` - находим fd удаленного файла (скорее всего 1)  
\> `/proc/<pid>/fd/<fd>` (очищаем файл)  
4. Нет. Если не считать немного памяти для хранения информации о нём.  
5. /var/run/utmp  
/usr/local/share/dbus-1/system-services  
/usr/share/dbus-1/system-services  
/lib/dbus-1/system-services  
/var/lib/snapd/dbus-1/system-services/  
6. Part of the utsname information is also accessible via /proc/sys/kernel/{ostype, hostname, osrelease, version, domainname}.  
7. ";" commands separated by a ; are executed sequentially. The shell waits for each command to terminate in turn.  
"&&" command after && is executed if, and only if, command before && returns an exit status of zero  
Смысла нет, т.к. при использовании set -e в случае возврата любой из подкомманд exit code != 0 скрипт автоматически завершается  
8. -e  Exit immediately if a command exits with a non-zero status.  
-u  Treat unset variables as an error when substituting.  
-x  Print commands and their arguments as they are executed.  
-o pipefail     the return value of a pipeline is the status of the last command to exit with a non-zero status, or zero if no command exited with a non-zero status  
Хорошо использовать в сценариях т.к. с этими опциями написанный код лучше проверяется на корректность и его проще диагностировать в случае каких-либо ошибок или некорректной работы.  
9. S - interruptible sleep (waiting for an event to complete)  

---------------------------------------------------------------------------------------------------
3.2.2  

1. cd is a shell builtin  
*(Чисто теоретически это могла бы быть функция, изменяющая значение переменной $PWD,   
если бы итог работы cd был только в изменении $PWD, но это не так)*
2. grep -c <some_string> <some_file>
3. systemd
4. `ls -error 2> /dev/pts/<session>`
5. `grep UseDNS < /etc/ssh/sshd_config > ~/grep_output_file`
6. `echo test > $(tty)`
7. `bash 5>&1`  
(откроется "на запись" командная оболочка bash с присвоенным файл дескриптором 5 с перенаправлением на stdout терминала)  
`echo netology > /proc/$$/fd/5`  
*(вывод команды echo перенаправляется на fd 5, который в свою очередь перенаправляет вывод на stdout терминала)*
8. `bash 5>&1`  
`ls -error 2>&1 1>&5 | grep invalid`
9. `cat /proc/$$/environ`  
`env`  
`ps e -p $$`  
*(Выводятся все переменные окружения и их значения в текущей сессии пользователя)*
10. `proc/[pid]/cmdline`  
Read-only file holds the complete command line for the process,   
unless process is a zombie.  
`proc/[pid]/exe`  
Symbolic link containing the actual path-name of the executed command.  
11. `cat /proc/cpuinfo | grep sse`  
`cat /proc/cpuinfo | grep -oE '\b[s]?sse[^ ]*'`  
sse sse2 ssse3 sse4_1 sse4_2  
12. `ssh -t localhost 'tty'`  
*(По умолчанию при выполнении удаленной команды через SSH не происходит аллокации TTY для удаленной сессии,
т.к. эта сессия может быть использована для передачи файлов или другого содержимого. Аргумент -t используется для принудительного создания TTY)*
13. `top` ctrl+z  
`disown top`  
`screen`  
`reptyr $(pgrep top)` ctrl+a " 0  
14. Команда tee считывает stdin и записывает его одновременно в stdout и в один или несколько подготовленных файлов.  
Конструкция `echo string | sudo tee /root/new_file` работает, т.к. предоставляются привелегии команде tee, которая непосредственно  
(**не** через перенаправление, которым занимается процесс shell'а с правами пользователя) производит запись в файл.

-----------------------------------------------------------------------------------------------
3.1.1  

1. complete
2. complete
3. complete
4. complete
5. memory 1024Mb cpu 2
6. Vagrantfile:  
&nbsp;&nbsp;config.vm.provider "virtualbox" do |v|  
&nbsp;&nbsp;&nbsp;&nbsp;v.memory = 2048  
&nbsp;&nbsp;&nbsp;&nbsp;v.cpus = 4  
&nbsp;&nbsp;end  
7. complete
8. man bash history  
line 1208 HISTSIZE  
ignoreboth is shorthand for ignorespace and ignoredups  
9. {} used in compound commands  
man bash line 332
10. `touch {1..100000}` - success  
`touch {1..300000}` - error "Argument List Too Long"  
cause final command-line arguments is larger than the arguments buffer space  
`getconf ARG_MAX`  
2097152  
11. [[ -d /tmp ]] tests the /tmp directory exist
12. `mkdir -p /tmp/new_path_directory/bash`  
`cp /bin/bash /tmp/new_path_directory/bash`  
`PATH=/tmp/new_path_directory/bash:$PATH`  
13. at executes commands at specified time  
batch executes commands when system load levels permit  
*(at запускает команды в указанное время,
а batch запускает команды в зависимости от загруженности системы (load average),
например: запустить команду, когда уровень средней загрузки системы будет ниже 0.1)*
14. complete

----------------------------------------------------------------------
