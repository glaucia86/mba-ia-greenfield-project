# Repository Guidelines

## Contexto do projeto

StreamTube é uma plataforma de compartilhamento de vídeos do MBA Full Cycle. A implementação atual é um backend NestJS 11 com TypeScript em `nestjs-project/`; planejamento e arquitetura ficam em `docs/`. Frontend, workers e armazenamento de objetos são componentes planejados. Verifique o código antes de assumir que uma funcionalidade existe.

## Progressive Disclosure

Comece por este arquivo. Leia apenas o guia correspondente à tarefa e, depois, os arquivos específicos de código ou configuração referenciados. Não carregue toda a pasta `doc-agents/` nem o planejamento completo por padrão. Se a tarefa envolver mais de uma área, consulte somente os guias relevantes.

Ao trabalhar em `nestjs-project/`, consulte primeiro o [AGENTS.md do backend](nestjs-project/AGENTS.md). Ele reúne as orientações locais e direciona aos guias técnicos conforme a tarefa.

| Quando trabalhar com… | Consulte |
| --- | --- |
| Estrutura, módulos ou requisitos de funcionalidades | [Arquitetura](doc-agents/architecture.md) |
| Organização da execução e decisões técnicas | [Princípios de trabalho](doc-agents/working-principles.md) |
| Dúvidas sobre abrangência ou mudanças adicionais | [Limites de escopo](doc-agents/scope-limits.md) |
| Branches, commits, merges ou conflitos | [Convenções Git](doc-agents/git-conventions.md) |
| Descrição de PRs ou manutenção dos guias | [Contribuição](doc-agents/contributing.md) |

## Regras essenciais

- Faça mudanças focadas e preserve trabalhos não relacionados.
- Valide o comportamento alterado e informe verificações não executadas.
- Mantenha segredos em arquivos de ambiente locais ignorados pelo Git.
- Preserve o português na documentação existente.
- Diferencie funcionalidades planejadas das implementadas, usando código e configuração como evidência.

## Manutenção dos guias

Mantenha aqui apenas contexto, direcionamento e regras compartilhadas. Coloque procedimentos detalhados no guia correspondente, com indicação de quando consultá-lo. Referencie configurações originais em vez de copiá-las. Atualize orientações afetadas por mudanças; não acumule históricos de tarefas ou resultados temporários nestes arquivos.
