



## Projeto da cadeira Sistemas Distribuídos

### Instruções para Configuração do Ambiente e Desenvolvimento do Backend:

1. **Instalação do Docker:**
   
   Siga as instruções no [site oficial do Docker](https://docs.docker.com/desktop/install/windows-install/) para instalar o Docker em seu sistema.

2. **Criar a Imagem e o Banco de Dados no Docker:**

   - Criar um contêiner MySQL com uma senha e um banco de dados personalizados:
   ```PowerShell
   docker run -d -p 3306:3306 --name db_sd -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=db_sd mysql:8.0
   ```
   ```PowerShell
   docker exec -it db_sd /bin/bash
   mysql -v
   mysql -u root -p -A
   SELECT user, host FROM mysql.user;
   UPDATE mysql.user SET host='%' WHERE user='root';
   FLUSH PRIVILEGES;
   ```

3. **Configuração do arquivo `.env`:**

   ```
  
   PORT=3333
   MYSQL_HOST=localhost
   MYSQL_USER=root
   MYSQL_PASSWORD=root
   MYSQL_DB=atendimento
   ```

4. **Abrir o Visual Studio Code:**

   Abra o Visual Studio Code para começar a trabalhar no backend do seu projeto.

5. **Criar a Estrutura do Backend:**

   Crie uma pasta para o backend do seu projeto no Visual Studio Code:
   ```bash
   mkdir backend
   ```

6. **Instalar as Dependências:**

   Certifique-se de que o Node.js e o npm estão instalados. Para verificar, execute:

   ```bash
   node -v
   npm -v
   ```

   Se não estiverem instalados, visite [nodejs.org](https://nodejs.org/) para baixar e instalar o Node.js, que inclui o npm.

   No terminal do Visual Studio Code, navegue até a pasta do backend e execute os seguintes comandos:

   ```bash
   npm install nodemon -D
   npm install dotenv
   npm install express
   npm install mysql2
   ```

7. **Montando o Banco de Dados:**

   Para configurar o banco de dados para o sistema de controle de atendimento em laboratórios médicos, execute os seguintes comandos SQL:

   ```sql
   -- Cria o banco de dados 'atendimento'
   CREATE DATABASE atendimento;

   -- Usar o banco de dados 'atendimento'
   USE atendimento;

   -- Cria a tabela 'Agentes'
   CREATE TABLE Agentes (
       id_agente INT AUTO_INCREMENT PRIMARY KEY,
       guiche ENUM('01', '02'),
       nome_agente VARCHAR(50)
   );

   -- Cria a tabela 'FilaTemp'
   CREATE TABLE FilaTemp (
       prioridade ENUM('SP', 'SE', 'SG'),
       data_emissao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
       ordem INT
   );

   -- Cria a tabela 'DataTemp'
   CREATE TABLE DataTemp (
       data_atendimento TIMESTAMP AUTO_INCREMENT CURRENT_TIMESTAMP
   );

   CREATE TABLE DisplayTemp (
       id_dpstemp INT AUTO_INCREMENT PRIMARY KEY,
       prioridade ENUM('SP', 'SE', 'SG'),
       data_emissao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
       ordem INT,
       guiche INT
   );

   -- Cria a tabela 'Senhas'
   CREATE TABLE Senhas (
       id INT AUTO_INCREMENT PRIMARY KEY,
       prioridade ENUM('SP', 'SE', 'SG'),
       data_emissao TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
       guiche INT,
       ordem INT,
       atendido TINYINT DEFAULT 0,
       data_atendimento TIMESTAMP,
       tempo_atendimento TIMESTAMP
   );

   INSERT INTO Agentes (guiche, nome_agente) VALUES (01, 'Jasé Chitsu');

   SET time_zone = 'America/Sao_Paulo';   
   ```

--- 

