# Configuração do collectd para coletar métricas do Mysql #

**mysql -uroot -pSuse#211095**

```
CREATE USER 'collectd'@'localhost' IDENTIFIED BY 'collectd';
GRANT USAGE ON *.* TO 'collectd'@'localhost';
GRANT PROCESS ON *.* TO 'collectd'@'localhost';
GRANT REPLICATION CLIENT ON *.* TO 'collectd'@'localhost';
```

**yum install collectd MySQL-python -y**

**curl -o /usr/lib64/python2.7/mysql.py https://raw.githubusercontent.com/miltongabriel/monitoring-stack/master/collectd/mysql/mysql.py**

**vim /etc/collectd.d/mysql.conf**

```
<LoadPlugin python>
        Globals true
</LoadPlugin>

<Plugin python>
        ModulePath "/usr/lib64/python2.7/"
        Import mysql
        <Module mysql>
                Host "localhost"
                Port 3306
                User "collectd"
                Password "collectd"
                Verbose false
        </Module>
</Plugin>
```
