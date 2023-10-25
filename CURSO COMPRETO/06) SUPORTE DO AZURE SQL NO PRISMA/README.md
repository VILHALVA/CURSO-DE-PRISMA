# SUPORTE DO AZURE SQL NO PRISMA
O Prisma é uma ferramenta popular para acessar bancos de dados relacionais a partir de aplicativos Node.js e TypeScript. O Prisma oferece suporte ao Azure SQL, permitindo que você se conecte a bancos de dados Azure SQL e interaja com eles usando consultas e operações tipadas. Para usar o Azure SQL com o Prisma, siga estas etapas:

1. **Configuração Inicial**:
   - Certifique-se de ter o Prisma instalado em seu projeto. Você pode fazê-lo usando o npm ou yarn.
   - Em seu diretório de projeto, execute `prisma init` para criar o arquivo `schema.prisma`, que é onde você definirá seu esquema de banco de dados.

2. **Definindo a Conexão com o Azure SQL**:
   - Abra o arquivo `schema.prisma` e defina uma conexão para o seu banco de dados Azure SQL. Aqui está um exemplo de uma definição de conexão:

   ```prisma
   datasource azure {
     provider = "sqlserver"
     url      = env("DATABASE_URL")
   }
   ```

   - Substitua `DATABASE_URL` pelo URL de conexão do seu banco de dados Azure SQL. Esse URL incluirá informações como o nome do servidor, a porta, o nome do banco de dados e as credenciais de autenticação.

3. **Gerando o Prisma Client**:
   - Execute `npx prisma generate` ou `yarn prisma generate` para gerar o Prisma Client com base nas informações do seu `schema.prisma`.

4. **Usando o Prisma Client**:
   - Agora, você pode usar o Prisma Client para realizar consultas e operações no banco de dados Azure SQL. Por exemplo, para recuperar todos os registros de uma tabela:

   ```javascript
   const { PrismaClient } = require('@prisma/client');
   const prisma = new PrismaClient();

   async function getAllRecords() {
     const records = await prisma.tableName.findMany();
     return records;
   }
   ```

   Certifique-se de substituir `tableName` pelo nome da tabela que você deseja consultar.

5. **Migrações de Banco de Dados**:
   - O Prisma também oferece suporte a migrações de banco de dados para evoluir o esquema do banco de dados conforme necessário. Você pode usar o Prisma CLI para gerar e aplicar migrações.

Certifique-se de revisar a documentação oficial do Prisma para obter informações detalhadas e exemplos relacionados ao uso do Prisma com o Azure SQL, uma vez que os detalhes específicos podem variar dependendo do seu ambiente e configuração.