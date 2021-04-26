
## Como instalar
1. Copie o arquivo `.env.example` e renomeie para `.env` (altere o valor da variáveis se desejar)
2. Instale Docker e certifique-se que Docker Compose (docker-compose) está disponível
3. Clone este repositório
4. Clone o repositório da aplicação em `./apps`
5. Crie o arquivo de configuração do apache (vhosts.conf) em `./config/apache` (há um exemplo em `config-samples/apache/foobar.conf`)
6. Suba os containers com o comando: ```docker-compose up --build --detach``` 
7. Conecte no servidor de banco de dados: ```mysql -h127.0.0.1 -uroot --ssl-mode=disabled -p``` e informe a senha contida no arquivo `.env` 
8. Crie o banco de dados: ```CREATE DATABASE nome_do_database;```
9. Conceda acesso ao banco de dados: ```GRANT ALL PRIVILEGES ON nome_do_database.* TO 'developers'@'%';```
10. ```FLUSH PRIVILEGES;```
11. Altere o arquivo hosts do seu sistema operacional adicionando a o domínio criado no arquivo de configuração do apache. Ex: ```127.0.0.1     local.transactionapi```
13. Conecte-se ao container da aplicação para realizar a instalação do projeto através do composer ```docker exec -it app bash``` e então, na pasta do projeto: ```composer install```
