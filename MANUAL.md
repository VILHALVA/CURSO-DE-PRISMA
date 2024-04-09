# MANUAL
## INSTALAÇÃO E CONFIGURAÇÃO:
## [USANDO O `VOLTA`:](https://volta.sh/)
Usar o Volta pode ajudar a resolver problemas de incompatibilidade com o Node.js. Volta é um gerenciador de versões do Node.js que permite instalar e usar diferentes versões do Node.js em um ambiente de desenvolvimento, garantindo que você possa trabalhar com a versão específica necessária para seu projeto.

Ao usar o Volta, você pode facilmente alternar entre versões do Node.js em diferentes projetos ou até mesmo dentro do mesmo projeto, garantindo que cada um use a versão específica compatível com as dependências.

Aqui estão os passos básicos para instalar e usar o Volta:

1. **Instalação do Volta**:
   - Você pode instalar o Volta seguindo as instruções do site oficial: [Volta.sh](https://volta.sh/).
   - Geralmente, ela é feita com um único comando, que pode variar dependendo do seu sistema operacional.

2. **Instalação do Node.js com o Volta**:
   - Após instala-lo, você pode usar o comando `volta install node@<version>` para instalar uma versão específica do Node.js.
   - Por exemplo, para instalar o Node.js na versão 16.x, você pode executar:
   ```bash
   volta install node@16.13
   ```

3. **Usando o Node.js com o Volta**:
   - Depois de instalar o Node.js desejado com o Volta, você pode definir a versão específica do Node.js para um projeto usando o comando dentro do diretório do projeto:
   ```bash
   volta pin node@16.13
   ```
   - Isso garantirá que o Node.js especificado pelo Volta seja usado ao executar comandos relacionados ao Node.js dentro desse projeto.

Usando o Volta, você pode gerenciar facilmente as versões do Node.js e garantir a compatibilidade com suas aplicações Meteor.js e outras dependências do projeto.

## CRIANDO PROJETO:
### Passo 1: Instalação do Prisma CLI
Certifique-se de ter o Prisma CLI instalado globalmente em sua máquina. Você pode instalar usando o npm (Node Package Manager) através do seguinte comando:

```bash
npm install -g prisma
```

### Passo 2: Inicialização do projeto
Você pode iniciar um novo projeto Prisma executando o seguinte comando no terminal:

```bash
prisma init 
```

### Passo 3: Configuração do ambiente
- Depois de criar o projeto, você precisará configurar seu ambiente de banco de dados. Isso pode ser feito modificando o arquivo `schema.prisma` no diretório do seu projeto. Este arquivo define o modelo de dados do seu aplicativo e a configuração do banco de dados.

- Você precisa definir pelo menos um modelo em seu arquivo `schema.prisma`. Um modelo é uma representação de uma tabela em seu banco de dados. Aqui está um exemplo básico de como você pode definir um modelo `User` em seu arquivo `schema.prisma`:

```prisma
// prisma/schema.prisma

// Definição do modelo User
model User {
  id    Int     @id @default(autoincrement())
  email String  @unique
  name  String?
}

// Definição do provedor de banco de dados
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

// Definição do gerador
generator client {
  provider = "prisma-client-js"
}
```

* **Definição do modelo User:** Neste exemplo, o modelo `User` tem três campos: `id`, `email` e `name`. O campo `id` é uma chave primária que é autoincrementável. O campo `email` é único e o campo `name` é opcional. 
* **Definição do provedor de banco de dados:** Definimos também um datasource chamado db com o provedor de banco de dados postgresql. O URL do banco de dados é definido usando a função env() para recuperar a URL do banco de dados de uma variável de ambiente chamada DATABASE_URL. Certifique-se de substituir DATABASE_URL pelo nome da variável de ambiente que contém a URL do seu banco de dados PostgreSQL.
- **Definição do gerador:** Neste exemplo, definimos um gerador chamado client com o provedor prisma-client-js. Este gerador é responsável por gerar o código do cliente Prisma para acessar seu banco de dados PostgreSQL.

### Passo 4: Gerar o client do Prisma
Após definir seu esquema no arquivo `schema.prisma`, você precisa gerar o cliente do Prisma. Isso é feito com o seguinte comando:

```bash
prisma generate
```

Este comando irá gerar o código TypeScript (ou JavaScript, dependendo da configuração do seu projeto) para interagir com o banco de dados.

### Passo 5: Implementação do código
Agora que o Prisma Client foi gerado com sucesso, você pode começar a usá-lo em seu projeto Node.js para interagir com o banco de dados.

Aqui estão alguns passos que você pode seguir para começar a usar o Prisma Client em seu projeto:

1. **Importar o Prisma Client**: No seu código Node.js, importe o Prisma Client usando uma das opções fornecidas pelo Prisma após a geração do código. Por exemplo:
   ```javascript
   // Importar o Prisma Client
   import { PrismaClient } from '@prisma/client'

   // Criar uma instância do Prisma Client
   const prisma = new PrismaClient()

   // Usar o Prisma Client para fazer consultas ao banco de dados
   ```

2. **Fazer consultas ao banco de dados**: Use os métodos fornecidos pelo Prisma Client para fazer consultas ao seu banco de dados. Por exemplo, você pode fazer consultas de leitura, inserção, atualização e exclusão de dados.

3. **Gerenciar transações**: Se necessário, você pode usar transações para garantir que um conjunto de operações no banco de dados seja executado atomicamente.

4. **Lidar com erros**: Certifique-se de lidar adequadamente com erros ao usar o Prisma Client. Isso inclui lidar com erros de validação, erros de consulta e erros de conexão com o banco de dados.

5. **Explorar a documentação**: Explore a documentação oficial do Prisma para obter mais informações sobre como usar o Prisma Client, incluindo exemplos de código, guias e referências de API.

A partir daqui, você pode começar a desenvolver sua aplicação, utilizando o Prisma Client para interagir com o banco de dados de forma eficiente e segura. Se tiver dúvidas específicas ou precisar de mais ajuda em algum ponto específico, não hesite em perguntar! Estou aqui para ajudar.

### Passo 6: Executar o projeto
Depois de implementar sua lógica de aplicativo, você pode executar o projeto usando qualquer estrutura ou ambiente de sua escolha (por exemplo, Express.js para back-end ou React.js para front-end).

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

## DIRETÓRIOS:
- `node_modules/`: Este diretório contém as dependências do projeto, incluindo o Prisma Client.

- `prisma/`: Este diretório contém o arquivo `schema.prisma`, que é onde você define o esquema do seu banco de dados usando a Prisma Schema Language.

- `.env`: Este arquivo contém variáveis de ambiente, como a URL do banco de dados, que são usadas para configurar a conexão com o banco de dados.

- `.prisma/`: Este diretório contém arquivos de configuração para o Prisma, como o arquivo `schema.prisma`.

Além disso, o Prisma Client gera arquivos e diretórios adicionais no momento da compilação, mas eles podem variar dependendo do seu ambiente de desenvolvimento e das configurações específicas do projeto.

Lembre-se de que esses são os diretórios comuns gerados pelo Prisma, e podem haver outros diretórios ou arquivos dependendo da configuração do seu projeto.