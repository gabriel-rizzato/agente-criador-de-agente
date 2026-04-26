# Arquitetura — equipe-lp-whatsapp

## Resumo executivo

Equipe de 6 agentes Claude que opera inteiramente dentro do Claude Agent SDK para produzir, a cada acionamento, um único arquivo `index.html` — responsivo, pronto para entregar ao cliente. O arquivo segue a stack HTML + Tailwind CDN + JS vanilla, reutilizando o componente WhatsApp já validado em produção. A skill `frontend-design` está instalada no projeto e guia o agente `builder-lp` a produzir interfaces visualmente distintivas, evitando estética genérica de IA.

## Alternativas consideradas

### Opção A — Arquivo único gerado em sequência por agentes especializados (RECOMENDADA)
- **Prós**: output final é um arquivo só; cada agente tem escopo delimitado; fácil de revisar e corrigir por seção; permite especialização de qualidade por responsabilidade
- **Contras**: o agente integrador precisa montar a estrutura HTML outer e costurar as partes
- **Custo estimado**: R$ 0 de infraestrutura; ~R$ 0,50–2,00 por LP em tokens

### Opção B — Agente único que gera o arquivo inteiro
- **Prós**: mais simples de orquestrar
- **Contras**: viola divisão de responsabilidades; perde qualidade nas seções do meio; impossível especializar prompts por função; sem "equipe"
- **Custo estimado**: mesmos tokens, qualidade inferior

## ✅ Recomendação: Opção A

**Por quê:** O briefing define explicitamente uma equipe de agentes com output único. A Opção A honra os dois: cada agente é especialista em sua peça, e o integrador costura tudo. A skill `frontend-design` amplifica a qualidade do `builder-lp`, garantindo que cada LP tenha identidade visual própria — não estética genérica.

## Componentes da solução

| Camada | Tecnologia / Agente | Função |
|---|---|---|
| Coleta de briefing | `briefing-lp` | Entrevista estratégica; produz `briefing.md` estruturado |
| Planejamento de seções | `planner-lp` | Decide quais seções a LP precisa e em que ordem; produz `plan.md` |
| Geração de copy | `copy-lp` | Escreve todos os textos (headline, CTAs, bullets) com limite de caracteres por elemento |
| Construção HTML | `builder-lp` | Traduz plano + copy em HTML/Tailwind; usa a skill `frontend-design` para escolhas visuais distintivas |
| Integração final | `integrator-lp` | Monta o `index.html` completo; injeta o componente WA parametrizado |
| Revisão | `reviewer-lp` | Valida HTML, número WA, responsividade, CTAs e critérios de qualidade visual da skill |

## Skill de design

A skill `frontend-design` está instalada em `.claude/skills/frontend-design` (via `.agents/skills/frontend-design`). Ela é ativada automaticamente quando o `builder-lp` constrói a LP e impõe:

- **Tipografia**: fontes com caráter — nunca Inter, Roboto, Arial ou fontes genéricas
- **Cores**: paleta coesa via CSS variables; dominantes com acentos fortes
- **Motion**: animações de alto impacto, scroll-trigger, micro-interações estratégicas
- **Composição**: assimetria, sobreposição, layouts inesperados, espaçamento generoso
- **Identidade**: nenhuma LP deve ter a mesma estética — variação intencional entre projetos

## Fluxo técnico

```
Usuário fornece briefing do projeto
        |
        v
[briefing-lp] ──► briefing.md
        |
        v
[planner-lp] ──► plan.md  (seções + tipo de LP)
        |
        v
[copy-lp] ──► copy.md  (todos os textos por seção, com limites de caracteres)
        |
        v
[builder-lp + skill frontend-design] ──► seções HTML com identidade visual
        |
        v
[integrator-lp]
  ├─ monta <head> (Tailwind CDN, Google Fonts, meta tags)
  ├─ injeta seções na ordem do plan.md
  ├─ copia bloco WA de whatsapp-button_v2.html
  │    └─ substitui: número, textos do modal, opções do select
  └─ fecha </body></html>
        |
        v
[reviewer-lp] ──► checklist técnico + checklist de qualidade visual
        |
        v
index.html ◄── entrega ao usuário
```

## Reutilização do componente WhatsApp

O componente `whatsapp-button_v2.html` é tratado como template parametrizável. O `integrator-lp` substitui:

| Parâmetro | Origem |
|---|---|
| `WHATSAPP_NUMBER` | briefing (número do cliente) |
| Título do modal | briefing (nome do profissional/empresa) |
| Subtítulo do modal | briefing (nicho/oferta) |
| Opções do select | briefing (serviços oferecidos) |
| Texto do tooltip desktop | briefing |
| Texto pré-preenchido WA | briefing |

Cores, animações, validações e máscara de telefone permanecem idênticos ao original.

## Gestão de imagens

1. **URL pública disponível**: usada diretamente com `loading="lazy"` e `alt` adequado
2. **Placeholder**: `https://placehold.co/[W]x[H]` com cor da paleta do cliente
3. **Fundo hero**: via classe Tailwind `bg-[url('...')]` ou `style` inline

## Integrações externas

- Tailwind CSS CDN — estilização
- Google Fonts CDN — tipografia escolhida pela skill/briefing
- WhatsApp API (`wa.me`) — redirect ao submit do modal
- Placehold.co — placeholders durante desenvolvimento

## Estimativa de custo mensal

- Infraestrutura: R$ 0
- Build/deploy: R$ 0
- APIs externas: R$ 0
- Tokens por LP gerada: ~R$ 0,50 a R$ 2,00
- **Total fixo mensal: R$ 0**

## Riscos e mitigações

- **builder-lp gera tags estruturais duplicadas** → gera só conteúdo interno de cada seção; `integrator-lp` monta o outer
- **substituição incompleta no template WA** → `reviewer-lp` verifica se há texto hardcoded do projeto de referência (ex: "Dr. Flávio")
- **copy muito longo para o layout** → `copy-lp` recebe limites de caracteres por elemento (headline ≤ 80 chars, bullet ≤ 120 chars)
- **imagem com URL privada ou expirada** → `briefing-lp` alerta e solicita URLs públicas; usa placeholder se indisponível
