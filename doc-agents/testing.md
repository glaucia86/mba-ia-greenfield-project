# Política de testes (Testing Policy)

Consulte ao escrever testes ou decidir como validar uma alteração.

## Ferramentas e localização

O backend usa Jest, ts-jest, utilitários de teste do NestJS e Supertest.

- Unitários: `src/**/*.spec.ts`, junto ao código; configuração em [package.json](../nestjs-project/package.json).
- End-to-end: `test/*.e2e-spec.ts`; configuração em [jest-e2e.json](../nestjs-project/test/jest-e2e.json).
- Cobertura: `nestjs-project/coverage/`. Não existe percentual mínimo configurado.

Escolha o tipo pelo comportamento: unitários isolam colaboradores e não acessam banco ou rede; integração exercita componentes reais, sem exigir banco quando a integração não o envolve; end-to-end valida o ciclo HTTP e pode não usar persistência. O teste HTTP atual não acessa banco.

Se forem adicionados testes `*.integration-spec.ts`, atualize deliberadamente a descoberta no Jest e separe as suítes conforme suas dependências. Esse sufixo ainda não é reconhecido pela configuração unitária atual. Não adicione TypeORM, dotenv ou infraestrutura apenas para seguir uma convenção de testes.

## Validação proporcional à mudança

| Alteração | Verificação |
| --- | --- |
| Comportamento de serviço ou controller | Teste de comportamento alterado, suíte unitária e build |
| Contrato HTTP ou integração da aplicação | Verificações anteriores e testes end-to-end relevantes |
| Correção de defeito | Teste de regressão quando reproduzir o defeito de forma útil e estável |
| Documentação | Links, caminhos, comandos e estrutura; renderização se alterar Mermaid |
| Configuração Docker | Validar Compose e verificar comunicação afetada quando o ambiente estiver disponível |

Não crie testes que apenas repitam a implementação. Alterações de texto não exigem testes da aplicação. Evite repetir verificações já aprovadas sem novas mudanças, falhas ou dúvidas que justifiquem isso.

## Comandos

Com o container da API preparado conforme [Desenvolvimento](development.md), execute no host, em `nestjs-project/`:

```bash
docker compose exec nestjs-api npm test
docker compose exec nestjs-api npm run test:e2e
docker compose exec nestjs-api npm run test:cov
docker compose exec nestjs-api npm run build
```

Durante a implementação, prefira verificações focadas: `docker compose exec nestjs-api npm test -- --runTestsByPath src/app.controller.spec.ts`. Antes de concluir mudanças de código, execute a suíte unitária, o build e os testes HTTP relevantes conforme a tabela. Para diagnóstico de tipos, use `docker compose exec nestjs-api npx tsc --noEmit` quando necessário; isso não é exigido para alterações de texto.

Para watch, use `docker compose exec nestjs-api npm run test:watch` em sessão gerenciada conforme o guia de desenvolvimento. Use cobertura para investigar lacunas, sem inventar um percentual obrigatório.

## Qualidade e isolamento

Teste resultados observáveis, caminhos de erro relevantes e contratos HTTP. Feche aplicações NestJS no teardown. Use dados isolados; testes não devem enviar e-mails reais nem modificar dados de produção. Simule dependências externas em testes unitários e declare serviços necessários aos testes de integração.

Se futuras suítes compartilharem banco ou estado mutável, prefira isolamento. Quando a execução serial for necessária, passe `-- --runInBand`, por exemplo: `docker compose exec nestjs-api npm run test:e2e -- --runInBand`. O script atual não inclui essa opção e os testes atuais não demonstram necessidade de serialização obrigatória.

## Evidências

Informe comandos executados, resultados e limitações do ambiente. Diferencie falhas introduzidas de problemas preexistentes quando houver evidência. Nunca declare como aprovado um teste não executado. Para diagnóstico de conectividade, consulte [Docker Networking](docker-networking.md).
