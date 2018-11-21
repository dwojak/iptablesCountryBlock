# iptablesCountryBlock

Automatically insert iptables rules, blocking system access by country specific subnets.
Installation:
cd /opt
mkdir iptablesCountryBlock
cd iptablesCountryBlock
mkdir backup
mkdir zones

vi /etc/cron.d/iptablesCountryBlock
#execute every day at 00:30AM
30 00 * * * root /opt/iptablesCountryBlock/iptablesCountryBlock.sh >> /var/log/iptablesCountryBlock.log 2>&1

touch /var/log/iptablesCountryBlock.log

vi /etc/logrotate.d/iptablesCountryBlock
/var/log/iptablesCountryBlock.log {
        missingok
        copytruncate
        daily
        rotate 7
        notifempty
}

vi /etc/rsyslog.d/iptablesCountryBlock.conf
:msg, contains, "country code ip drop" -/var/log/iptablesCountryBlock.log
#& stop
& ~
or
vi /etc/syslog.conf
local4.*                                                /var/log/iptablesCountryBlock.log

