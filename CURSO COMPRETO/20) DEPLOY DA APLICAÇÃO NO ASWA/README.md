# DEPLOY DA APLICAÇÃO NO ASWA
O deploy de uma aplicação no Azure Static Web Apps (ASWA) envolve a implantação de seu aplicativo web estático no Azure usando o serviço ASWA. O ASWA simplifica o processo de implantação de aplicativos estáticos, permitindo que você implante facilmente seu código no Azure diretamente do seu repositório no GitHub. Aqui estão as etapas gerais para realizar o deploy de sua aplicação no ASWA:

**Pré-requisitos**:
1. Certifique-se de que você tenha uma conta no Azure e tenha configurado um repositório no GitHub para o código-fonte da sua aplicação web estática.

**Passos para Deploy**:

1. **Preparação do Repositório**:
   - Certifique-se de que seu repositório no GitHub contenha o código-fonte da sua aplicação estática e um arquivo de configuração chamado `.github/workflows/azure-static-web-apps.yml` para a automação do deploy.

2. **Crie um Recurso do Azure Static Web Apps**:
   - Acesse o Portal do Azure e crie um novo recurso do Azure Static Web Apps.
   - Conecte o recurso à sua conta do GitHub, selecione o repositório que contém seu código-fonte e siga as instruções para configurar as opções do ASWA.

3. **Configuração do GitHub Actions**:
   - O arquivo `.github/workflows/azure-static-web-apps.yml` define as configurações de implantação no GitHub Actions. Certifique-se de que ele esteja configurado corretamente. Aqui está um exemplo simples desse arquivo:

   ```yaml
   name: Build and deploy.

   on:
     push:
       branches:
         - main

   jobs:
     build_and_deploy_job:
       if: github.event_name == 'push' || (github.event_name == 'workflow_dispatch')
       runs-on: ubuntu-latest

       steps:
       - uses: actions/checkout@v2

       - name: Build and Deploy
         id: builddeploy
         uses: Azure/static-web-apps-deploy@v0.0.1
         with:
           azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_MYAPP }}
           repo_token: ${{ secrets.GITHUB_TOKEN }}
           action: 'upload'
           app_location: '/' # This is the folder with your built output
           api_location: 'api' # This is where your Azure Functions code lives
           app_artifact_location: 'webapp'

       - name: Post Deploy Step
         id: post_deploy
         run: |
           echo "Post Deploy Step"
           curl -X POST https://<your-function-app>.azurewebsites.net/api/refresh
         continue-on-error: true
   ```

   Certifique-se de substituir `<your-function-app>` pelo nome do seu aplicativo de funções do Azure, caso você tenha um.

4. **Commit e Push para o Repositório do GitHub**:
   - Faça um commit das alterações em seu repositório local e faça um push para o repositório do GitHub. Isso acionará o GitHub Actions para iniciar o processo de build e deploy no Azure.

5. **Acompanhe o Progresso no Portal do Azure**:
   - Acesse o portal do Azure para acompanhar o progresso da implantação e verificar se tudo ocorreu conforme o esperado.

6. **Acesse a Aplicação**:
   - Após a conclusão da implantação, você pode acessar sua aplicação usando o URL fornecido no portal do Azure para o recurso do Azure Static Web Apps.

Lembre-se de que essas são diretrizes gerais e as configurações específicas do seu projeto podem variar. Certifique-se de consultar a documentação do Azure Static Web Apps e a documentação do GitHub Actions para obter mais detalhes e resolver problemas específicos. Além disso, adapte as etapas de acordo com o sistema de controle de versão e as ferramentas de build que você está usando em seu projeto.