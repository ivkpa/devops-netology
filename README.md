3.1.1\
\
1. complete\
2. complete\
3. complete\
4. complete\
5. memory 1024Mb cpu 2\
6. Vagrantfile:\
&nbsp;&nbsp;&nbsp;config.vm.provider "virtualbox" do |v|\
&nbsp;&nbsp;&nbsp;&nbsp;v.memory = 2048\
&nbsp;&nbsp;&nbsp;&nbsp;v.cpus = 4\
&nbsp;&nbsp;&nbsp;end\
7. complete\
8. man bash history\
line 1208 HISTSIZE\
ignoreboth is shorthand for ignorespace and ignoredups\
9. {} used in compound commands\
man bash\
line 332\
10. touch {1..100000} - success\
touch {1..300000} - error "Argument List Too Long"\
cause final command-line arguments is larger than the arguments buffer space\
getconf ARG_MAX\
2097152\
11. [[ -d /tmp ]] tests the /tmp directory exist\
12. mkdir -p /tmp/new_path_directory/bash\
cp /bin/bash /tmp/new_path_directory/bash\
PATH=/tmp/new_path_directory/bash:$PATH\
13. The commands of a batch job run sequentially one after another while the commands in at jobs may run in parallel.\
14. complete\
