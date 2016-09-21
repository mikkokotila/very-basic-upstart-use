# Very basic Ubuntu Upstart use (great for total beginners)

TL;DR

It's much easier to do very powerful things with upstart than you think. 

### How to get start with your first Upstart job

IMPORTANT: 

- use full/absolute paths everywhere (also inside the script you run from upstart) 
- there are two different levels; system level and user level 


##### adding a system level upstart job 

    vim /etc/init/servicename.conf 

To run run hello.sh located in the home folder of root, include: 

    exec /root/hello.sh

With this one line added, hello.sh becomes a service. Because we had named it 'servicename' (in the filename), we can now do things like: 

   sudo service servicename status
   sudo service servicename start
   sudo service servicename restart
   sudo service servicename stop

To make this more useful, in the /etc/init/servicename.conf file, let's add:

   start on filesystem or runlevel [2345]
   stop on shutdown

There is a way to include scripts (as opposed to single command) by using stanzas, but the single line command will allow you to do a lot because you can always run a script with the command. 

##### checking the syntax of the conf file

init-checkconf /etc/init/servicename.conf

##### check if the process is running

ps ax | grep scriptname | grep -v grep

##### killing the processes related with the service

kill `ps ax | grep scriptname | grep -v grep | cut -d ' ' -f2 | tr '\n' ' '`
