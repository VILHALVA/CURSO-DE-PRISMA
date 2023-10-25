# PRINCIPAIS CONCEITOS DO PRISMA
O Prisma é uma ferramenta de acesso a bancos de dados que simplifica o desenvolvimento de aplicativos com Node.js e TypeScript. Aqui estão alguns dos principais conceitos associados ao Prisma:

1. **Prisma Schema**:
   - O Prisma Schema é um arquivo central em que você define os modelos de dados da sua aplicação, suas relações e validações.
   - Ele é escrito em uma linguagem declarativa própria e oferece uma visão clara da estrutura do banco de dados.
   
2. **Modelos**:
   - Os modelos são entidades de dados que representam tabelas ou coleções no banco de dados.
   - Você define os campos de cada modelo no Prisma Schema, incluindo os tipos de dados e as relações com outros modelos.

3. **Relações**:
   - O Prisma permite definir relações entre modelos, como um relacionamento "um para muitos" ou "muitos para muitos", usando diretivas como `@relation` e `@map`.
   - Isso é fundamental para modelar relações complexas entre entidades no banco de dados.

4. **Consultas Prisma (Prisma Client)**:
   - O Prisma gera automaticamente um cliente (Prisma Client) com base no seu Prisma Schema.
   - O Prisma Client oferece métodos para realizar consultas e operações de banco de dados de forma tipada e segura em seu código TypeScript.

5. **Consultas Tipadas**:
   - As consultas feitas com o Prisma Client são tipadas, o que significa que os resultados são verificados em tempo de compilação, ajudando a evitar erros de digitação.

6. **Migrações**:
   - O Prisma suporta migrações de banco de dados, que são scripts gerados automaticamente para evoluir o esquema do banco de dados.
   - Isso é útil quando você precisa fazer alterações na estrutura do banco de dados sem perder dados.

7. **Transações**:
   - O Prisma permite criar transações, que são usadas para agrupar um conjunto de operações de banco de dados em uma única unidade atômica.
   - Isso garante a consistência dos dados em situações complexas.

8. **Controle de Versão do Schema**:
   - O Prisma oferece controle de versão para o Prisma Schema, permitindo que você evolua o esquema do banco de dados ao longo do tempo de forma controlada.

9. **Seed Data**:
   - O Prisma facilita a inclusão de dados iniciais no banco de dados (conhecidos como "seed data") por meio do uso de scripts e métodos no Prisma Client.

10. **Múltiplos Bancos de Dados**:
    - O Prisma suporta a conexão e a interação com múltiplos bancos de dados em uma única aplicação, caso seja necessário.

Estes são os principais conceitos relacionados ao Prisma. O Prisma se destaca por sua capacidade de simplificar o acesso a bancos de dados, a criação de esquemas de dados declarativos e a geração de código TypeScript tipado para consultas seguras. Essas características tornam o Prisma uma escolha popular para desenvolvedores que trabalham com Node.js e bancos de dados relacionais.