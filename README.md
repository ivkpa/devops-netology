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
