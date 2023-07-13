
# Creating service for jasper server

This manual has the discription about adding jasper service to ubuntu server as service, while server goes down this service will help us to start the jasper server without any manual support.




## Procedure

Create file called jasperserver in init.d

```bash
sudo vi /etc/init.d/jasperserver
```
 Insert this text

 ```bash
 #!/bin/sh
### BEGIN INIT INFO
# Provides: jasperserver
# Required-Start:
# Required-Stop:
# Default-Start: 2 3 4 5
# Default-Stop: 0 1 6
# Short-Description: Start JasperServer at boot time
# Description: Enable service provided by JasperServer.
### END INIT INFO

JASPER_HOME="/opt/jasperreports-server-cp-8.0.0"

case "$1" in
start)
if [ -f $JASPER_HOME/ctlscript.sh ]; then
echo "Starting JasperServer"
$JASPER_HOME/ctlscript.sh start
fi
;;
stop)
if [ -f $JASPER_HOME/ctlscript.sh ]; then
echo "Stopping JasperServer"
$JASPER_HOME/ctlscript.sh stop
fi
;;
restart)
if [ -f $JASPER_HOME/ctlscript.sh ]; then
echo "Restarting JasperServer"
$JASPER_HOME/ctlscript.sh restart
fi
;;
status)
if [ -f $JASPER_HOME/ctlscript.sh ]; then
$JASPER_HOME/ctlscript.sh status
fi
;;
*)
echo $"Usage: $0 {start|stop|restart|status}"
exit 1
;;
esac
```

Set jasperserver in init.d as execute permission

```bash
sudo chmod +x /etc/init.d/jasperserver
```
Update jserperserver as default service in Ubuntu

```bash
sudo update-rc.d jasperserver defaults
```
Navigate to the /etc/rc1.d/ directory using the following command

```bash
cd /etc/rc1.d/
```

```bash
sudo ln -s /etc/init.d/jasperserver K20jasperserver
```

Navigate to the /etc/rc2.d/ directory using the following command

```bash 
cd /etc/rc2.d/
```
```bash
sudo ln -s /etc/init.d/jasperserver K20jasperserver
```

To start manually

```bash
sudo service jasperserver start
```

Try rebooting server to check whether jasperserver restarts of server startup.