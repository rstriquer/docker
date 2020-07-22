# PostgreSQL Database on Docker

Imagem originalmente criada a partir das referências em https://hub.docker.com/_/postgres

Para executar a imagem você deve baixar o arquivo "yml" deste diretório e executar "docker-compose up", o sistema irá começar a criação da instância. 

Antes da criação da instância o docker irá iniciar o download das imagens envolvidas e só após iniciará a criação da instância propriamente dita. Recomendamos que a primeira execução seja feita sem jogar o docker para o background (opção "-d" do docker-compose), desta forma você poderá acompanhar em tela o download dos arquivos, assim como o andamento da criação da instância inicial.

A criação desta instância na primeira execução, após o download da imagem, irá demorar por volta de 10min (ou mais, dependendo de sua máquina) mas após executar será apresentado uma saída similar a apresentada abaixo. Apenas após as mensagens a instância estará pronta para uso.

    PostgreSQL init process complete; ready for start up.

# Usuário e senha para acesso
Para connectar a base criada utilize os parâmetros abaixo:

* **HOST**: localhost

* **PORT**: 5432

* **Database**: dev

* **USERNAME** postgres

* **PASSWORD**: 123qwe

* **SCHEMA**: public

Caso deseje se conectar diretamente pela linha de comandos utilize conforme abaixo:

docker exec -it oracle_db bash -c "psql -U postgres"

# Recomendações

Use sem restrições

