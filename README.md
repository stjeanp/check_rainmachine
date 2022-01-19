# check_rainmachine
## Nagios plugin to monitor RainMachine irrigation controller

check_rainmachine is a small python script that is used to monitor RainMachine irrigation controller status. It makes sure that it can authenticate against the specified irrigation controller and then checks to see if any updates are available for it. If either action fails, it will cause a critical alert to be thrown.

It should be run on the Nagios server itself, which needs to have connectivity to the irrigation controller open on TCP port 8080.

## Usage

```
Usage: check_rainmachine [options]

This Nagios plugin checks the health of a RainMachine irrigation controller.

Options:
  -h, --help                 show this help message and exit
  -H HOST, --host=HOST       The hostname/IP of the RainMachine
  -p PASSWD, --pass=PASSWD   The password to use
  --ssl_check                Verify SSL/TLS certificates
```

## Installation

1. Copy the file to your Nagios plugins directory
2. Set the ownership and permissions appropriately
4. Test execution on your Nagios server
5. Update the Pi-hole host definition to check it.

### Example Nagios command definition

Note: since the password is needed, it can be stored in resource.cfg to keep it more secure. In this example, it's in the $USER5$ variable.

```
# 'check_rainmachine' command definition
define command{
  command_name    check_rainmachine
  command_line    $USER1$/check_rainmachine -H $HOSTADDRESS$ -p $USER5$
}
```

### Example Nagios service definition

```
define service{
  use                           local-service
  host_name                     rainmachine
  service_description           Basic RainMachine checks
  check_command                 check_rainmachine
}
```
