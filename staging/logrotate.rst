logrotate

rotate daily keeping all logs and appending date to archives​:
/var/log/tools/*.log {
       daily
       rotate 730
       compress
       delaycompress
       copytruncate
       notifempty
       missingok
       dateext
       dateformat "_%Y-%m-%d"
}
obviously replacing the indicated path with wherever the actual logfiles are located. logrotate can be installed on osx via `brew install logrotate`.
