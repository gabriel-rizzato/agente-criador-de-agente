# equipe-lp-whatsapp

Equipe de agentes que produz landing pages HTML completas, focadas em conversão para WhatsApp, a partir de um briefing fornecido pelo usuário.

## O que este sistema faz

Recebe um briefing com os dados do cliente (nicho, oferta, número de WhatsApp, paleta de cores, serviços) e produz um único arquivo `index.html` responsivo, com botão WhatsApp flutuante e modal funcionando — pronto para abrir no browser e entregar ao cliente. Todo o processo ocorre dentro de uma sessão de trabalho, sem npm, frameworks ou build process: stack HTML + Tailwind CDN + JS vanilla.

## Equipe de agentes

| # | Nome | Papel |
|---|---|---|
| 1 | briefing-lp | Entrevistador estratégico — conduz coleta de dados do projeto e gera `briefing.md` |
| 2 | planner-lp | Arquiteto de seções — define estrutura, ordem e objetivo de cada seção em `plan.md` |
| 3 | copy-lp | Redator persuasivo — escreve todos os textos da LP com limites de caracteres em `copy.md` |
| 4 | builder-lp | Construtor HTML/visual — traduz plano e copy em blocos HTML/Tailwind em `sections.html` |
| 5 | integrator-lp | Montador técnico — monta o `index.html` final com head, CDNs e componente WhatsApp parametrizado |
| 6 | reviewer-lp | Auditor de qualidade — executa checklist técnico e visual e emite veredicto em `review.md` |

## Fluxo de trabalho

```
Usuário (dados do projeto)
        |
        v
[1. briefing-lp] ──► outputs/[slug-cliente]/briefing.md
        |
        v ← APROVACAO HUMANA OBRIGATORIA
[2. planner-lp] ──► outputs/[slug-cliente]/plan.md
        |
        v (aprovacao opcional)
[3. copy-lp] ──► outputs/[slug-cliente]/copy.md
        |
        v
[4. builder-lp + skill frontend-design] ──► outputs/[slug-cliente]/sections.html
        |
        v
[5. integrator-lp] ──► outputs/[slug-cliente]/index.html
        |
        v
[6. reviewer-lp] ──► outputs/[slug-cliente]/review.md
        |
        v
APROVADO? ──Sim──► index.html entregue ao usuario
          |
          Nao
          |
          v ← APROVACAO HUMANA (alerta de correcoes)
     [agente responsavel pela correcao]
          |
          v
     [reviewer-lp novamente]
```

O `briefing-lp` invoca o `planner-lp` apos aprovacao humana do briefing. O `planner-lp` invoca o `copy-lp`. O `copy-lp` invoca o `builder-lp`. O `builder-lp` invoca o `integrator-lp`. O `integrator-lp` invoca o `reviewer-lp`. O `reviewer-lp` reporta o veredicto ao orquestrador (Claude principal), que decide o proximo passo.

## Como usar

1. Garanta que esta nesta pasta: `cd equipe-lp-whatsapp`
2. Inicie o Claude Code: `claude`
3. Descreva o projeto da LP que deseja criar (nome do cliente, nicho, tipo de pagina). O Claude principal invocara os agentes da equipe automaticamente na sequencia correta.

Cada LP gerada fica salva em `outputs/[slug-cliente]/` dentro deste projeto. Por exemplo, um projeto para "Dra. Ana Nutricao" ficara em `outputs/dra-ana-nutricao/`.

## Pontos de aprovacao humana

1. **Apos briefing-lp**: aprovacao obrigatoria — confirmar que `briefing.md` capturou todos os dados do cliente corretamente antes de avancar para o planejamento de secoes.
2. **Apos reviewer-lp (APROVADO)**: entrega final ao usuario — o `index.html` esta pronto para abrir no browser e enviar ao cliente.
3. **Apos reviewer-lp (CORRECOES NECESSARIAS)**: alerta humano obrigatorio — o orquestrador apresenta a lista de correcoes antes de reprocessar os agentes responsaveis.

## Skill frontend-design

A skill `frontend-design` esta instalada em `.claude/skills/frontend-design` e e ativada automaticamente pelo `builder-lp` antes de qualquer decisao visual. Ela impoe:

- **Tipografia**: fontes com carater via Google Fonts — nunca Inter, Roboto, Arial ou fontes genericas
- **Cores**: paleta coesa via CSS custom properties; dominantes com acentos fortes
- **Motion**: animacoes scroll-trigger, micro-interacoes estrategicas (classe `.reveal`)
- **Composicao**: assimetria, sobreposicao, layouts inesperados, espacamento generoso
- **Identidade**: cada LP tem estetica distinta — variacao intencional entre projetos

## Componente WhatsApp de referencia

O componente base esta em:
`c:\Users\Samsung\Desktop\projetos_desenvolvidos\github_projetos\site-drflaviomadeira\botao_wpp\whatsapp-button_v2.html`

O `integrator-lp` le esse template, substitui todos os dados do projeto de referencia (numero, nome, servicos) pelos dados reais do cliente e injeta o componente parametrizado no `index.html` final. O `reviewer-lp` verifica que nenhum texto do projeto de referencia sobrou no arquivo entregue.

## Restricoes e custos

- Stack: HTML + Tailwind CDN + JS vanilla — sem npm, frameworks ou build process
- Infraestrutura: R$ 0
- Tokens por LP gerada: aproximadamente R$ 0,50 a R$ 2,00
- Total fixo mensal: R$ 0

## Documentacao completa

- `00-briefing.md` — definicao do problema e escopo
- `01-architecture.md` — decisao tecnica e justificativa
- `02-team.md` — composicao e fluxo da equipe
- `.claude/agents/` — agentes especialistas
- `.claude/skills/` — skill frontend-design usada pelo builder-lp
