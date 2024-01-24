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
