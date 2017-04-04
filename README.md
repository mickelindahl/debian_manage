# Debian manage

## Server email support
Configure mailgun with postfix such that server can send emails.

Run `sudo apt-get update && sudo apt-get install postfix libsasl2-modules`

Run `sudo nano /etc/postfix/main.cf` and add

```
relayhost = smpt.mailgun.org:587
smtp_sasl_auth_enable = yes
smtp_sasl_security_options = noanonymous
smtp_sasl_password_maps=static:postmaster@yourdomain.se:{password}
```

Reload postfix `sudo service postfix restart`

Open terminal and run `tail -f /var/log/syslog` to check if it went well 

Then open another terminal and send email with `mail -s "Test mail" mikael.lindahl@greencargo.com <<< "A test message using Mailgun"`
and chack if it went well in the output in the first termial

## Enable email notiofication for new packages


Install [apticron](https://debian-administration.org/article/491/Automatic_package_update_nagging_with_apticron) 
```
apt-get install apticron
```

Edit `apticron.conf` 
```
nano /etc/apticron/apticron.conf
```
Set appropirate variables. Atleast `EMAIL` but can also be nice to set `SYSTEM` 
