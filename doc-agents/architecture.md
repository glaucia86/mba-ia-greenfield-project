# Arquitetura e estrutura do projeto

Consulte ao localizar código, alterar limites entre módulos ou determinar o escopo de funcionalidades.

## Estrutura atual

- `nestjs-project/src/main.ts`: inicialização da aplicação HTTP.
- `nestjs-project/src/app.module.ts`: módulo raiz do NestJS.
- `nestjs-project/src/app.controller.ts` e `app.service.ts`: endpoint e serviço iniciais.
- `nestjs-project/src/*.spec.ts`: testes unitários junto ao código.
- `nestjs-project/test/`: testes HTTP de ponta a ponta e configuração do Jest.
- `nestjs-project/compose.yaml`: container da API, PostgreSQL e MailHog.

O backend é uma estrutura inicial. A presença de um container de banco de dados não implica persistência ou migrações implementadas. Ainda não existe frontend nem diretório de recursos estáticos da aplicação.

## Arquitetura planejada

Consulte o [diagrama C4](../docs/diagrams/software-arch.mermaid) ao alterar interações entre serviços. Ele descreve Next.js, NestJS, PostgreSQL, um worker FFmpeg, S3/MinIO, uma fila de processamento e SMTP. A tecnologia da fila permanece indefinida no diagrama.

Para requisitos de funcionalidades, localize e leia apenas a fase relevante no [plano do projeto](../docs/project-plan.md). Verifique suas dependências antes de implementar. Diferencie a arquitetura planejada do código atual.

## Alterações

Agrupe novos comportamentos do backend em módulos NestJS adequados e registre os providers e controllers. Atualize o diagrama quando os caminhos de comunicação ou limites entre serviços mudarem. Atualize o plano quando o escopo ou as dependências de entrega mudarem; evite manter outro inventário de funcionalidades aqui.
