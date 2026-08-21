# Vizinhança Real

Aplicativo para avaliações reais de imóveis de aluguel, ajudando futuros inquilinos a saber como é morar em um lugar antes de assinar o contrato.

> "Descubra como é realmente morar ali antes de assinar."

Anúncios de aluguel mostram fotos, metragem e preço — mas não mostram infiltração, elevador quebrado, internet ruim ou proprietário lento para resolver problema. O Vizinhança Real reúne avaliações reais de quem já morou no imóvel, no condomínio, com o proprietário ou com a imobiliária, para que quem está prestes a alugar saiba disso antes de assinar.

## Equipe

Maria Fernanda Costa, Pedro Rangel, Giovanna Niel

## Como funciona

- **Busca** — digite parte do endereço ou nome do condomínio e veja os resultados filtrarem em tempo real.
- **Avaliação em 4 categorias** — apartamento, condomínio, proprietário e imobiliária, cada uma com nota de 1 a 5 e comentário opcional.
- **"O que eu gostaria de saber antes de alugar"** — campo obrigatório de texto livre em toda avaliação, para deixar o alerta específico em vez de genérico.
- **Nota + relato sempre juntos** — a nota é a visão geral, o relato é a experiência real; as duas aparecem sempre lado a lado.

Mais detalhes de escopo, métricas e prioridades em [`PRD (1).md`](<./PRD (1).md>). O sistema de design (tokens de cor, tipografia, tom de voz e as 5 telas do MVP) está em [`design (2).md`](<./design (2).md>).

## Stack

| Camada | Tecnologia |
|---|---|
| Linguagem | TypeScript |
| Gerenciador de pacotes | pnpm workspaces (Node.js 24) |
| API | Express 5 |
| Banco de dados | PostgreSQL + Drizzle ORM |
| Validação | Zod (`zod/v4`), `drizzle-zod` |
| Geração de API | Orval (a partir da spec OpenAPI) |
| Build | esbuild |
| Mobile | Expo / React Native |

## Estrutura do repositório

Monorepo organizado em pnpm workspaces:

```
artifacts/
  api-server/       # servidor Express (API)
  mobile/           # app mobile (Expo / React Native)
  mockup-sandbox/   # sandbox de protótipos/mockups (Vite)
lib/
  api-client-react/ # hooks de cliente da API para React (gerados via Orval)
  api-spec/         # spec OpenAPI, fonte de verdade dos contratos de API
  api-zod/          # schemas Zod compartilhados
  db/               # schema do banco (Drizzle ORM) e migrações
scripts/            # scripts utilitários do workspace
docs/               # documentação do projeto
```

## Como rodar

Pré-requisitos: Node.js 24, pnpm, e uma instância PostgreSQL.

```bash
# instalar dependências (obrigatório usar pnpm)
pnpm install

# configurar variável de ambiente obrigatória
export DATABASE_URL="postgres://usuario:senha@host:porta/banco"

# rodar a API (porta 5000)
pnpm --filter @workspace/api-server run dev

# aplicar o schema do banco (apenas em desenvolvimento)
pnpm --filter @workspace/db run push

# regenerar hooks de API e schemas Zod a partir da spec OpenAPI
pnpm --filter @workspace/api-spec run codegen
```

### Outros comandos úteis

```bash
pnpm run typecheck   # typecheck completo de todos os pacotes
pnpm run build       # typecheck + build de todos os pacotes
```

## Repositório no GitHub

O remoto canônico é `origin` e a branch de publicação é `main`. Mais detalhes em [`docs/github-integration.md`](./docs/github-integration.md).

## Licença

MIT
