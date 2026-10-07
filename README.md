# systemd
How to setup jar as a service in systemd

## Steps
### Step 1
~~~
sudo vi /etc/systemd/system/myapp.service
~~~
### Step 2
Contents of myapp.service

~~~
[Unit]
Description=Java Web Application
After=syslog.target network.target

[Service]
User=sujeet
WorkingDirectory=/home/sujeet/apps
ExecStart=/usr/bin/java -jar /home/sujeet/apps/myapp.jar --server.port=8080
SuccessExitStatus=143
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
~~~

### Step 3
Start enable the service
~~~
sudo systemctl daemon-reload
sudo systemctl start myapp
sudo systemctl enable myapp
sudo journalctl -u myapp -e
~~~

# Follow logs live
sudo journalctl -u your-service.service -f

# Last 100 lines
sudo journalctl -u your-service.service -n 100 --no-pager

# Logs from the current boot
sudo journalctl -u your-service.service -b

# Logs from the last hour
sudo journalctl -u your-service.service --since "1 hour ago"

