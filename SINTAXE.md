# SINTAXE
## CRIANDO PROJETO:
Para criar um novo projeto usando o Prisma, você geralmente segue estes passos:

### Passo 1: Instalação do Prisma CLI
Certifique-se de ter o Prisma CLI instalado globalmente em sua máquina. Você pode instalar usando o npm (Node Package Manager) através do seguinte comando:

```bash
npm install -g prisma
```

### Passo 2: Inicialização do projeto
Você pode iniciar um novo projeto Prisma executando o seguinte comando no terminal:

```bash
prisma init nome-do-projeto
```

Substitua "nome-do-projeto" pelo nome que você deseja dar ao seu projeto.

### Passo 3: Configuração do ambiente
Depois de criar o projeto, você precisará configurar seu ambiente de banco de dados. Isso pode ser feito modificando o arquivo `schema.prisma` no diretório do seu projeto. Este arquivo define o modelo de dados do seu aplicativo e a configuração do banco de dados.

### Passo 4: Gerar o client do Prisma
Após definir seu esquema no arquivo `schema.prisma`, você precisa gerar o cliente do Prisma. Isso é feito com o seguinte comando:

```bash
prisma generate
```

Este comando irá gerar o código TypeScript (ou JavaScript, dependendo da configuração do seu projeto) para interagir com o banco de dados.

### Passo 5: Implementação do código
Agora você pode começar a implementar a lógica do seu aplicativo usando o cliente Prisma gerado. Isso inclui a criação, leitura, atualização e exclusão de dados no banco de dados.

### Passo 6: Executar o projeto
Depois de implementar sua lógica de aplicativo, você pode executar o projeto usando qualquer estrutura ou ambiente de sua escolha (por exemplo, Express.js para back-end ou React.js para front-end).

### Passo 7: Publicar e implantar
Depois de testar e verificar que seu aplicativo está funcionando conforme esperado, você pode publicá-lo e implantá-lo em um ambiente de produção.

## EXEMPLOS DE CÓDIGOS:
Abaixo estão alguns exemplos de código usando o Prisma, juntamente com explicações sobre o que cada parte do código faz:

1. **Definição de um Modelo de Banco de Dados usando Prisma Schema:**

```prisma
// Arquivo: schema.prisma

// Define um modelo chamado 'User'
model User {
  id        Int      @id @default(autoincrement())
  name      String
  email     String   @unique
  createdAt DateTime @default(now())
}
```

- **Explicação:** Este código define um modelo de banco de dados simples chamado `User` com três campos: `id`, `name` e `email`. O campo `id` é uma chave primária autoincrementável, `email` é único e `createdAt` é uma data e hora padrão.

2. **Executando uma Migração para Aplicar o Esquema ao Banco de Dados:**

```bash
npx prisma migrate dev --name init
```

- **Explicação:** Este comando executa uma migração usando o Prisma CLI para aplicar as alterações definidas no arquivo de esquema do Prisma (`schema.prisma`) ao banco de dados. O parâmetro `--name init` define o nome da migração como "init".

3. **Usando o Prisma Client para Interagir com o Banco de Dados:**

```typescript
// Arquivo: app.ts

import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()

async function main() {
  // Cria um novo usuário
  const newUser = await prisma.user.create({
    data: {
      name: 'Alice',
      email: 'alice@example.com',
    },
  })
  console.log('Novo usuário criado:', newUser)

  // Consulta todos os usuários
  const allUsers = await prisma.user.findMany()
  console.log('Todos os usuários:', allUsers)
}

main()
  .catch((e) => {
    throw e
  })
  .finally(async () => {
    await prisma.$disconnect()
  })
```

- **Explicação:** Este código TypeScript usa o Prisma Client para criar um novo usuário no banco de dados e, em seguida, consulta todos os usuários existentes. O `PrismaClient` é importado do pacote `@prisma/client`. O método `prisma.user.create()` cria um novo registro na tabela `User` e o método `prisma.user.findMany()` consulta todos os registros na tabela `User`.

Esses são apenas alguns exemplos básicos de como usar o Prisma para definir esquemas de banco de dados, executar migrações e interagir com o banco de dados em seu aplicativo. O Prisma fornece uma API limpa e fácil de usar para manipular dados, tornando o desenvolvimento de aplicativos back-end mais eficiente e agradável.