# StreamTube — Plataforma de Compartilhamento de Vídeos

Projeto da disciplina **Desenvolvimento de Aplicações de IA** do MBA de Engenharia de Software com IA da [Full Cycle](https://fullcycle.com.br).

Este é um projeto greenfield desenvolvido para demonstrar como construir uma aplicação do zero utilizando IA de forma adequada no processo de desenvolvimento.

## 📋 Pré-requisitos

- Docker
- Node.js v25+
- npm

## 🏗️ Arquitetura

O projeto segue uma arquitetura baseada em containers:

- **Frontend** (Next.js) — Interface da plataforma
- **API** (Nest.js) — Regras de negócio e autenticação
- **Video Worker** (FFmpeg) — Processamento de vídeos em background
- **Database** (PostgreSQL) — Usuários, canais, vídeos, comentários, likes
- **Object Storage** (S3/MinIO) — Arquivos de vídeo e thumbnails
- **Message Queue** — Fila de processamento de vídeos
- **Email Service** (SMTP) — Confirmação de conta e recuperação de senha

O diagrama de arquitetura completo está em `docs/diagrams/software-arch.mermaid`.

## 🚀 Instalação

### Backend (NestJS)

```bash
cd nestjs-project
docker compose up -d
docker compose exec nestjs-api bash
npm install
npm run start:dev
```

A API estará disponível em `http://localhost:3000`.

### Executar testes

```bash
# Testes unitários
npm run test

# Testes e2e
npm run test:e2e

# Cobertura de testes
npm run test:cov
```

## 🛠️ Estrutura do Projeto

```text
green-field-ai-project/
├── docs/
│   └── diagrams/
│       └── software-arch.mermaid        # Diagrama de arquitetura (C4)
├── nestjs-project/                      # Backend API
│   ├── src/
│   │   ├── main.ts                      # Entry point
│   │   ├── app.module.ts                # Módulo raiz
│   │   ├── app.controller.ts            # Controller principal
│   │   ├── app.controller.spec.ts       # Testes unitários do controller
│   │   └── app.service.ts               # Service principal
│   ├── test/
│   │   ├── app.e2e-spec.ts              # Testes e2e
│   │   └── jest-e2e.json                # Configuração Jest e2e
│   ├── compose.yaml                     # Docker Compose (API + PostgreSQL)
│   ├── Dockerfile.dev                   # Dockerfile de desenvolvimento
│   ├── eslint.config.mjs                # Configuração ESLint
│   ├── nest-cli.json                    # Configuração NestJS CLI
│   ├── package.json                     # Dependências do projeto
│   ├── tsconfig.json                    # Configuração TypeScript
│   ├── tsconfig.build.json              # Configuração TypeScript (build)
│   └── README.md                        # Documentação do backend
├── .gitignore
├── LICENSE
└── README.md
```

## 📚 Fases do Projeto

| Fase | Descrição | Dependência | Status |
|------|-----------|-------------|--------|
| **01** | Configuração Base do Projeto | — | 🔄 Em andamento |
| **02** | Cadastro, Login e Gerenciamento de Conta | Fase 01 | ⏳ Pendente |
| **03** | Upload e Processamento de Vídeos | Fase 01, 02 | ⏳ Pendente |
| **04** | Gerenciamento de Vídeos e Canal | Fase 02, 03 | ⏳ Pendente |
| **05** | Página de Visualização do Vídeo | Fase 03, 04 | ⏳ Pendente |
| **06** | Interações Sociais (Likes, Comentários, Inscrições) | Fase 02, 05 | ⏳ Pendente |
| **07** | Página Inicial, Busca e Finalização | Todas | ⏳ Pendente |

## 📖 Stack Tecnológica

| Camada | Tecnologia |
|--------|------------|
| Frontend | Next.js |
| Backend | NestJS 11, TypeScript, Express |
| Banco de Dados | PostgreSQL 17 |
| Containerização | Docker, Docker Compose |
| Testes | Jest, Supertest |
| Linting | ESLint, Prettier |

---

> Projeto desenvolvido por [Glaucia Lemos](https://github.com/glaucia86) como parte do MBA de Engenharia de Software com IA — Full Cycle. Iniciado em maio de 2026.