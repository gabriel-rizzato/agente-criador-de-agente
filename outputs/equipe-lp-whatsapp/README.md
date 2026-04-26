# equipe-lp-whatsapp

> Equipe de agentes que produz landing pages HTML completas, focadas em conversao para WhatsApp, a partir de um briefing fornecido pelo usuario.

## Inicio rapido

```bash
cd equipe-lp-whatsapp
claude
```

Descreva o projeto da LP que deseja criar. Os agentes sao invocados automaticamente na sequencia correta.

## Estrutura

```
equipe-lp-whatsapp/
├── CLAUDE.md                  — contexto principal lido pelo Claude Code
├── 00-briefing.md             — definicao do problema e escopo
├── 01-architecture.md         — decisao tecnica e justificativa
├── 02-team.md                 — composicao e fluxo da equipe
├── .claude/
│   ├── agents/                — equipe de 6 agentes especialistas
│   │   ├── briefing-lp.md
│   │   ├── planner-lp.md
│   │   ├── copy-lp.md
│   │   ├── builder-lp.md
│   │   ├── integrator-lp.md
│   │   └── reviewer-lp.md
│   └── skills/
│       └── frontend-design    — skill de design ativada pelo builder-lp
└── outputs/
    └── [slug-cliente]/        — LP gerada para cada cliente
        ├── briefing.md
        ├── plan.md
        ├── copy.md
        ├── sections.html
        ├── index.html         — arquivo final para entregar ao cliente
        └── review.md
```

## Equipe

| Agente | Descricao |
|---|---|
| briefing-lp | Conduz entrevista estrategica e produz briefing.md estruturado |
| planner-lp | Define estrutura de secoes e ordem narrativa da LP em plan.md |
| copy-lp | Escreve todos os textos com limites de caracteres em copy.md |
| builder-lp | Constroi blocos HTML/Tailwind com identidade visual em sections.html |
| integrator-lp | Monta index.html final com Tailwind CDN, Google Fonts e componente WhatsApp parametrizado |
| reviewer-lp | Executa checklist tecnico e visual e emite veredicto em review.md |

## Fluxo resumido

```
briefing-lp → [APROVACAO HUMANA] → planner-lp → copy-lp → builder-lp → integrator-lp → reviewer-lp → [ENTREGA ou CORRECAO]
```

## Custo estimado

- Infraestrutura: R$ 0
- Por LP gerada: aproximadamente R$ 0,50 a R$ 2,00 em tokens
- Total fixo mensal: R$ 0
