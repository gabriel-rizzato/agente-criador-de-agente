# Configuração — equipe-lp-whatsapp

Referências externas centralizadas. Agentes devem ler este arquivo em vez de usar caminhos hardcoded.

## LP de referência

- **Arquivo principal**: `c:\Users\Samsung\Desktop\projetos_desenvolvidos\github_projetos\site-drflaviomadeira\index.html`
- **Componente WhatsApp**: `c:\Users\Samsung\Desktop\projetos_desenvolvidos\github_projetos\site-drflaviomadeira\botao_wpp\whatsapp-button_v2.html`
- **Tokens de design**: `c:\Users\Samsung\Desktop\projetos_desenvolvidos\github_projetos\site-drflaviomadeira\DESIGN.md`

## Skill de design

- **Nome**: frontend-design
- **Localização**: `.claude/skills/frontend-design` (symlink de `.agents/skills/frontend-design`)
- **Quando usar**: sempre que o builder-lp estiver construindo seções HTML

## Padrões obrigatórios (herdados da LP de referência)

- Stack: HTML semântico + Tailwind CSS CDN + JavaScript vanilla inline
- Animações: classes `.reveal`, `.reveal-left`, `.reveal-right` + Intersection Observer
- Delays: `.reveal-delay-1` (110ms), `.reveal-delay-2` (220ms), `.reveal-delay-3` (330ms), `.reveal-delay-4` (440ms)
- Modal WA: backdrop blur, formulário com nome/telefone/motivo, máscara de telefone, abertura via `wa.me`
- Botão WA flutuante: `fixed bottom-5 right-5`, `animate-ping` + `animate-pulse`, tooltip desktop

## Output de cada LP gerada

Cada LP fica em: `outputs/equipe-lp-whatsapp/[slug-cliente]/`

```
[slug-cliente]/
├── briefing.md       ← briefing-lp
├── plan.md           ← planner-lp
├── copy.md           ← copy-lp
├── sections.html     ← builder-lp
├── index.html        ← integrator-lp
└── review.md         ← reviewer-lp
```
