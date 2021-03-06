check_lagg_failover
===================

Nagios plugin for FreeBSD lagg failover interface.

Alert when a lagg failover interface has failed-over to a slave port.

For more information about lagg interfaces in general;  
http://www.freebsd.org/doc/handbook/network-aggregation.html

This check is meant to serve two purposes;

1. To alert that, for some reason, the master port is no longer active.

	This could mean that the nic card is fried,
	the upstream switch is down, etc.

2. To give the system administrator as much time as possible
	in order to bring the master port back online.

	This is especially important when the lagg interface
	is configured with only two ports.

	In such configurations, running with a disabled MASTER port is risky,
	as there is no fail-over capability.


Limitations
-----------

This plugin only works when the lagg interface is configured in "Failover Mode".


Dependencies
------------

`nagios-plugins` must be installed from the ports tree.


Installation
------------

Copy `check_lagg_failover` to `/usr/local/libexec/nagios/check_lagg_failover`

Then set ownership and permissions;
```
chown root:wheel /usr/local/libexec/nagios/check_lagg_failover
chmod 0555       /usr/local/libexec/nagios/check_lagg_failover
```

Examples
-------

```
~$ /usr/local/libexec/nagios/check_lagg_failover lagg0
OK - lagg0 master port is active
~$ echo $?
0
```

```
~$ /usr/local/libexec/nagios/check_lagg_failover igb0
WARN - igb0 is not a link failover interface!
~$ echo $?
1
```

Testing
-------

Tested with a lagg interface consisting of two ports ("laggport"),
although it should work with any number of ports.

Tested on FreeBSD 9.2-RELEASE-p5.

If you can confirm this plugin to work with other versions or configurations,
please contact me so I can update this section. Thank you!
