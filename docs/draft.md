# WIP Config puppet

```
[root@alma-srv manifests]# rpm -qa | grep puppet
puppetserver-7.14.0-1.el8.noarch
puppet7-release-7.0.0-15.el8.noarch
puppet-agent-7.27.0-1.el8.x86_64
```

## site.pp

```site.pp
# Site configuration
node default {
  # Install the Puppet agent
  package { 'puppet':
    ensure => installed,
  }

  # Start the Puppet agent
  service { 'puppet':
    ensure => running,
    enable => true,
  }
}

node 'alma-client.adsillh.local' {
  include module_test
  include dhcp
  dhcp::pool{ 'ops.dc1.example.net':
  network => '10.0.2.0',
  mask    => '255.255.255.0',
  range   => ['10.0.2.10 10.0.2.100', '10.0.2.200 10.0.2.250' ],
  gateway => '10.0.1.1',
}
}

node 'alma-srv.adsillh.local' {
  package { 'puppet-lint':
  ensure   => '1.1.0',
  provider => 'gem',
  }
}
```

```
[root@puppet production]# tree
.
├── data
├── environment.conf
├── hiera.yaml
├── manifests
│   └── site.pp
└── modules
    ├── dhcpd_adsillh
    │   ├── files
    │   │   └── dhcpd.conf
    │   └── manifests
    │       └── init.pp
    └── module_test
        ├── files
        │   └── conf_de_test.conf
        └── manifests
            └── init.pp

[root@puppet production]# cat modules/dhcpd_adsillh/manifests/init.pp 
class dhcpd_adsillh {
  package { 'dhcp-server':
    ensure => installed,
  }
  service { 'dhcpd':
    ensure => running,
    enable => true
  }
  file {'/etc/dhcp/dhcpd.conf':
    ensure => present,
    source => 'puppet:///modules/dhcpd_adsillh/dhcpd.conf',
  }
}

[root@puppet production]# cat manifests/site.pp 
# Install Puppet Agent everywhere

node default {
  # Install the Puppet agent
  package { 'puppet':
    ensure => installed,
  }

  # Start the Puppet agent
  service { 'puppet':
    ensure => running,
    enable => true,
  }
}

# Apply some things somewhere

node serveur01.adsillh.local {
  include module_test
  include dhcpd_adsillh
  package { 'net-tools':
    ensure => present,
  }
  exec { 'touch':
    command => [ '/usr/bin/touch', '/tmp/test_exec']
  }
}

node puppet.admin.adsillh.local {
  package { 'puppet-lint':
  ensure   => '1.1.0',
  provider => 'gem',
  }
}
```
