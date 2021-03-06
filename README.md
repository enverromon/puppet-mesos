# Puppet module: mesos

This is a Puppet module for mesos based on the second generation layout ("NextGen") of Example42 Puppet Modules.

Made by Enver Romon / Kimia Solutions S.L.

Official site: http://www.kimia.mobi

Official git repository: http://github.com/enverromon/puppet-mesos

Released under the terms of Apache 2 License.

This module requires functions provided by the Example42 Puppi module (you need it even if you don't use and install Puppi)

For detailed info about the logic and usage patterns of Example42 modules check the DOCS directory on Example42 main modules set.


## USAGE - Basic management

* Install mesos with default settings

        class { 'mesos': }

* Install a specific version of mesos package

        class { 'mesos':
          version => '1.0.1',
        }

* Disable mesos service.

        class { 'mesos':
          disable => true
        }

* Remove mesos package

        class { 'mesos':
          absent => true
        }

* Enable auditing without without making changes on existing mesos configuration *files*

        class { 'mesos':
          audit_only => true
        }

* Module dry-run: Do not make any change on *all* the resources provided by the module

        class { 'mesos':
          noops => true
        }


## USAGE - Overrides and Customizations
* Use custom sources for main config file

        class { 'mesos':
          source => [ "puppet:///modules/example42/mesos/mesos.conf-${hostname}" , "puppet:///modules/example42/mesos/mesos.conf" ],
        }


* Use custom source directory for the whole configuration dir

        class { 'mesos':
          source_dir       => 'puppet:///modules/example42/mesos/conf/',
          source_dir_purge => false, # Set to true to purge any existing file not present in $source_dir
        }

* Use custom template for main config file. Note that template and source arguments are alternative.

        class { 'mesos':
          template => 'example42/mesos/mesos.conf.erb',
        }

* Automatically include a custom subclass

        class { 'mesos':
          my_class => 'example42::my_mesos',
        }


## USAGE - Example42 extensions management
* Activate puppi (recommended, but disabled by default)

        class { 'mesos':
          puppi    => true,
        }

* Activate puppi and use a custom puppi_helper template (to be provided separately with a puppi::helper define ) to customize the output of puppi commands

        class { 'mesos':
          puppi        => true,
          puppi_helper => 'myhelper',
        }

* Activate automatic monitoring (recommended, but disabled by default). This option requires the usage of Example42 monitor and relevant monitor tools modules

        class { 'mesos':
          monitor      => true,
          monitor_tool => [ 'nagios' , 'monit' , 'munin' ],
        }

* Activate automatic firewalling. This option requires the usage of Example42 firewall and relevant firewall tools modules

        class { 'mesos':
          firewall      => true,
          firewall_tool => 'iptables',
          firewall_src  => '10.42.0.0/24',
          firewall_dst  => $ipaddress_eth0,
        }


## CONTINUOUS TESTING

Travis {<img src="https://travis-ci.org/example42/puppet-mesos.png?branch=master" alt="Build Status" />}[https://travis-ci.org/example42/puppet-mesos]
