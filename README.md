# speedport

a simple python script to get data from Speedport Cosmote router

## python script

`check_speedport`

## nagios config

copy `check_speedport` file to `/usr/local/nagios/libexec/`

```
###############################################################################
#
# HOST DEFINITIONS
#
###############################################################################

# Define the switch that we'll be monitoring

define host {

    use                     generic-switch                      ; Inherit default values from a template
    host_name               speedport                           ; The name we're giving to this switch
    alias                   SpeedPort Plus                      ; A longer name associated with the switch
    address                 192.168.3.1                         ; IP address of the switch
    hostgroups              switches                            ; Host groups this switch is associated with
}



###############################################################################
#
# HOST GROUP DEFINITIONS
#
###############################################################################

# Create a new hostgroup for switches

define hostgroup {

    hostgroup_name          switches                            ; The name of the hostgroup
    alias                   Network Switches                    ; Long name of the group
}



###############################################################################
#
# COMMAND DEFINITION
#
###############################################################################

define command {
    command_name            check_speedport
    command_line            $USER1$/check_speedport
}



###############################################################################
#
# SERVICE DEFINITIONS
#
###############################################################################

# Create a service to PING to switch

define service {

    use                     generic-service                     ; Inherit values from a template
    host_name               speedport                           ; The name of the host the service is associated with
    service_description     PING                                ; The service description
    check_command           check_ping!200.0,20%!600.0,60%      ; The command used to monitor the service
    check_interval          5                                   ; Check the service every 5 minutes under normal conditions
    retry_interval          1                                   ; Re-check the service every minute until its final/hard state is determined
}

define service {

    use                     generic-service                     ; Inherit values from a template
    host_name               speedport                           ; The name of the host the service is associated with
    service_description     vDSL                                ; The service description
    check_command           check_speedport                     ; The command used to monitor the service
    check_interval          5                                   ; Check the service every 5 minutes under normal conditions
    retry_interval          1                                   ; Re-check the service every minute until its final/hard state is determined
}
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
