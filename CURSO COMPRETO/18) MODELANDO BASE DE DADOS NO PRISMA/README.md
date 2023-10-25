# MODELANDO BASE DE DADOS NO PRISMA
O Prisma é uma ferramenta de modelagem e acesso a bancos de dados que facilita a criação e a interação com bancos de dados relacionais a partir de uma aplicação Node.js. Aqui estão os passos básicos para modelar uma base de dados no Prisma:

**1. Instale o Prisma**:
   Certifique-se de que você já tenha instalado o Prisma CLI. Se ainda não o fez, você pode instalar executando o seguinte comando:

   ```bash
   npm install -g prisma
   ```

**2. Inicialize um Novo Projeto do Prisma**:
   No diretório do seu projeto, inicie um novo projeto do Prisma executando:

   ```bash
   prisma init
   ```

   Isso criará uma estrutura de diretórios e arquivos para o projeto do Prisma.

**3. Defina o Schema do Prisma**:
   No diretório `prisma`, você encontrará um arquivo chamado `schema.prisma`. É neste arquivo que você define o modelo da sua base de dados. Você pode usar a linguagem de definição do Prisma para criar os modelos de entidades, campos e relações.

   Aqui está um exemplo de como você pode definir um modelo de usuário no `schema.prisma`:

   ```prisma
   model User {
     id       Int      @id @default(autoincrement())
     username String
     email    String   @unique
     posts    Post[]
   }
   ```

   Este exemplo define uma entidade `User` com campos `id`, `username`, `email` e uma relação com a entidade `Post`.

**4. Execute `prisma generate`**:
   Após definir o modelo no arquivo `schema.prisma`, você precisa gerar os artefatos de código correspondentes. Execute o seguinte comando para gerar os artefatos:

   ```bash
   prisma generate
   ```

   Isso gerará código para acesso ao banco de dados com base no seu modelo.

**5. Atualize o Banco de Dados**:
   Após gerar os artefatos, você precisa aplicar as mudanças ao banco de dados real. Execute o seguinte comando para criar ou atualizar o esquema do banco de dados:

   ```bash
   prisma db push
   ```

**6. Interaja com o Banco de Dados**:
   Agora, você pode interagir com o banco de dados usando as funções e classes geradas pelo Prisma. Por exemplo, para criar um novo usuário, você pode fazer o seguinte:

   ```javascript
   const { PrismaClient } = require('@prisma/client');
   const prisma = new PrismaClient();

   async function createUser() {
     const user = await prisma.user.create({
       data: {
         username: 'john_doe',
         email: 'john@example.com',
       },
     });
     console.log('Novo usuário criado:', user);
   }

   createUser()
     .catch((error) => {
       console.error('Erro ao criar usuário:', error);
     })
     .finally(async () => {
       await prisma.$disconnect();
     });
   ```

   Lembre-se de seguir as melhores práticas e a documentação do Prisma para modelar seu banco de dados de acordo com os requisitos do seu projeto.

O Prisma oferece muitos recursos poderosos, como migrações, consultas e operações de escrita complexas, e permite que você modele e acesse seu banco de dados de forma eficiente a partir do seu aplicativo Node.js. Certifique-se de consultar a documentação oficial do Prisma para obter mais detalhes e exemplos.