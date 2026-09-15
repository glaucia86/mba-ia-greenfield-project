# Convenções de código

Consulte antes de implementar ou formatar código TypeScript.

## Estilo e nomenclatura

- Use indentação de dois espaços, aspas simples e vírgulas finais, conforme o código existente e a [configuração do Prettier](../nestjs-project/.prettierrc).
- Use PascalCase para classes e camelCase para métodos e variáveis.
- Nomeie arquivos pela responsabilidade: `video.controller.ts`, `video.service.ts` e `video.module.ts` são exemplos para funcionalidades futuras.
- Mantenha o tratamento HTTP nos controllers e o comportamento de negócio nos serviços; use a injeção de dependências do NestJS.
- Siga a configuração TypeScript existente e os padrões do código próximo à alteração.

## Formatação e análise estática

Execute no host, em `nestjs-project/`, com o container da API ativo:

```bash
docker compose exec nestjs-api npm run lint
docker compose exec nestjs-api npm run format
```

Ambos os comandos modificam arquivos: lint executa ESLint com `--fix`, e format executa Prettier sobre código e testes. Revise as diferenças e evite alterações de formatação sem relação com a tarefa.

[eslint.config.mjs](../nestjs-project/eslint.config.mjs) define verificações TypeScript que consideram informações de tipos e integração com Prettier. Consulte esse arquivo ao investigar regras; não duplique todas as regras aqui nem as desative apenas para silenciar falhas.

## Contratos REST

Ao criar endpoints de recursos, use substantivos no plural, como `/videos`, e métodos HTTP coerentes: GET para leitura, POST para criação, PATCH para atualização parcial e DELETE para remoção. Mantenha URLs e formatos de resposta consistentes com contratos existentes.

Escolha códigos de status pelo resultado: por exemplo, 201 para criação, 404 para recurso inexistente e 204 somente quando não houver corpo. Valide respostas de sucesso e erro em testes HTTP. Não altere contratos existentes apenas para uniformizar estilo fora do escopo da tarefa.

## Recursos necessários após o build

Ao adicionar templates, arquivos estáticos ou outros recursos carregados em execução, confira sua presença e seus caminhos em `dist/` após compilar. Configure `compilerOptions.assets` em [nest-cli.json](../nestjs-project/nest-cli.json) quando esses arquivos precisarem ser copiados pelo Nest CLI; use `watchAssets` se também precisarem acompanhar alterações durante desenvolvimento.

Não configure recursos inexistentes nem suponha que a compilação TypeScript copie todos os arquivos. Teste o carregamento no código compilado quando a alteração depender desses recursos. Para detalhes, consulte a [documentação de assets do Nest CLI](https://docs.nestjs.com/cli/monorepo#assets).

## Documentação

Use títulos Markdown descritivos, caminhos concretos e exemplos de comandos executáveis. Preserve a indentação de quatro espaços do diagrama Mermaid e verifique a renderização após alterações estruturais.
