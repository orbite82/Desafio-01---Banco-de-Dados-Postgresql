<div align="center">
<img src="https://user-images.githubusercontent.com/47891196/139104117-aa9c2943-37da-4534-a584-e4e5ff5bf69a.png" width="350px" />
</div>

# Desafio 01 - Banco de Dados Postgresql

Você está dando os primeiros passos no uso de containers. E a melhor forma de iniciar no mundo de containers é usar em ambiente de desenvolvimento.

Sua missão é ajudar a equipe de desenvolvimento a ter mais autonomia no desenvolvimento de projetos. E uma das reclamações da equipe é o setup local.

Crie um comando para criar um banco de dados PostgreSQL no ambiente do desenvolvedor de uma forma que cumpra os seguintes requisitos:

O nome do banco de dados deve ser curso_docker
O usuário de acesso ao banco deve ser docker_usr
A senha do usuário deve ser docker_pwd
Lembrando que a execução em container deve ser transparente pra quem está desenvolvendo. E que aqui você não precisa se preocupar com a perda dos dados do banco e nem nada disso, é apenas para desenvolvimento pontual.

Coloque aqui embaixo o comando que a equipe deve usar pra criar um banco de dados PostgreSQL com esses requisitos.


1. **Criar um Container PostgreSQL**: Execute o seguinte comando no terminal. Este comando irá baixar a imagem do PostgreSQL e criar um novo container.

   ```bash
   docker run --name meu-postgres -e POSTGRES_USER=meu_usuario -e POSTGRES_PASSWORD=minha_senha -e POSTGRES_DB=meu_banco -p 5432:5432 -d postgres
   ```

   **Explicação dos parâmetros**:
   - `--name meu-postgres`: nomeia o container como "meu-postgres".
   - `-e POSTGRES_USER=meu_usuario`: define o usuário do banco de dados.
   - `-e POSTGRES_PASSWORD=minha_senha`: define a senha do usuário.
   - `-e POSTGRES_DB=meu_banco`: cria um banco de dados com o nome especificado.
   - `-p 5432:5432`: mapeia a porta 5432 do container para a porta 5432 do host.
   - `-d`: executa o container em segundo plano (modo "detached").
   - `postgres`: especifica a imagem do PostgreSQL.

3. **Verificar se o Container está em Execução**: Para verificar se o container foi criado e está em execução, use:

   ```bash
   docker ps
   ```

4. **Conectar ao Banco de Dados**: Você pode usar um cliente SQL, como o `psql`, ou uma interface gráfica, como o DBeaver ou pgAdmin, para se conectar ao banco de dados. Os detalhes de conexão seriam:
   - Host: `localhost`
   - Porta: `5432`
   - Usuário: `meu_usuario` = docker_usr
   - Senha: `minha_senha` = docker_pwd
   - Banco de dados: `meu_banco` = curso_docker

5. **Acessar o Container** (opcional): Se você quiser acessar o shell do PostgreSQL dentro do container, use:

   ```bash
   docker exec -it meu-postgres psql -U meu_usuario -d meu_banco
   ```

6. **Parar e Remover o Container**: Para parar o container, use:

   ```bash
   docker stop meu-postgres
   ```

   E para removê-lo:

   ```bash
   docker rm meu-postgres
   ```

# Ou No Banco de dados

Para criar um banco de dados PostgreSQL com os requisitos especificados, você pode usar o seguinte comando SQL no ambiente do desenvolvedor. Assumindo que você já tenha acesso ao PostgreSQL, você pode executar esses comandos no terminal ou em um cliente de banco de dados como o `psql`.

```sql
-- Criar o usuário
CREATE USER docker_usr WITH PASSWORD 'docker_pwd';

-- Criar o banco de dados
CREATE DATABASE curso_docker WITH OWNER docker_usr;

-- Conceder permissões ao usuário no banco de dados
GRANT ALL PRIVILEGES ON DATABASE curso_docker TO docker_usr;
```

### Passos para execução:

1. Acesse o terminal do PostgreSQL:
   ```bash
   psql -U postgres
   ```

2. Cole os comandos acima e pressione Enter.

### Observação:
- Certifique-se de ter permissões adequadas para criar usuários e bancos de dados.
- O nome do usuário, banco de dados e senha devem ser ajustados caso você precise seguir alguma convenção específica no seu ambiente.
