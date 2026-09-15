# Limites de escopo (Scope Limits)

Consulte quando houver dúvida sobre incluir trabalho adicional, alterar contratos ou executar ações fora do pedido.

## Dentro da tarefa

Inclua implementação, correções diretamente necessárias, validação e documentação afetada para concluir o resultado solicitado. Resolva detalhes rotineiros de forma autônoma quando forem compatíveis com o pedido e com os padrões existentes.

## Evitar expansão não solicitada

- Não implemente fases futuras do projeto apenas porque aparecem no planejamento.
- Não acrescente frontend, filas, armazenamento, autenticação ou persistência a uma tarefa que não depende desses componentes.
- Evite refatorações amplas, renomeações, formatação geral e atualizações de dependências sem relação com o objetivo.
- Não introduza frameworks, serviços ou mudanças de arquitetura sem necessidade demonstrável para a tarefa.
- Não altere contratos públicos ou dados persistidos como efeito colateral silencioso.

Se uma ampliação for necessária para concluir o pedido, explique a dependência. Solicite uma decisão quando envolver uma mudança material de requisitos, compatibilidade ou custo ainda não autorizada. Registre melhorias independentes como sugestões, sem executá-las automaticamente.

## Operações e dados

Não descarte trabalho local, apague dados, reescreva histórico compartilhado ou publique/deploye mudanças sem autorização aplicável ao pedido. Autorizações já dadas continuam válidas; não crie etapas repetidas de confirmação para ações já autorizadas.

Não envie mensagens a terceiros nem exponha credenciais como parte incidental do trabalho. Use os ambientes de desenvolvimento e teste apropriados.

## Conclusão

Conclua quando o resultado solicitado estiver implementado e as verificações adequadas tiverem sido realizadas, com limitações informadas. Não transforme problemas preexistentes sem relação com a tarefa em trabalho adicional obrigatório. Para preservar mudanças durante operações Git, consulte [Convenções Git](git-conventions.md).
