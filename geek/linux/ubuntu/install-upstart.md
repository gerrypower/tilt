## Install Upstart for Startup Tasks
[Upstart](http://upstart.ubuntu.com) is an amazing init daemon replacement,
that makes writing powerful startup scripts easy. I installed in on Raspbian
to handle startup scripts for my weather radio project and my picture frame.
For some ideas on how it might be useful and some recipes, check out the
[Upstart Cook Book](http://upstart.ubuntu.com/cookbook/).

### Installation
````
sudo apt-get install upstart --force-yes
````

### Sample Startup Scripts
#### nginx
```shell
description "nginx http daemon"

start on (local-filesystems and net-device-up IFACE!=lo)
stop on shutdown

env NAME=nginx
env DAEMON=/usr/sbin/nginx
env PID=/var/run/nginx.pid

expect fork
respawn
respawn limit 5 10

pre-start script

  # stop job from continuing if no config file found for daemon
  if [ ! -f /etc/default/$NAME ]
  then
    stop; exit 0;
  fi

  # source the config file
  . /etc/default/$NAME

  # stop job from continuing if admin has not enabled service in
  # config file.
  if [ -z "$ENABLE" ]
  then
    stop; exit 0;
  fi

  $DAEMON -t
  if [ $? -ne 0 ]
  then
    stop; exit 0;
  fi

end script

exec $DAEMON
```

#### Wifi Monitor for the RaspberryPi with Flakey Wifi
```shell
description "A script to ensure wlan0 stays connected"

# Note: Since this starts when the wlan interface comes up,
# this will have to be manually stopped if you really want
# to bring wlan0 down. 'sudo stop network-monitor'

start on (local-filesystems and net-device-up IFACE=wlan0)
stop on shutdown

respawn
respawn limit 5 10

pre-start script
  sleep 30
  if ! ifconfig wlan0 | grep -q "inet addr:" || ! ping -c 1 8.8.8.8 > /dev/null ; then
    echo "Network connection down! Attempting reconnection."
    ifup --force wlan0
  fi
end script

script

  sleep 30
  while true; do
    if ! ifconfig wlan0 | grep -q "inet addr:" || ! ping -c 1 8.8.8.8 > /dev/null; then
      exit 1
    fi
    sleep 60
  done

end script

```
