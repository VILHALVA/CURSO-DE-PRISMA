# SINTAXE
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