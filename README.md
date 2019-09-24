# check_mikrotik-by-ssh-ping-remote-ip monitoring plugin
Connects to a Mikrotik router and checks if it can ping a specific IP address

## Usage
    sudo -u nagios /usr/local/bin/mikrotik-by-ssh-ping-remote-ip 192.168.177.106 4.2.2.1 comglobalit-monitoreo

## SSH key generation
    sudo -u nagios ssh-keygen -f /var/lib/nagios/id_rsa

## Install public key in RouterOS
See https://wiki.mikrotik.com/wiki/Use_SSH_to_execute_commands_(DSA_key_login)

## Nagios/Icinga Configuration
Command definition
```
define command {
        command_name    check_mikrotik-by-ssh-ping-remote-ip
        command_line    /usr/local/bin/mikrotik-by-ssh-ping-remote-ip '$HOSTADDRESS$' '$ARG1$' '$ARG2$' '$ARG3$' '$ARG4$' '$ARG5$' '$ARG6$' '$ARG7$' '$ARG8$'
}
```

Host definition
```
define service {
       host_name                customer-host
       service_description      ISP1-: PING via SSH a 4.2.2.1
       check_command            check_mikrotik-by-ssh-ping-remote-ip!4.2.2.1!mikrotik-user!
       use                      generic-service
}
```
