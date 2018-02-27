Grafana - Instalação e configuração inicial
===========================================

1. Adicionar o repositório do Grafana

        echo '[grafana]
        name=grafana
        baseurl=https://packagecloud.io/grafana/stable/el/6/$basearch
        repo_gpgcheck=1
        enabled=1
        gpgcheck=1
        gpgkey=https://packagecloud.io/gpg.Listkey https://grafanarel.s3.amazonaws.com/RPM-GPG-KEY-grafana
        sslverify=1
        sslcacert=/etc/pki/tls/certs/ca-bundle.crt' > /etc/yum.repos.d/grafana.repo

2. Instalar via yum

        yum install grafana -y
        
3. Iniciar e habilitar o inicio automatico

        systemctl enable grafana-server
        systemctl start grafana-server
        
##### Opcional - Alterar porta do grafana para 80

1. No arquivo /etc/grafana/grafana.ini adicionar/alterar a configuração http_port=80 no bloco **[server]**

2. Executar o comando

        setcap 'cap_net_bind_service=+ep' /usr/sbin/grafana-server

