# LAMPhp82 on Docker

Este arquivo está disponível também em sua versão em [Português Brasileiro](./README-pr_br.md)

O ambiente aqui definido irá instanciar três contâineres, um contendo o apache
com a linguagem PHP 8.2 trabalhando em FastCGI, outro com o banco de dados
MySQL Server 8 e um último com o mailhog. A instância php irá
fazer uso do diretório corrente para ser a base dos arquivos servidos no
ambiente Apache, html serão processados como arquivos convencionais pelo apache,
arquivos php serão interpretados pelo php e servidos pelo apache em seguida. O PHP está
configurado para uso com o xDebug3 que será disponibilizado no porte 9003.

O Servidor MySQL está configurado de forma restritiva, como boa parte de alguns servidores
compartilhados na internet, foi inspirado na configuração da Digital Ocean. O script
irá criar um banco de dados com o nome configurado no parâmetro DB_DATABASE, um usuário
para operação deste banco de dados, segundo a variável DB_USER que fará uso da senha
definida na variável DB_PASSWORD e autoridade de acesso a partir de qualquer host.

O mailhog não possui alterações de suas configurações padrões, ele é um wrapper de email
muito útil para ambientes de desenvolvimento.

As configurações do arquivo docker-composer.yml podem ser alteradas a partir de um arquivo
.env disponibilizado na mesma pasta do docker-compose.yml.

Para executar a imagem você deve baixar o arquivo "yml" deste diretório, criar um diretório
com o nome "storage/docker" e dentro dele criar a pasta mysql. Todas estas pastas devem ter
autorização para leitura e escrita pelo usuário que irá executar o comando do docker.
em seguida você deve criar a instância web para depois executar "docker-compose up", o
que irá disponibilizar o ambite para seu uso.

Ao concluir a criação destes arquivos e diretórios locais você poderá executar o
"docker-compose up", que por sua vez irá iniciar o download das imagens
envolvidas e só após iniciará a criação da instância propriamente dita.
Recomendamos que a primeira execução seja feita sem jogar o docker para o
background (opção "-d" do docker-compose), desta forma você poderá acompanhar
em tela o download dos arquivos, assim como o andamento da criação da instância
inicial.

PS: A criação desta instância na primeira execução, após o download da imagem, irá
demorar por volta de 10min (ou mais, dependendo de sua máquina) mas após executar
será apresentado uma saída similar a apresentada abaixo. Apenas após as mensagens
a instância estará pronta para uso.

    2020-07-22 00:46:23 1 [Note] mysqld: ready for connections.
    Version: '5.6.48'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server (GPL)

# Recomendações

Use sem restrições

# MySQL

A execução deste comando cria uma instância com um banco de dados MySQL específico.

Para connectar a base criada utilize os parâmetros abaixo:

* **HOST**: localhost
* **PORT**: 3306
* **DATABASE**: database_local
* **USERNAME** someuser
* **PASSWORD**: 123456

Caso deseje se conectar diretamente pela linha de comandos utilize conforme
abaixo:

```bash
docker exec -it LAMPhp82_db bash -c "mysql"
```

## PHP

### xDebug

Para que o xdebug funcione no Visual Studio Code é necessário selecionar uma
configuração de debug para PHP e adicionar no arquivo launch.json criado para
o debugger as seguintes variáveis:

```json
    "pathMappings": {
        "/app": "${workspaceFolder}"
    },
```

Para facilitar ainda mais adicionamos no projeto um arquivo launch.json que fica
no diretório ".vscode"
