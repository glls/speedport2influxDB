# speedport

A python script to get connection data from Speedport Cosmote router and store it in InfluxDB

## python script :

`check_speedport`

## nagios configuration :

copy `check_speedport` file to `/usr/local/nagios/libexec/`

copy `speedport.cfg` to your objects dir e.g. `/usr/local/nagios/etc/objects`

## run it every 15 min with crontab :
```
*/15 * * * * /path/to/speedport/check_speedport -w
```

## sample output :

```
device_name : Speedport Plus
rebooting : 0
router_state : OK
provis_inet : xx0
provis_voip : xx0
save_fails : 0
title : Speedport Plus Configuration Program
loginstate : 0
status : ok
datetime : 2020-11-07 09:50:56
uptime : 39 days, 5 hours, 46 minutes, 49 seconds
firmware_version : XXXXXXXXXXX.00.XXX_OTEX
serial_number : SCCCCCCCCCCCCCC
dsl_link_status : online
dsl_sync_time : 2020-09-29 05:08:11
dsl_online_time : 2020-10-07 02:43:04
dsl_status : online
dsl_downstream : 74498
dsl_upstream : 10998
dsl_max_downstream : 86356
dsl_max_upstream : 23707
dsl_transmission_mode : VDSL2-17A  Annex B
dsl_crc_errors : 13379
dsl_fec_errors : 33242882
dsl_snr : 9.6 / 20.0
dsl_atnu : 8.0 / 17.5
vdsl_atnu : 17.5
vdsl_atnd : 8.0
wlan_ssid : XXX
wlan_5ghz_ssid : XXX5
use_wlan : 1
use_wlan_5ghz : 0
use_wps : 1
```
