# Configuração do collectd para coletar métricas do MongoDB #

1. Teste

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

		pip install pymongo
