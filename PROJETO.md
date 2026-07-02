# Casos Esquecidos — Documentação do Projeto
> Arquivo de referência para manutenção contínua com Claude.
> Atualizar sempre que houver mudança estrutural relevante.

---

## Identidade

- **Nome do site:** Casos Esquecidos
- **Autor / pseudônimo:** D. Broch
- **Domínio:** casosesquecidos.com.br
- **Objetivo:** Divulgar o livro na Amazon, publicar contos semanais gratuitos, receber doações via Pix

---

## Acesso e Infraestrutura

| Recurso | Detalhe |
|---|---|
| Hospedagem | GitHub Pages (gratuito) |
| Repositório | `davidbrochini-web/casosesquecidos-site` |
| GitHub username | `davidbrochini-web` |
| Domínio registrado em | Registro.br |
| SSL | Automático via GitHub Pages (Enforce HTTPS ativado) |
| Deploy | Push direto na branch `main` → publicado em ~2 min |

### Token GitHub (para Claude fazer push)
- Tipo: Fine-grained personal access token
- Escopo: somente repositório `casosesquecidos-site`
- Permissões: Contents (read/write) + Metadata (read)
- **Gerar novo token em:** GitHub → Settings → Developer settings → Fine-grained tokens
- O token expira ou é revogado? Gerar um novo e colar na conversa com Claude

### DNS (configurado no Registro.br)
```
A     @    185.199.108.153
A     @    185.199.109.153
A     @    185.199.110.153
A     @    185.199.111.153
CNAME www  davidbrochini-web.github.io
```

---

## Estrutura de Arquivos

```
casosesquecidos-site/
├── index.html              ← Home principal
├── contos.html             ← Listagem completa de contos
├── sitemap.xml             ← Mapa do site para Google
├── robots.txt              ← Permissões para crawlers
├── CNAME                   ← casosesquecidos.com.br (gerado pelo GitHub)
├── PROJETO.md              ← Este arquivo
├── contos/
│   ├── o-portal-de-pedra-negra.html   ← Caso Nº 001
│   ├── o-apartamento-7.html           ← Caso Nº 002
│   ├── a-entrega.html                 ← Caso Nº 003
│   └── o-grupo.html                   ← Caso Nº 004
└── assets/
    ├── style.css           ← Folha de estilo compartilhada (todas as páginas)
    ├── capa.jpg            ← Capa do livro (1024x1536px)
    ├── pix-qrcode.png      ← QR Code Pix estático
    ├── bg/                 ← Imagens de fundo das seções
    │   ├── universo-cult.jpg
    │   ├── livro-desk.jpg
    │   ├── contos-grave.jpg
    │   └── apoio-door.jpg
    └── contos/             ← Imagens ilustrativas de cada conto (banner 1600x700px)
        ├── conto-001-o-portal-de-pedra-negra.jpg
        ├── conto-002-o-apartamento-7.jpg
        └── conto-003-a-entrega.jpg
```

---

## Design System

### Paleta de cores (variáveis CSS em `style.css`)
| Variável | Hex | Uso |
|---|---|---|
| `--bg` | `#0b0a08` | Fundo principal |
| `--bg-panel` | `#15120e` | Cards e painéis |
| `--gold` | `#cdb077` | Destaques, links |
| `--blood` | `#9c2b2b` | Botão primário, acento |
| `--blood-bright` | `#c43a3a` | Hover, número dos casos |
| `--paper` | `#e8dfc8` | Texto principal |
| `--paper-dim` | `#b7ad94` | Texto secundário |
| `--muted` | `#6f6858` | Texto terciário, metadados |
| `--line` | `#322c22` | Bordas e divisores |

### Tipografia (Google Fonts)
- **Display / títulos:** Cinzel (500, 600, 700)
- **Corpo / leitura:** EB Garamond (400, italic, 500)
- **Mono / UI:** JetBrains Mono (400, 500)

### Conceito visual
Estética de "ficha de investigação / arquivo de caso". Fundo escuro, luz âmbar, textura de carvão. Sem gore explícito — atmosfera em vez de susto. Imagens geradas via ChatGPT com estilo: dark oil painting, charcoal texture, amber and deep green tones, atmospheric horror, no gore, cinematic composition.

---

## Conteúdo

### O Livro
- **Título:** Alguns Casos Devem Ficar Esquecidos
- **Link Amazon:** https://www.amazon.com.br/dp/B0F6D1LXSV
- **Casos no livro:** 11 (001 a 011)

### Contos publicados no site
| Nº | Título | Arquivo | Imagem |
|---|---|---|---|
| 001 | O Portal de Pedra Negra | `o-portal-de-pedra-negra.html` | ✅ |
| 002 | O Apartamento 7 | `o-apartamento-7.html` | ✅ |
| 003 | A Entrega | `a-entrega.html` | ✅ |
| 004 | O Grupo | `o-grupo.html` | ❌ aguardando imagem |

### Apoio / Doação
- **Pix (chave):** david.brochini@gmail.com
- **QR Code:** arquivo `assets/pix-qrcode.png` (Pix estático, sem valor fixo)

---

## Como publicar um novo conto

1. Receber o arquivo `.md` ou `.pdf` do conto do autor
2. Criar `contos/nome-do-conto.html` baseado no template dos contos existentes
3. Adicionar card na `contos.html` (desbloquear o caso "Selado" atual e criar o próximo "Selado")
4. Atualizar os 2 cards de destaque na `index.html` (sempre mostrar os 2 mais recentes)
5. Adicionar entrada no `sitemap.xml`
6. Se houver imagem: otimizar em 1600x700px JPEG, salvar em `assets/contos/conto-00X-nome.html`
7. Commit e push para `main`

### Template de commit
```
Publica Caso 00X: [Título do Conto]
```

---

## SEO

- **Sitemap:** `https://casosesquecidos.com.br/sitemap.xml`
- **Robots.txt:** permite todos os crawlers (Google, IAs)
- **Schema.org:** WebSite + Book na home; ShortStory em cada conto
- **Open Graph:** configurado em todas as páginas (preview no WhatsApp/Instagram)
- **Canonical:** configurado em todas as páginas
- **Google Search Console:** a configurar (submeter sitemap após primeira sessão)
- **Google Analytics:** a configurar

---

## Decisões técnicas relevantes

- **Sem backend por enquanto:** site 100% estático. Quando passar de ~30-50 contos, migrar para VPS com banco de dados (PostgreSQL). Conteúdo vira tabela `contos`, site vira aplicação Node.js ou PHP.
- **Sem sistema de assinatura ainda:** modelo atual é contos grátis + doação Pix + venda do livro na Amazon. Ghost CMS pode entrar no futuro para assinantes pagos.
- **CSS paths de background-image** são relativos ao arquivo CSS (`bg/` não `assets/bg/`).
- **Imagens grandes:** usar Python `Pillow` para otimizar antes de subir. Máximo recomendado: 200KB por imagem de fundo, 150KB por banner de conto.
- **Push no GitHub:** sempre usar `git pull --rebase` antes de `git push` para evitar conflito com commits automáticos do GitHub (CNAME, etc).

---

## Histórico de versões relevantes

| Data | O que foi feito |
|---|---|
| Jun 2026 | Site criado do zero, GitHub Pages, DNS configurado |
| Jun 2026 | SSL ativado (Enforce HTTPS) |
| Jun 2026 | SEO completo: Open Graph, Schema.org, sitemap, robots.txt |
| Jun 2026 | Imagens de fundo por seção, cards de contos com foto |
| Jun 2026 | Mobile-first: header responsivo, espaçamentos adaptados |
| Jun 2026 | Barra de anúncio no topo ("contos grátis toda semana") |
| Jun 2026 | Seção do livro corrigida para 11 casos reais |
| Jun 2026 | Limpeza de CSS morto (66 linhas removidas) |
