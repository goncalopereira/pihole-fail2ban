Ideas for unsucking PiHole in the Cloud

# Securing the Pi-hole with fail2ban to prevent DNS Amplification attacks

## Create jail file

    nano /etc/fail2ban/jail.d/pihole-any.conf

Copy & paste the following content into the newly created file

    [pihole-any]
    enabled = true
    port     = 53
    action   = %(banaction)s[name=%(__name__)s-tcp, port="%(port)s", protocol="tcp", chain="%(chain)s", actname=%(banaction)s-tcp]
               %(banaction)s[name=%(__name__)s-udp, port="%(port)s", protocol="udp", chain="%(chain)s", actname=%(banaction)s-udp]
    logpath = /var/log/pihole.log
    findtime = 60
    maxretry = 5
    bantime = 3600
    
## Install filter file

    cd /etc/fail2ban/filter.d
    sudo wget https://raw.githubusercontent.com/goncalopereira/pihole-fail2ban/master/filter.d/pihole-any.conf -O pihole-any.conf
    
