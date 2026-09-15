# Desenvolvimento local e configuração

Consulte ao instalar dependências, iniciar a API ou alterar containers e configurações de ambiente.

## Pré-requisitos

O [README principal](../README.md) especifica Docker, Node.js v25+ e npm. Verifique em [Dockerfile.dev](../nestjs-project/Dockerfile.dev) a versão do Node fixada para o container. Execute os comandos em `nestjs-project/`.

## Preparar infraestrutura

Prepare o arquivo `.env` local exigido pelo [compose.yaml](../nestjs-project/compose.yaml), usando as variáveis necessárias à implementação. Não invente variáveis obrigatórias nem copie segredos de produção.

```bash
docker compose up -d db mailhog
docker compose ps
docker compose exec db pg_isready -U streamtube
```

“Subir o ambiente” significa iniciar apenas a infraestrutura. Confirme que os serviços solicitados estão ativos e prontos conforme [Redes Docker](docker-networking.md), incluindo MailHog. Não declare sucesso apenas porque `up -d` terminou.

## Preparar ferramentas e iniciar a aplicação

Para instalar dependências, compilar ou testar, prepare o container da API:

```bash
docker compose up -d nestjs-api
docker compose exec nestjs-api npm install
```

Instale dependências no primeiro uso ou quando elas mudarem. O comando padrão do container mantém o processo ativo sem iniciar NestJS. Isso permite executar ferramentas sem servir a aplicação.

Quando o pedido incluir rodar ou servir o projeto:

```bash
docker compose exec nestjs-api npm run start:dev
```

`start:dev` monitora alterações. A API usa `PORT` ou, por padrão, 3000; alinhe mudanças com as portas do Compose. Confira o HTTP após iniciar, usando `curl.exe -i http://localhost:3000` no Windows ou `curl -i http://localhost:3000` em outros ambientes. O scaffold atual responde 200 e `Hello World!`; atualize a verificação se esse contrato mudar.

## Processos contínuos e encerramento

Servidor e modos watch devem usar uma sessão gerenciada ou processo em segundo plano com saída consultável. Não aguarde indefinidamente seu término nem inicie instâncias duplicadas. Informe como acessar a aplicação e encerrar a sessão; finalize apenas processos iniciados para a tarefa quando não precisarem permanecer ativos.

A saída de um processo iniciado com `docker compose exec` pode estar na sessão de execução; consulte-a além dos logs do container. Use `docker compose down` no host quando o pedido incluir encerrar o ambiente. Não acrescente `-v` nem remova dados como limpeza automática.

## Cuidados com a configuração

Trate as credenciais do Compose como exclusivas de desenvolvimento. Documente novas variáveis com exemplos sem dados sensíveis. Não inclua dependências geradas, arquivos compilados ou relatórios de cobertura nos commits. Atualize as instruções de configuração quando os requisitos de inicialização mudarem.

O Compose já injeta variáveis por `env_file`. Configure carregamento adicional com dotenv somente se necessário à execução escolhida. Valores como `MAIL_FROM="StreamTube <noreply@streamtube.local>"` podem usar aspas para clareza; um arquivo `.env` não é um script de shell. Não execute seu conteúdo como comandos.
