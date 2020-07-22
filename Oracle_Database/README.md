# Oracle Database on Docker

Imagem originalmente criada a partir das referências em https://hub.docker.com/_/oracle-database-enterprise-edition

Para executar a imagem você deve acessar o docker hub na conta da Oracle, na URL https://hub.docker.com/_/oracle-database-enterprise-edition e aceitar os termos de uso para só após seu usuário ter autorização de uso da imagem.

Após ter assinado os termos de uso basta baixar o arquivo "yml" deste diretório e executar "docker-compose up", o sistema irá identificar a versão do Oracle apontada no arquivo e começar a criação da instância.

Antes da criação da instância o docker irá iniciar o download das imagens envolvidas e só após iniciará a criação da instância propriamente dita. Recomendamos que a primeira execução seja feita sem jogar o docker para o background (opção "-d" do docker-compose), desta forma você poderá acompanhar em tela o download dos arquivos, assim como o andamento da criação da instância inicial.

A criação desta instância na primeira execução, após o download da imagem, irá demorar por volta de 10min (ou mais, dependendo de sua máquina) mas após executar será apresentado uma saída similar a apresentada abaixo. Apenas após as mensagens a instância estará pronta para uso.

    Done ! The database is ready for use .
    # ===========================================================================
    # == Add below entries to your tnsnames.ora to access this database server ==
    # ====================== from external host =================================
    ORCLCDB=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<ip-address>)(PORT=<port>))
        (CONNECT_DATA=(SERVER=DEDICATED)(SERVICE_NAME=ORCLCDB.localdomain)))
    ORCLPDB1=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<ip-address>)(PORT=<port>))
        (CONNECT_DATA=(SERVER=DEDICATED)(SERVICE_NAME=ORCLPDB1.localdomain)))

# Usuário e senha para acesso
Para connectar a base criada utilize os parâmetros abaixo:

* **HOST**: localhost

* **PORT**: 1521

* **Database**: ORCLPDB1.localdomain

* **PDB**: ORCLPDB1

* **USERNAME** sys

* **ROLE**: SYSDBA

* **PASSWORD**: Oradoc_db1

Abaixo exemplo de configuração no aplicativo DBeaver para acesso ao banco de dados.

![Tela de configurações para conectar no banco de dados utilizando o DBeaver](./ilustracao01.png)

Caso deseje se conectar diretamente pela linha de comandos utilize conforme abaixo:

docker exec -it oracle_db bash -c "source /home/oracle/.bashrc; /u01/app/oracle/product/12.2.0/dbhome_1/bin/sqlplus /nolog"

# Recomendações

Originalmente o arquivo está configurado para executar a versão 12c Release 2 (12.2.0.1) Enterprise Edition, segundo alguns estudos que fiz na internet seria possível alterar a TAG da versão e com isso instanciar outra versão do banco, conforme suas necessidades, para isto bastaria trocar a TAG docker configurada no parâmetro "image" do arquivo docker-compose.yml deste diretório, porem no forum do site hub.docker encontrei pessoas apontando falhas para instanciar a versão 12.1.0.2, eu também observei essas falhas quando tentei utilizar esta versão e na página oficial da imagem no docker hub fazem referência apenas a versão 12.2.0.1, por isso é possível que no futuro eles utilizem a TAG da imagem docker para disponibilizar outras versões do aplicaitvo, mas no momentorecomendo utilizar o Relase 2 da 12c apenas.

Caso deseje estudar mais sobre o banco de dados recomendo o uso das imagens da própria Oracle disponível na URL https://github.com/oracle/docker-images/blob/master/OracleDatabase/SingleInstance/README.md


# Outros

Para mais informações sobre o banco de dados Oracle acesse a [documentação online do fabricante](https://docs.oracle.com/en/database/oracle/oracle-database/index.html).

## License
To download and run Oracle Database, regardless whether inside or outside a Docker container, you must download the binaries from the Oracle website and accept the license indicated at that page.

All scripts and files hosted in this project and GitHub [docker-images/OracleDatabase](./) repository required to build the Docker images are, unless otherwise noted, released under [UPL 1.0](https://oss.oracle.com/licenses/upl/) license.

## Copyright
Copyright (c) 2014-2019 Oracle and/or its affiliates. All rights reserved.