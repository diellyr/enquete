# Documentação Enquete 1.0

obs : é necessário ter o docker instalado em seu Linux (apenas linux)

# Instalação do Docker

- Usuários que tem o seu sistema baseado em Debian podem usar o apt-get ou o aptitude:

sudo apt-get update

sudo apt-get install docker.io

- Usuários que tem o seu sistema baseado em RedHat podem usar o yum:

yum install docker

# Baixar os conteiners e a aplicação

### 0 - baixando os dados da aplicação 

descompacte o arquivo enquete.tar.gz dentro de /root

### 1 - baixe os dockers abaixo

docker pull diellyr/enquete.mariadb
docker pull diellyr/enquete.nodejs
docker pull diellyr/enquete.http


### 2 - iniciando os dockers

### - o Primeiro start pode ser feito conforme abaixo

- start mariadb

docker run -it --name mariadb -v /root/Enquete/mariadb:/var/lib/mysql -p 3360:3360 -d diellyr/enquete.mariadb

- start nodejs

docker run -it --name node -v /root/Enquete/nodejs:/root -p 3000:3000 -d diellyr/enquete.nodejs

- start apache

docker run -it --name httpd -v /root/Enquete/apache:/app -p 800:80 -d diellyr/enquete.http

obs1: depois pode usar apenas os comandos mais abaixo "parando e subindo os conteiner" para start dos conteineres, "caso precise matar o conteiners e iniciar tudo novamente use os comandos acima ;) "


Pronto! 

agora é só acessar o endereço abaixo:

### Acesso a Enquete
http://localhost:800




..........................................................................

### parando e subindo os conteineres

- para o banco
docker stop mariadb, 
docker start mariadb

- para o nodejs
docker stop node
docker start node

- para o apache
docker stop httpd
docker start httpd


..........................................................................

### troubleshouting

- verificando se o nodejs está funcionando

http://localhost:3000/perguntas/1   

obs: o numero no final é a sequencia das perguntas

-  subindo o nodejs manualmente

obs2: caso, apenas caso precise iniciar o npm do nodejs manualmente, será  necessário entrar no conteiner conforme comando abaixo:

- comando 1
docker exec -it node bash

- comando 2
nohup npm start &

- comando 3 ( caso queira validar)
tail -f nohup.out 

(vai aparecer deste jeito) significa que o node foi iniciado
> nodemysql@1.0.0 start /root
> nodejs select.js


