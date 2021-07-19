# PiCap service

# How to Run a Script as a Service in Raspberry Pi

## Service for the Script

Now we're going to define the service to run this script:

```Shell
cd /lib/systemd/system/
sudo nano picap.service
```

The service definition must be on the /lib/systemd/system folder. Our service is going to be called "picap.service":

```text
[Unit]
Description=Picap Service
After=multi-user.target

[Service]
Type=simple
ExecStart=/usr/bin/python /home/pi/PiCapExamples/Python/picap-datastream-osc-py/datastream-osc.py -h 192.168.0.52
Restart=on-abort

[Install]
WantedBy=multi-user.target
```

Now that we have our service we need to activate it:

```Shell
sudo chmod 644 /lib/systemd/system/picap.service
chmod +x /home/pi/PiCapExamples/Python/picap-datastream-osc-py/datastream-osc.py
sudo systemctl daemon-reload
sudo systemctl enable picap.service
sudo systemctl start picap.service
```

## Service Tasks
For every change that we do on the /lib/systemd/system folder we need to execute a daemon-reload (third line of previous code). If you want to check the status of the service, you can execute:

`sudo systemctl status picap.service`

In general:

### Check status
`sudo systemctl status picap.service`

### Start service
`sudo systemctl start picap.service`

### Stop service
`sudo systemctl stop picap.service`

### Check service's log
`sudo journalctl -f -u picap.service`

## REFERENCES
- https://wiki.archlinux.org/index.php/systemd
- https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files
- https://coreos.com/os/docs/latest/getting-started-with-systemd.html
