# notify-by-mqtt

a Nagios/Icinga notification module which wraps data into JSON and fires it off to an MQTT broker.

## `icinga.cfg`

```
enable_environment_macros=1
```

### `commands.cfg`

```
define command{
    command_name notify-service-by-mqtt
    command_line /home/jpm/icinga/notify-mqtt.py
    }
```

### `contacts_icinga.cfg`

```
define contact{
        contact_name                    root
        alias                           Root
        service_notification_period     24x7
        host_notification_period        24x7
        service_notification_options    w,u,c,r
        host_notification_options       d,r
#        service_notification_commands   notify-service-by-email
        service_notification_commands   notify-service-by-mqtt
        host_notification_commands      notify-host-by-email
        email                           root@localhost
        }
```


As an example payload:

```json
{
    "_type": "icinga", 
    "date": "2014-04-04", 
    "eventstarttime": "1396621975", 
    "hostdisplayname": "localhost", 
    "hostname": "localhost", 
    "hoststatetype": "HARD", 
    "servicedesc": "JPtest", 
    "servicedisplayname": "JPtest", 
    "serviceoutput": "file /tmp/f1: ENOENT", 
    "servicestate": "CRITICAL", 
    "servicestateid": "2", 
    "shortdatetime": "2014-04-04 16:38:25", 
    "time": "16:38:25", 
    "timet": "1396622305"
}
```
