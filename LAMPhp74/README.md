# LAMPhp74 on Docker

Imagem originalmente criada a partir das referências em
https://hub.docker.com/_/mysql e https://hub.docker.com/_/ubuntu

O ambiente aqui definido irá instanciar dois contâineres, um contendo o apache
com a linguagem PHP 7.4, outro com o banco de dados MySQL. A instância php irá
fazer uso do diretório 'public_html' para ser a base dos arquivos servidos no
ambiente Apache, html serão processados como arquivos convencionais pelo apache,
arquivos php serão interpretados pelo php e servidos pelo apache em seguida.

Para executar a imagem você deve baixar o arquivo "yml" deste diretório
juntamente com o conteúdo do diretório 'docker', em seguida você deve criar a
instância web para depois executar "docker-compose up", o que irá disponibilizar
o ambite para seu uso.

Para criar a imagem necessária para o apache e o php você deve executar a
seguinte sequência de comandos:

    cd docker
    openssl req -new -newkey rsa:4096 -days 3650 -nodes -x509 -subj "/C=../ST=...../L=..../O=..../CN=..." -keyout ./ssl.pem -out ./ssl.pem
    cd ..
    docker build -t rstriquer/LAMPhp74:3.0 ./docker/

A execução da criação da imagem, descrita nos passos acima, irá fazer o download
da imagem original do ubuntu, realizar compilações e configurações locais e por
isto irá demorar alguns minutos.

Ao concluir a criação da imagem do servidor de páginas você poderá executar o
"docker-compose up", que por sua vez irá iniciar o download das imagens
envolvidas e só após iniciará a criação da instância propriamente dita.
Recomendamos que a primeira execução seja feita sem jogar o docker para o
background (opção "-d" do docker-compose), desta forma você poderá acompanhar
em tela o download dos arquivos, assim como o andamento da criação da instância
inicial.

A criação desta instância na primeira execução, após o download da imagem, irá
demorar por volta de 10min (ou mais, dependendo de sua máquina) mas após executar
será apresentado uma saída similar a apresentada abaixo. Apenas após as mensagens
a instância estará pronta para uso.

    2020-07-22 00:46:23 1 [Note] mysqld: ready for connections.
    Version: '5.6.48'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server (GPL)


# Recomendações

Use sem restrições

# Outros

Ainda estou estudando uma forma mais automatizada de configurar um servidor de
SSL no contáiner. Se tiver indicações de tutoriais não deixe de fazer
comentários diretamente no arquivo README.md deste diretório. Ficarei
agradecido.

# MySQL

A execução deste comando cria uma instância sem bancos de dados específicos
(além dos atuais de contróle do próprio MySQL), por este motivo não existe
abaixo definição de banco de dados.

Para connectar a base criada utilize os parâmetros abaixo:

* **HOST**: localhost

* **PORT**: 3306

* **USERNAME** root

* **PASSWORD**: 123qwe

Caso deseje se conectar diretamente pela linha de comandos utilize conforme
abaixo:

docker exec -it LAMPhp73_db bash -c "mysql"



## PHP

Caso deseje fazer alguma alteração no ambiente do PHP faça tais alterações
diretamente no arquivo php.ini disponível no diretório "./docker" e reinicie a
instância, isso irá refletir diretamente no ambiente.

Caso você precie apenas do PHP rodando localmente recomendo executar o comando
abaixo, com ele você poderá trocar de versão e fazer ajustes rápidos sem a
estrutura dos demais componentes deste projeto, como uma outra máquina virtual
de MySQL.

```docker run -it --rm --name my-running-script -p 9000:9000 -v "$PWD":/usr/src/myapp -w /usr/src/myapp php:7.4-cli php -S 0.0.0.0:9000```

## xDebug

Para que o xdebug funcione no Visual Studio Code é necessário selecionar uma
configuração de debug para PHP e adicionar no arquivo launch.json criado para
o debugger as seguintes variáveis:

```json
    "serverSourceRoot": "/var/www/html",
    "localSourceRoot": "${workspaceRoot}/public_html"
```

Para facilitar ainda mais adicionamos no projeto um arquivo launch.json que fica
no diretório ".vscode"