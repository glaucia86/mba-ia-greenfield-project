# Convenções Git

Consulte ao criar branches, preparar alterações, escrever commits, integrar trabalho ou resolver conflitos.

## Branches

Use uma branch de curta duração para cada alteração coerente. Os nomes sugeridos usam um prefixo em minúsculas e uma descrição em kebab-case:

- `feat/video-upload`
- `fix/account-validation`
- `docs/agent-guidelines`
- `chore/update-tooling`

Estas são recomendações para contribuição; o histórico atual não estabelece uma política de nomes de branches. Verifique a branch de origem pretendida antes de criar outra; o checkout atual usa `main`.

## Mensagens de commit

Siga o estilo existente em inglês e no imperativo: `Add project plan documentation for StreamTube`. Mantenha os títulos concisos e descreva a alteração resultante. Use o corpo da mensagem quando o motivo ou uma decisão precisar de explicação.

Exemplos: `Add video upload validation`, `Fix account confirmation handling` e `Document local development setup`. Não existe exigência estabelecida de prefixos Conventional Commits. Separe alterações sem relação entre si em commits distintos.

## Revisão e preparação

Execute na raiz do repositório:

```bash
git status --short
git diff
git add doc-agents/git-conventions.md
git diff --cached
git diff --cached --check
```

Substitua o caminho de exemplo pelos arquivos pretendidos. Prepare caminhos explícitos ou trechos selecionados, especialmente quando houver trabalho não relacionado. Inspecione arquivos não rastreados antes de adicioná-los: o comando `git diff` comum não mostra seu conteúdo. Exclua credenciais, dependências, arquivos compilados e relatórios de cobertura.

Execute as verificações adequadas à alteração, conforme a [Política de testes](testing.md), antes de criar o commit. Registre a validação relevante no PR.

## Integração e conflitos

Inspecione a árvore de trabalho e as alterações recebidas antes de executar merge ou rebase. Preserve edições não relacionadas. Resolva conflitos entendendo ambas as alterações; depois revise as diferenças resultantes e execute novamente as verificações afetadas.

Nenhuma estratégia de merge ou política de proteção de branches está documentada aqui; siga as configurações do repositório e a orientação dos mantenedores. Evite reescrever histórico compartilhado. Não use force push, hard reset ou comandos de limpeza de arquivos para contornar conflitos ou descartar o trabalho de outra pessoa.

Para descrições de PRs e manutenção da documentação, consulte [Contribuição](contributing.md).
