# ZBX-Automations - Extractor
 Scripts de automação - Zabbix - Extractor

O extractor foi criado para extrair grandes volumes de dados da base de dados, algo que não é possivel dentro do front-end do Zabbix.

O script pode ser executado tanto com itens unicos quanto com multiplas chaves.

Ps: Esse script foi adaptado e alterado por duas pessoas diferentes anteriores a mim, eu efetuei algumas pequenas alterações e corrigi alguns bugs.

Initial Source From : http://doc.bonfire-project.eu/R2/monitoring/bonfire_monitoring_data_to_csv.html

Minors changes From : https://github.com/ahmedzbyr/zabbix-automations

## Requisitos
Para rodar esse script, você precisa ter o python-argparse instalado.
Debian:

    apt-get install python-argparse

RHEL (CentOS, outros)

    yum install python-argparse

Em seguida, ajustar as permissões dos scripts:

    chmod +x extractor.py
    chmod +x zabbix_api.py

## Itens unicos
Essa opção vai se conectar ao Zabbix e coletar os dados da chave especificada. logo em seguida um .CSV é criado no formato nome_da_chave.csv

    sudo ./extractor.py -s 127.0.0.1 -n host-in-zabbix -u admin -p zabbix -k key-in-zabbix -t1 "2021-01-01 12:00:00" -v 1

## Itens Múltiplos
Essa opção assim como a outra, conecta ao Zabbix e coleta os dados das chaves mencionadas.
Cada chave tera seu próprio arquivo .CSV, obedecendo o formato passado anteriormente, nome_da_chave.csv

    sudo ./extractor.py -s 127.0.0.1 -n host-in-zabbix -u admin -p zabbix -f sample_key_file.txt -t1 "2021-01-01 12:00:00" -v 1 
    sudo ./extractor.py -s 127.0.0.1 -n host-in-zabbix -u admin -p zabbix -f sample_zabbix_export_file.xml -t1 "2021-01-01 12:00:00" -v 1

O arquivo vai ser impresso da seguinte maneira

    key|timestamp|value
    TestKeyFromZabbix_VS.dlBytes|2021-01-01 12:00:00|0
    TestKeyFromZabbix_VS.dlBytes|2021-01-01 12:05:00|0
    TestKeyFromZabbix_VS.dlBytes|2021-01-01 12:10:00|0
    TestKeyFromZabbix_VS.dlBytes|2021-01-01 12:15:00|3517

Post sobre o script com mais detalhes quanto ao funcionamento:
[Extração de dados em massa](https://mromeiro-f.medium.com/extração-de-dados-em-massa-6243786435f8)

## Uso
    usage: extractor.py [-h] -s SERVER_IP -n HOSTNAME
                                           (-k KEY | -f FILE) -u USERNAME -p
                                           PASSWORD [-o OUTPUT] -t1 DATETIME_START
                                           [-t2 DATETIME_END] [-v DEBUG_LEVEL]
    
    Fetch history from aggregator and save it into CSV file
    
    optional arguments:
      -h, --help            show this help message and exit
      -s SERVER_IP, --server-ip SERVER_IP
                            Server IP address
      -n HOSTNAME, --hostname HOSTNAME
                            Hostname of the VM
      -k KEY, --key KEY     Zabbix Item key
      -f FILE, --file FILE  Zabbix Item key File. XML export file from Zabbix.
                            Text file with key in each line.Each Key will create
                            its own csv file.
      -u USERNAME, --username USERNAME
                            Zabbix username
      -p PASSWORD, --password PASSWORD
                            Zabbix password
      -o OUTPUT, --output OUTPUT
                            Output file name, default key_hostname.csv (will
                            remove all special chars).This Option currently works
                            with -k/--key option.
      -t1 DATETIME_START, --datetime-start DATETIME_START
                            Start datetime, 'yyyy-mm-dd HH:MM:SS' use this pattern
                            '2014-10-15 19:12:00" if only t1 specified then time
                            period will be t1 to now()
      -t2 DATETIME_END, --datetime-end DATETIME_END
                            end datetime, "yyyy-mm-dd HH:MM:SS" use this pattern
                            '2014-10-15 19:12:00'
      -v DEBUG_LEVEL, --debug-level DEBUG_LEVEL
                            log level, default 0

<!-- CONTACT -->
## Contato

- Linkedin: [Michael Fortes](https://www.linkedin.com/in/mikefortes/)
- Twitter: [@mikes_script
](https://twitter.com/mikes_script)
- Email: mromeiro.f@gmail.com

Project Link: [https://github.com/Punkays/ZBX-Automations](https://github.com/MikeFortes/ZBX-Automations)
