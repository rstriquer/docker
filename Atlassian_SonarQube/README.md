# SonarQube on Docker

Para executar basta salvar o arquivo docker-compose.yml em seu computador e executar "docker-compose up -d". Após isto siga para o endereço localhost:9000 para completar a configuração da máquina virtual.

# Para execução
Para connectar acesse a URL http://localhost:9000/ e utilize os parâmetros abaixo:

* **USERNAME** admin

* **PASSWORD**: admin

Após conectar configurar um projeto e anotar o project key que é o project token. Depois de configurar o projeto será apresentado um botão "Run analysis on your project"  e ao final da seleção será apresentado uma linha de comando que deverá ser utilizado para executar em uma linha de comando (shell/terminal) e com isso o sistema irá fazer a avaliação de seu código e disponibilizar o relatório na interface web.

O comando da linha de comando é similar ao abaixo:

```shell
sonar-scanner \
  -Dsonar.projectKey=myproj \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=753fb0b2d2b2d0c2f826084df458d426d7b3bcc0
```

# Recomendações

Use sem restrições. Ao que percebi, se você tentar utilizar algum parâmetro ou funcionalidade não autorizada na versão community ele irá lhe comunicar das vantagens de adquirir um pacote pago e não proceder com o solicitado.

Na eventualidade de você estar apenas fazendo um estudo inicial do aplicativo recomendo retirar as linhas relacionadas a volumes do docker-composer.yml

# Outros

Considere utilizar extensões disponíveis da comunidade para extender as funcionalidades do aplicativo.

## License

https://www.sonarqube.org/ is a free & open source product in its Community Edition (same configured in this docker-composer.yml)

## Copyright

© 2008-2021, SonarSource S.A, Switzerland. All content is copyright protected. SONARQUBE and SONARSOURCE are trademarks of SonarSource SA.

All other trademarks and copyrights are the property of their respective owners. All rights are expressly reserved.

Privacy Policy | Distributed under LGPL v3