# Fluidz Skills

**Skills de GTM para [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) — by [Fluidz](https://fluidz.com.br)**

Repositório com 124 skills prontas para uso em vendas, marketing, inteligência competitiva, SEO, prospecção e geração de leads. Cada skill é um conjunto de instruções que o Claude Code segue para executar tarefas específicas de Go-To-Market.

---

## O que é uma Skill?

Uma skill é um arquivo `SKILL.md` com instruções detalhadas que o Claude Code utiliza como referência para executar uma tarefa. Funciona como um "manual de instruções" que ensina o Claude Code a realizar atividades específicas — como scraping de anúncios, prospecção de leads, análise de concorrentes, etc.

Existem 3 tipos de skills:

- **Capabilities** (54) — ferramentas atômicas, de propósito único (ex: scraping do Reddit, extração de voz de marca)
- **Composites** (61) — cadeias de múltiplas skills combinadas (ex: pesquisa de concorrente + geração de battlecard)
- **Playbooks** (9) — workflows completos de ponta a ponta (ex: pipeline inteiro de prospecção outbound)

---

## Pré-requisitos

- **Node.js** versão 18 ou superior — [download aqui](https://nodejs.org/)
- **Claude Code** instalado e configurado — [documentação oficial](https://docs.anthropic.com/en/docs/claude-code/overview)

Para verificar se o Node.js está instalado:

```bash
node --version
# Deve retornar v18.x.x ou superior
```

---

## Instalação rápida

```bash
npx github:edupegoretti/fluidz-skills install <slug>
```

Onde `<slug>` é o identificador da skill que você quer instalar. Por exemplo:

```bash
npx github:edupegoretti/fluidz-skills install reddit-scraper
npx github:edupegoretti/fluidz-skills install battlecard-generator
npx github:edupegoretti/fluidz-skills install cold-email-outreach
```

Isso baixa os arquivos da skill para `~/.claude/skills/<slug>/` (destino padrão para Claude Code).

---

## Plataformas suportadas

O CLI suporta 3 plataformas. Use **uma** flag por comando:

```bash
# Claude Code (padrão — não precisa da flag)
npx github:edupegoretti/fluidz-skills install google-ad-scraper

# Claude Code + Codex
npx github:edupegoretti/fluidz-skills install google-ad-scraper --codex

# Claude Code + Cursor (requer --project-dir)
npx github:edupegoretti/fluidz-skills install google-ad-scraper --cursor --project-dir /caminho/do/projeto
```

O que cada flag faz:

| Flag | Onde instala | Observação |
|------|-------------|------------|
| `--claude` (padrão) | `~/.claude/skills/<slug>/` | Nenhuma flag necessária |
| `--codex` | `~/.claude/skills/<slug>/` + copia para `~/.codex/skills/<slug>/` | — |
| `--cursor` | `~/.claude/skills/<slug>/` + cria regra em `.cursor/rules/fluidz-<slug>.mdc` | Requer `--project-dir` |

Regras:
- Somente **uma** flag de plataforma por comando
- A flag `--cursor` exige obrigatoriamente o `--project-dir`

---

## Todos os comandos do CLI

```bash
# Listar todas as 124 skills disponíveis
npx github:edupegoretti/fluidz-skills list

# Instalar uma skill (padrão: Claude Code)
npx github:edupegoretti/fluidz-skills install <slug>

# Instalar para Codex
npx github:edupegoretti/fluidz-skills install <slug> --codex

# Instalar para Cursor
npx github:edupegoretti/fluidz-skills install <slug> --cursor --project-dir /caminho/do/projeto

# Ver detalhes de uma skill (descrição, tags, arquivos)
npx github:edupegoretti/fluidz-skills info <slug>
```

---

## Como usar após a instalação

Depois de instalar uma skill, copie o `SKILL.md` para o diretório de skills do seu projeto:

```bash
mkdir -p .claude/skills
cp ~/.claude/skills/<slug>/SKILL.md .claude/skills/<slug>.md
```

A partir daí, o Claude Code vai reconhecer a skill e seguir as instruções contidas no `SKILL.md` quando você referenciar aquela skill na conversa.

Exemplo prático completo:

```bash
# 1. Instale a skill de scraping do Reddit
npx github:edupegoretti/fluidz-skills install reddit-scraper

# 2. Copie para o seu projeto
mkdir -p .claude/skills
cp ~/.claude/skills/reddit-scraper/SKILL.md .claude/skills/reddit-scraper.md

# 3. No Claude Code, peça para usar a skill
# "Use a skill reddit-scraper para buscar posts sobre IA no r/artificial"
```

---

## Skills disponíveis (124)

### Ads (12)
| Skill | Tipo | Descrição |
|-------|------|-----------|
| `ad-angle-miner` | Comp | Minera ângulos de anúncios que convertem a partir de reviews, Reddit e ads de concorrentes |
| `ad-campaign-analyzer` | Comp | Analisa performance de campanhas de ads (Google, Meta, LinkedIn) |
| `ad-creative-intelligence` | Comp | Scraping de ads de concorrentes, clustering por hook/ângulo/formato |
| `ad-spend-allocator` | Comp | Recomendação de realocação de budget entre canais pagos |
| `ad-to-landing-page-auditor` | Comp | Auditoria de consistência entre anúncio e landing page |
| `competitor-ad-teardown` | Comp | Análise profunda da estratégia de ads do concorrente |
| `google-ad-scraper` | Cap | Scraping do Google Ads Transparency Center |
| `google-search-ads-builder` | Comp | Construtor completo de campanha Google Search Ads |
| `meta-ad-scraper` | Cap | Scraping da Meta Ad Library (Facebook, Instagram) |
| `meta-ads-campaign-builder` | Comp | Construtor completo de campanha Meta Ads |
| `paid-channel-prioritizer` | Comp | Recomendação de quais canais pagos priorizar |
| `trending-ad-hook-spotter` | Comp | Monitora redes sociais para detectar narrativas tendência para hooks de ads |

### Brand (4)
| Skill | Tipo | Descrição |
|-------|------|-----------|
| `brand-voice-extractor` | Cap | Extrai tom e estilo a partir de conteúdo publicado |
| `launch-positioning-builder` | Comp | Pesquisa concorrentes e gera documento de posicionamento |
| `messaging-ab-tester` | Comp | Gera variantes de mensagem e deploy como testes A/B no LinkedIn/email |
| `visual-brand-extractor` | Cap | Extrai branding visual (cores, fontes, layout) |

### Inteligência Competitiva (11)
| Skill | Tipo | Descrição |
|-------|------|-----------|
| `battlecard-generator` | Comp | Pesquisa concorrente e produz battlecard estruturado para vendas |
| `company-current-gtm-analysis` | Comp | Scoring completo de GTM com mapa de oportunidades |
| `competitive-pricing-intel` | Comp | Monitora páginas de preços de concorrentes e mudanças |
| `competitive-strategy-tracker` | Comp | Sistema vivo de estratégia competitiva com perfis persistentes |
| `competitor-content-tracker` | Comp | Monitora conteúdo de concorrentes em blogs, LinkedIn e Twitter |
| `competitor-intel` | Comp | Tracking de concorrentes em múltiplas fontes |
| `competitor-monitoring-system` | Play | Monta sistema contínuo de monitoramento competitivo |
| `industry-scanner` | Comp | Briefing diário de inteligência da indústria |
| `seo-domain-analyzer` | Cap | Métricas de SEO do domínio via Semrush/Ahrefs |
| `seo-traffic-analyzer` | Cap | Análise de tráfego e palavras-chave do site |
| `tech-stack-teardown` | Cap | Engenharia reversa do stack de vendas/marketing de uma empresa |

### Conteúdo (17)
| Skill | Tipo | Descrição |
|-------|------|-----------|
| `blog-scraper` | Cap | Scraping de blogs via RSS com fallback Apify |
| `campaign-brief-generator` | Comp | Geração de brief completo de campanha de marketing |
| `client-package-local` | Play | Empacota trabalho do cliente em entrega local (filesystem) |
| `client-package-notion` | Play | Empacota trabalho do cliente em páginas Notion compartilháveis |
| `client-packet-engine` | Play | Gerador de pacotes de cliente em lote |
| `content-asset-creator` | Cap | Gera relatórios e páginas HTML com branding |
| `content-brief-factory` | Comp | Briefs de conteúdo detalhados em escala com análise de SERP |
| `content-repurposer` | Comp | Gera 10+ peças derivadas a partir de conteúdo longo |
| `create-html-carousel` | Cap | Cria carrosséis para LinkedIn como imagens PNG |
| `create-html-slides` | Cap | Cria apresentações HTML com animações |
| `create-workflow-diagram` | Cap | Cria diagramas de workflow estilo FigJam/Miro como PNGs |
| `customer-story-builder` | Comp | Gera case studies estruturados a partir de inputs brutos |
| `feature-launch-playbook` | Comp | Gera kit completo de lançamento a partir de uma feature/update |
| `help-center-article-generator` | Comp | Gera artigos estruturados para central de ajuda |
| `qbr-deck-builder` | Comp | Monta outline de QBR deck a partir de dados do cliente |
| `site-content-catalog` | Cap | Inventário completo do conteúdo de um site |
| `youtube-watcher` | Cap | Extração de transcrições do YouTube via yt-dlp |

### Geração de Leads (22)
| Skill | Tipo | Descrição |
|-------|------|-----------|
| `apollo-lead-finder` | Cap | Prospecção em duas fases no Apollo.io com enriquecimento |
| `champion-tracker` | Cap | Rastreia champions de produto para mudanças de emprego |
| `competitor-post-engagers` | Cap | Encontra leads a partir de quem engaja em posts de concorrentes no LinkedIn |
| `conference-speaker-scraper` | Cap | Extrai palestrantes de sites de conferências |
| `contact-cache` | Cap | Banco de contatos em CSV com deduplicação |
| `crustdata-supabase` | Cap | CrustData People Search com dedup via Supabase |
| `event-prospecting-pipeline` | Play | Pipeline completo de prospecção a partir de eventos |
| `expansion-signal-spotter` | Comp | Monitora contas para sinais de upsell/cross-sell |
| `funding-signal-monitor` | Comp | Monitora anúncios de funding (Series A-C) |
| `get-qualified-leads-from-luma` | Comp | Prospecção completa de leads a partir de eventos Luma |
| `inbound-lead-enrichment` | Comp | Enriquece dados faltantes de leads inbound |
| `inbound-lead-qualification` | Comp | Qualifica leads inbound contra critérios de ICP |
| `inbound-lead-triage` | Comp | Triagem de todos os leads inbound de um período |
| `job-posting-intent` | Cap | Detecta intenção de compra a partir de vagas de emprego |
| `kol-engager-icp` | Cap | Encontra leads ICP-fit a partir de audiências de KOLs no LinkedIn |
| `lead-qualification` | Cap | Engine de qualificação de leads com intake conversacional |
| `linkedin-job-scraper` | Cap | Scraping de vagas do LinkedIn via python-jobspy |
| `luma-event-attendees` | Cap | Scraping de listas de participantes de eventos Luma |
| `pain-language-engagers` | Cap | Encontra leads a partir de posts com linguagem de dor no LinkedIn |
| `signal-detection-pipeline` | Play | Detecta sinais de compra, qualifica leads e gera outreach |
| `signal-scanner` | Cap | Detecta sinais de compra em empresas do TAM |
| `tam-builder` | Cap | Constrói TAM com scoring usando Apollo + Supabase |

### Monitoramento (11)
| Skill | Tipo | Descrição |
|-------|------|-----------|
| `hacker-news-scraper` | Cap | Busca stories/comentários no HN via Algolia API |
| `kol-content-monitor` | Comp | Rastreia posts de KOLs no LinkedIn e Twitter/X |
| `newsletter-monitor` | Comp | Monitora inbox AgentMail para sinais em newsletters |
| `newsletter-signal-scanner` | Comp | Assina e monitora newsletters da indústria |
| `newsletter-sponsorship-finder` | Cap | Encontra newsletters para oportunidades de patrocínio |
| `product-hunt-scraper` | Cap | Scraping de lançamentos trending no Product Hunt |
| `reddit-scraper` | Cap | Scraping de posts do Reddit por keyword, subreddit ou período |
| `review-scraper` | Cap | Scraping de reviews do G2, Capterra e Trustpilot |
| `sponsored-newsletter-finder` | Comp | Descobre newsletters para oportunidades de patrocínio |
| `twitter-scraper` | Cap | Busca posts no Twitter/X com filtragem por data |
| `web-archive-scraper` | Cap | Scraping do Wayback Machine para sites arquivados |

### Outreach (20)
| Skill | Tipo | Descrição |
|-------|------|-----------|
| `agentmail` | Cap | Plataforma de email API-first para agentes de IA |
| `champion-move-outreach` | Comp | Outreach ativado por mudança de emprego de champion |
| `cold-email-outreach` | Cap | Orquestração completa de cold email outreach |
| `customer-win-back-sequencer` | Comp | Pesquisa contas churned e gera sequências de win-back |
| `disqualification-handling` | Comp | Tratamento de leads desqualificados ou quase-fit |
| `early-access-email-sequence` | Cap | Sequência de 7 emails de onboarding personalizada |
| `email-drafting` | Cap | Escrita de cold email com frameworks e personalização |
| `find-influencers` | Cap | Encontra influenciadores do TikTok via Apify |
| `funding-signal-outreach` | Comp | Detecção de sinal de funding + outreach |
| `hiring-signal-outreach` | Comp | Detecção de sinal de contratação + outreach |
| `kol-discovery` | Cap | Encontra KOLs via pesquisa web + LinkedIn |
| `leadership-change-outreach` | Comp | Sinal de mudança de liderança + outreach |
| `linkedin-commenter-extractor` | Cap | Extrai comentadores de posts do LinkedIn |
| `linkedin-influencer-discovery` | Cap | Encontra thought leaders no LinkedIn em qualquer área |
| `linkedin-outreach` | Cap | Construtor completo de campanha de outreach no LinkedIn |
| `linkedin-post-research` | Cap | Pesquisa posts do LinkedIn por keyword |
| `linkedin-profile-post-scraper` | Cap | Scraping de posts recentes de perfis do LinkedIn |
| `news-signal-outreach` | Comp | Outreach ativado por sinal de notícia |
| `outbound-prospecting-engine` | Play | Engine completa de prospecção outbound |
| `setup-outreach-campaign` | Cap | Configuração de campanha outbound no Smartlead |

### Pesquisa (17)
| Skill | Tipo | Descrição |
|-------|------|-----------|
| `brainstorming-partner` | Cap | Frameworks estruturados de brainstorming |
| `churn-risk-detector` | Comp | Detecta indicadores de churn e produz scorecard de risco |
| `client-onboarding` | Play | Onboarding completo: inteligência + estratégia |
| `gcalcli-calendar` | Cap | Gestão de Google Calendar via gcalcli |
| `icp-identification` | Cap | Pesquisa empresa, define ICP e roteia para próximo passo |
| `icp-persona-builder` | Cap | Constrói personas sintéticas de comprador ICP |
| `icp-website-audit` | Comp | Auditoria completa de website pelos olhos do ICP |
| `icp-website-review` | Cap | Avalia um website pela perspectiva do ICP |
| `meeting-brief` | Comp | Preparação diária de reuniões com pesquisa profunda de participantes |
| `pipeline-review` | Comp | Análise de pipeline a partir de dados de CRM |
| `review-intelligence-digest` | Comp | Scraping de reviews + extração de temas e provas sociais |
| `sales-call-prep` | Comp | Inteligência pré-call de vendas |
| `sales-coaching` | Comp | Coach de vendas com IA analisando todos os dados de vendas |
| `sales-performance-review` | Comp | Review periódico de performance de vendas |
| `sequence-performance` | Comp | Review de performance de sequências/campanhas de email |
| `voice-of-customer-synthesizer` | Comp | Agrega feedback de clientes em relatório VoC unificado |
| `youtube-apify-transcript` | Cap | Extração de transcrições do YouTube via Apify API |

### SEO (10)
| Skill | Tipo | Descrição |
|-------|------|-----------|
| `aeo-visibility` | Cap | Teste de visibilidade em AI answer engines |
| `aeo-visibility-monitor` | Comp | Checks recorrentes de AEO no ChatGPT, Perplexity e Gemini |
| `programmatic-seo-planner` | Comp | Identifica padrões de páginas de SEO programático que vale construir |
| `programmatic-seo-spy` | Comp | Engenharia reversa do SEO programático de concorrentes |
| `search-ad-keyword-architect` | Comp | Pesquisa profunda de keywords para paid search |
| `seo-content-audit` | Comp | Auditoria completa de SEO: inventário de conteúdo + métricas + gaps |
| `seo-content-engine` | Play | Monta e opera um motor de conteúdo SEO |
| `seo-opportunity-finder` | Comp | Encontra oportunidades quick-win de conteúdo SEO |
| `serp-feature-sniper` | Comp | Analisa features da SERP e produz conteúdo otimizado |
| `topical-authority-mapper` | Comp | Mapeia clusters de tópicos completos com arquitetura hub/spoke |

---

## Estrutura de uma skill

Cada skill é uma pasta dentro de `skills/<categoria>/<slug>/` contendo:

```
skills/capabilities/reddit-scraper/
├── SKILL.md           # Instruções que o Claude Code segue
└── skill.meta.json    # Metadados (slug, categoria, tags, comando de instalação)
```

Exemplo de `skill.meta.json`:

```json
{
  "slug": "reddit-scraper",
  "category": "capabilities",
  "tags": ["monitoring"],
  "installation": {
    "base_command": "npx github:edupegoretti/fluidz-skills install reddit-scraper",
    "supports": ["claude", "cursor", "codex"]
  }
}
```

As 3 categorias:

| Categoria | Pasta | Quantidade | O que é |
|-----------|-------|------------|---------|
| Capabilities | `skills/capabilities/` | 54 | Ferramentas atômicas de propósito único |
| Composites | `skills/composites/` | 61 | Cadeias que combinam múltiplas capabilities |
| Playbooks | `skills/playbooks/` | 9 | Workflows completos de ponta a ponta |

---

## Desenvolvimento local

Se você quer contribuir ou testar localmente:

```bash
# 1. Clone o repositório
git clone https://github.com/edupegoretti/fluidz-skills.git
cd fluidz-skills

# 2. Instale as dependências
npm install

# 3. Valide que todas as skills estão corretas (SKILL.md + skill.meta.json)
node scripts/validate-skills.js

# 4. Reconstrua o índice de skills
node scripts/build-index.js

# 5. Rode os testes
npm test

# 6. Teste o CLI localmente
node bin/fluidz-skills.js list
node bin/fluidz-skills.js info reddit-scraper
node bin/fluidz-skills.js install reddit-scraper
```

Para rodar tudo de uma vez:

```bash
npm run ci
# Equivale a: validate-skills → build-index → test
```

---

## Criando uma nova skill

1. Crie a pasta dentro da categoria correta:

```bash
mkdir -p skills/capabilities/minha-nova-skill
```

2. Crie o `SKILL.md` com as instruções que o Claude Code deve seguir.

3. Crie o `skill.meta.json`:

```json
{
  "slug": "minha-nova-skill",
  "category": "capabilities",
  "tags": ["minha-tag"],
  "installation": {
    "base_command": "npx github:edupegoretti/fluidz-skills install minha-nova-skill",
    "supports": ["claude", "cursor", "codex"]
  }
}
```

4. Valide e reconstrua o índice:

```bash
node scripts/validate-skills.js
node scripts/build-index.js
```

5. Teste a instalação:

```bash
node bin/fluidz-skills.js install minha-nova-skill
```

---

## Solução de problemas

**"command not found: npx"**
O Node.js não está instalado ou não está no PATH. Instale em [nodejs.org](https://nodejs.org/).

**"Skill not found"**
O slug digitado não existe. Rode `npx github:edupegoretti/fluidz-skills list` para ver os slugs disponíveis.

**"HTTP 404"**
O índice de skills não foi encontrado. Verifique sua conexão com a internet e se o repositório está público no GitHub.

**"Only one target flag can be used"**
Você usou mais de uma flag (`--claude`, `--codex`, `--cursor`) no mesmo comando. Use apenas uma.

**"Target --cursor requires --project-dir"**
A flag `--cursor` exige que você passe o caminho do projeto com `--project-dir /caminho/do/projeto`.

---

## Licença

MIT — Copyright (c) 2026 Fluidz

---

## Mantido por

[Fluidz](https://fluidz.com.br) — Automação inteligente de GTM

Repositório: [github.com/edupegoretti/fluidz-skills](https://github.com/edupegoretti/fluidz-skills)
