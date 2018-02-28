# Configuração do collectd para coletar métricas do MongoDB #

**mongo --username suse --password suse admin**
	
```
use admin

db.createRole({
    role: "serverStatus",
    privileges: [
        { resource: { cluster: true }, actions: [ "serverStatus" ] },
    ],
    roles: []
})

db.createUser( {
  user: "collectd",
  pwd: "collectd",
  roles: [ { role: "readAnyDatabase", db: "admin" }, { role: "clusterMonitor", db: "admin" }, {role: "serverStatus", db: "admin"} ]
});

quit ()
```

**yum install -y epel-release**
**yum install -y python-pip collectd**

**pip install --upgrade pip**
**pip install pymongo**

**curl -o /usr/lib64/python2.7/mongodb.py https://raw.githubusercontent.com/miltongabriel/monitoring-stack/master/collectd/mongodb/mongodb.py**

**vim /etc/collectd.conf**

```
LoadPlugin network
<Plugin "network">
  Server "192.168.100.20" "25826" #Colocar aqui o IP do servidor InfluxDB + porta de monitoração definida para o collectd
</Plugin>

Include "/etc/collectd.d"
```

**vim /etc/collectd.d/mongodb.conf**

```
LoadPlugin python
<Plugin python>
    ModulePath "/usr/lib64/python2.7/"
    LogTraces true
    Import "mongodb"
    <Module mongodb>
          Host     "127.0.0.1"
          Port     "27017"
          User     "collectd"
          Password "collectd"
          Database "admin"
    </Module>
</Plugin>
```
