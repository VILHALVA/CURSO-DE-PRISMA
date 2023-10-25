# CRIANDO AZURE SQL SHADOW DATABASE
O conceito de um "Azure SQL Shadow Database" não é uma configuração ou recurso padrão no Azure SQL Database. Um banco de dados sombra geralmente se refere a um banco de dados secundário ou replicado que é mantido para fins de backup, recuperação ou testes. Você pode criar um banco de dados sombra manualmente no Azure SQL Database seguindo algumas etapas específicas. A ideia principal é criar uma cópia de segurança (snapshot) do banco de dados primário e restaurá-lo em um novo banco de dados. Aqui está um processo geral:

1. **Crie um Snapshot do Banco de Dados Primário**:
   - No Azure Portal, vá para o Azure SQL Database que você deseja criar como banco de dados sombra.
   - Na seção "Configurar", clique em "Criar instantâneo".
   - Siga as instruções para criar um instantâneo do banco de dados.

2. **Restaure o Instantâneo em um Novo Banco de Dados**:
   - No Portal do Azure, vá para a seção "Instantâneos de banco de dados" e selecione o instantâneo que você criou.
   - No menu, escolha "Restaurar" e siga as instruções para restaurar o instantâneo em um novo banco de dados. Você pode escolher um novo nome para o banco de dados sombra.

3. **Configure a Replicação (Opcional)**:
   - Se você deseja que o banco de dados sombra seja uma réplica em tempo real do banco de dados primário, pode configurar a replicação entre os dois bancos de dados. O Azure SQL Database oferece opções de replicação, como a Replicação de Grupo Elástico.

4. **Use o Banco de Dados Sombras**:
   - Agora você pode usar o banco de dados sombra para fins de backup, recuperação, testes ou qualquer outra finalidade que você tenha em mente.

Lembre-se de que a criação de um banco de dados sombra requer recursos adicionais e custos, pois você está mantendo uma cópia adicional dos dados. Além disso, a frequência da criação de instantâneos e da replicação depende das suas necessidades de recuperação e disponibilidade.

Certifique-se de considerar a estratégia de recuperação de desastres e a política de retenção de instantâneos para gerenciar seus bancos de dados sombra de forma eficaz e econômica. Além disso, consulte a documentação do Azure SQL Database e as práticas recomendadas específicas para a criação de bancos de dados sombra.