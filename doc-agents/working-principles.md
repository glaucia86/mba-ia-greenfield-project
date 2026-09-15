# Princípios de trabalho (Working Principles)

Consulte ao organizar a execução, investigar um problema ou tomar decisões técnicas.

## Entender antes de alterar

1. Identifique o resultado esperado e os critérios de conclusão da tarefa.
2. Consulte apenas os guias relevantes do índice principal.
3. Inspecione o estado do Git e os arquivos diretamente envolvidos.
4. Verifique hipóteses no código e nas configurações antes de editar.

O planejamento descreve intenção; a implementação demonstra o comportamento atual. Registre divergências relevantes sem assumir que componentes planejados já estão disponíveis.

## Executar com foco

- Faça a menor mudança coerente que resolva o problema por completo.
- Reutilize padrões, dependências e configurações existentes quando forem adequados.
- Prefira decisões simples e reversíveis para detalhes rotineiros já incluídos no pedido.
- Peça esclarecimento quando uma ambiguidade alterar o resultado esperado ou exigir uma decisão do usuário; avance no trabalho independente dessa resposta.
- Preserve alterações locais não relacionadas e examine diffs antes de concluir.

## Validar e comunicar

Siga a [Política de testes](testing.md) para selecionar verificações proporcionais. Relate o que mudou, o motivo, os resultados da validação e limitações concretas. Não declare sucesso com base apenas na ausência de erros visíveis.

Em tarefas longas, comunique descobertas e próximos passos relevantes de forma breve. Evite narrar cada comando ou guardar a conversa inteira na documentação permanente.

## Manter contexto útil

Leia arquivos adicionais quando surgir uma necessidade específica. Referencie a fonte original em vez de copiar configurações ou requisitos para vários guias. Ao encontrar trabalho adicional, aplique os [Limites de escopo](scope-limits.md) antes de expandir a tarefa.
