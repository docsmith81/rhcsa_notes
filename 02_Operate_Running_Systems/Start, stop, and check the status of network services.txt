Start, stop, and check the status of network services

Start service:
# service httpd start

Restart process:
# service httpd restart

Reload process configuration:
# service httpd reload

Stop service:
# service httpd stop

Check status of service:
# service httpd status

Configure service to start on boot:
# chkconfig httpd on

Specify levels at which the service will start up in at boot:
# chkconfig --levels 345 httpd on

Stop service from starting on boot:

# chkconfig httpd off