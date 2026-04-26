# Equipe de Agentes — equipe-lp-whatsapp

## Visão geral

O trabalho foi decomposto em 6 responsabilidades distintas que seguem um fluxo linear estrito: coleta, planejamento, escrita, construção visual, montagem e revisão. Cada agente recebe um artefato de texto e entrega outro. A separação é justificada pelo contexto radicalmente diferente de cada etapa: estratégia de negócio (briefing), arquitetura de informação (planner), escrita persuasiva (copy), código HTML com identidade visual (builder), integração técnica (integrator) e auditoria de qualidade (reviewer).

**Total de agentes:** 6

## Tabela de agentes

| # | Nome (kebab-case) | Papel | Input | Output | Modelo sugerido |
|---|---|---|---|---|---|
| 1 | briefing-lp | Entrevistador estratégico | Descrição inicial do usuário | `briefing.md` estruturado | sonnet |
| 2 | planner-lp | Arquiteto de seções | `briefing.md` | `plan.md` com seções, ordem e tipo de LP | sonnet |
| 3 | copy-lp | Redator persuasivo | `briefing.md` + `plan.md` | `copy.md` com todos os textos por seção | sonnet |
| 4 | builder-lp | Construtor HTML/visual | `plan.md` + `copy.md` + skill frontend-design | Seções HTML individuais (`sections.html`) | sonnet |
| 5 | integrator-lp | Montador técnico | `sections.html` + `briefing.md` + template WA | `index.html` completo parametrizado | sonnet |
| 6 | reviewer-lp | Auditor de qualidade | `index.html` + `briefing.md` + `plan.md` | `review.md` com veredicto | haiku |

## Detalhamento de cada agente

### 1. briefing-lp

- **Responsabilidade**: Conduzir entrevista estratégica com o usuário para coletar todos os dados necessários para a LP e ajudá-lo a decidir o tipo ideal quando houver dúvida.
- **Input**: Descrição inicial livre do usuário (via conversa); pode chegar com dados parciais ou completos.
- **Output**: `briefing.md` salvo em `outputs/[projeto-cliente]/briefing.md` com campos padronizados: cliente, nicho, tipo de LP, número WhatsApp, paleta, referências de imagem, serviços/opções do modal.
- **Ferramentas necessárias**: Write
- **Por que existe separadamente**: Contexto de negócio e entrevista — completamente diferente de código ou escrita de copy. O briefing-lp precisa raciocinar sobre qual tipo de LP converte melhor para cada nicho.

### 2. planner-lp

- **Responsabilidade**: Decidir a estrutura da LP — quais seções existem, em que ordem aparecem e qual é a lógica narrativa de cada uma.
- **Input**: `briefing.md` (leitura).
- **Output**: `plan.md` com lista ordenada de seções, objetivo de cada seção (o que o visitante deve sentir/fazer), tipo de componente visual sugerido e estimativa de altura em viewport.
- **Ferramentas necessárias**: Read, Write
- **Por que existe separadamente**: Decisão arquitetural de UX de conversão — requer conhecimento de fluxo narrativo, contexto distinto da escrita de copy ou da construção HTML.

### 3. copy-lp

- **Responsabilidade**: Escrever todos os textos da LP respeitando limites de caracteres por elemento.
- **Input**: `briefing.md` + `plan.md` (leitura de ambos).
- **Output**: `copy.md` com textos organizados por seção, contagem de caracteres ao lado de cada elemento crítico (headline ≤ 80 chars, bullet ≤ 120 chars, CTA ≤ 40 chars).
- **Ferramentas necessárias**: Read, Write
- **Por que existe separadamente**: Escrita persuasiva tem voz própria — misturar com construção de HTML faria o builder perder foco em código e o copy perder foco em persuasão.

### 4. builder-lp

- **Responsabilidade**: Traduzir plano e copy em blocos HTML/Tailwind com identidade visual de alta qualidade, sem repetição de estética entre projetos.
- **Input**: `plan.md` + `copy.md` (leitura); skill `frontend-design` ativa para decisões visuais.
- **Output**: `sections.html` contendo apenas o conteúdo interno de cada `<section>` — sem `<html>`, `<head>` ou `<body>`.
- **Ferramentas necessárias**: Read, Write
- **Skill obrigatória**: `frontend-design` — consultada para cada decisão de tipografia, paleta, motion e composição. LP de referência em `c:\Users\Samsung\Desktop\projetos_desenvolvidos\github_projetos\site-drflaviomadeira\index.html`.
- **Por que existe separadamente**: Construção de HTML com identidade visual requer contexto longo de código e decisões de design simultâneas.

### 5. integrator-lp

- **Responsabilidade**: Montar o `index.html` final completo com `<head>` + CDNs + seções + componente WhatsApp parametrizado.
- **Input**: `sections.html` + `briefing.md` + `plan.md` + template WA em `c:\Users\Samsung\Desktop\projetos_desenvolvidos\github_projetos\site-drflaviomadeira\botao_wpp\whatsapp-button_v2.html`.
- **Output**: `index.html` completo, válido, com Tailwind CDN, Google Fonts, meta tags de responsividade, seções na ordem correta e componente WA com dados do cliente substituídos.
- **Ferramentas necessárias**: Read, Write
- **Por que existe separadamente**: Montagem técnica de HTML válido com injeção de componente parametrizado — qualquer erro aqui quebra toda a LP.

### 6. reviewer-lp

- **Responsabilidade**: Executar checklist técnico e visual no `index.html` e emitir veredicto.
- **Input**: `index.html` + `briefing.md` + `plan.md` (leitura dos três).
- **Output**: `review.md` com checklist técnico (número WA, ausência de texto hardcoded do projeto de referência, Tailwind CDN, Google Fonts, meta viewport, botão WA funcional) + checklist visual (tipografia não-genérica, paleta coesa, animação presente, layout não-simétrico em pelo menos uma seção, alt text nas imagens) + veredicto APROVADO ou CORREÇÕES NECESSÁRIAS.
- **Ferramentas necessárias**: Read, Write
- **Por que existe separadamente**: Revisão é tarefa estruturada de checklist — diferente de construção ou escrita. Haiku reduz custo sem perda de qualidade na tarefa classificatória.

## Fluxo de integração

```
Usuário (dados do projeto)
        |
        v
[1. briefing-lp] ──► briefing.md
        |
        v ← APROVAÇÃO HUMANA OBRIGATÓRIA
[2. planner-lp] ──► plan.md
        |
        v (aprovação opcional)
[3. copy-lp] ──► copy.md
        |
        v
[4. builder-lp + skill frontend-design] ──► sections.html
        |
        v
[5. integrator-lp] ──► index.html
        |
        v
[6. reviewer-lp] ──► review.md
        |
        v
APROVADO? ──Sim──► index.html entregue ao usuário
          |
          Não
          |
          v
     [agente responsável pela correção]
          |
          v
     [reviewer-lp novamente]
```

## Pontos de validação humana

- Após briefing-lp: aprovação obrigatória — confirmar que briefing.md capturou os dados corretamente
- Após planner-lp: aprovação opcional — revisar se as seções fazem sentido para o objetivo
- Após reviewer-lp (APROVADO): entrega final ao usuário
- Após reviewer-lp (CORREÇÕES): alerta humano com lista de correções antes de reprocessar

## Tratamento de falhas

- **briefing-lp sem dados suficientes**: nova rodada de perguntas; não avançar com número WA, tipo de LP ou nicho em branco
- **planner-lp com estrutura inconsistente**: retornar ao planner com instrução específica; não passar para copy-lp
- **copy-lp acima dos limites de caracteres**: reinvocar com feedback dos elementos que excedem
- **builder-lp inclui tags estruturais**: integrator-lp faz strip; reviewer-lp valida ausência de duplicatas
- **integrator-lp deixa texto hardcoded do projeto de referência**: reviewer-lp detecta e retorna com lista de substituições
- **reviewer-lp aprova com falhas evidentes**: fallback para aprovação humana obrigatória
