# Agente Criador de Sistemas

> Pipeline de 5 agentes especialistas que transforma uma ideia em um sistema completo de agentes de IA, pronto para uso no Claude Code.

## O que é

Você descreve uma ideia. O sistema:

1. **Discovery** — faz perguntas até a ideia estar madura
2. **Architect** — define a stack técnica econômica
3. **Team Designer** — desenha a equipe de agentes ideal
4. **Agent Builder** (loop) — constrói cada agente da equipe
5. **Integrator** — empacota tudo em uma pasta pronta para uso

No final, você tem uma pasta nova em `outputs/[seu-projeto]/` com `CLAUDE.md` + `.claude/agents/` configurados, que funciona como um projeto Claude Code completo.

## Pré-requisitos

- [Claude Code](https://docs.claude.com/en/docs/claude-code/overview) instalado
- VSCode (ou qualquer editor)
- Conta Anthropic com créditos de API

## Como usar

1. **Abra a pasta no VSCode:**
   ```
   File → Open Folder → ia-agente-criador-sistemas
   ```

2. **Abra o terminal integrado (Ctrl+`) e rode:**
   ```bash
   claude
   ```

3. **Descreva o que você quer construir:**
   ```
   Quero criar um sistema para [...]
   ```

4. **Siga o fluxo:** o orquestrador vai pedir o nome do projeto e ativar o pipeline. Você aprova cada etapa crítica antes de avançar.

5. **Use o projeto gerado:** ao final, navegue até `outputs/[seu-projeto]/` e rode `claude` lá dentro. A equipe específica do projeto novo está pronta.

## Estrutura

```
agente-criador-sistemas/
├── CLAUDE.md                        ← orquestrador do pipeline
├── README.md                        ← este arquivo
├── .claude/
│   └── agents/
│       ├── 1-discovery.md
│       ├── 2-architect.md
│       ├── 3-team-designer.md
│       ├── 4-agent-builder.md
│       └── 5-integrator.md
├── templates/
│   └── agent-template.md            ← molde para o agent-builder
└── outputs/                         ← projetos gerados aparecem aqui
    └── [seu-projeto]/
        ├── CLAUDE.md
        ├── 00-briefing.md
        ├── 01-architecture.md
        ├── 02-team.md
        └── .claude/agents/
            ├── agente-1.md
            └── ...
```

## Pontos de aprovação humana

O pipeline pausa para sua aprovação após:

- ✋ Discovery (briefing)
- ✋ Architect (stack)
- ✋ Team Designer (composição da equipe)

A criação dos agentes (etapa 4) e o empacotamento (etapa 5) rodam automaticamente após a aprovação da equipe.

## Custo aproximado

Um ciclo completo com Sonnet costuma ficar entre **R$ 1,50 e R$ 5** em tokens, dependendo do tamanho do projeto e quantas iterações de aprovação você fizer.

## Versionamento

Recomendado: criar um repositório Git da pasta `agente-criador-sistemas/` e adicionar `outputs/` ao `.gitignore` se preferir versionar cada projeto gerado em seu próprio repositório.

```bash
git init
echo "outputs/" >> .gitignore
git add .
git commit -m "feat: pipeline inicial do agente criador de sistemas"
```

## Personalização

Cada arquivo em `.claude/agents/` é um markdown editável. Para ajustar o comportamento de qualquer etapa, edite o arquivo correspondente. Recomenda-se versionar mudanças com Git para manter histórico.
