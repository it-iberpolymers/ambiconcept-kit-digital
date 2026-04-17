# Ambiconcept · Kit Digital

Portal de recursos digitais para distribuidores e parceiros da Ambiconcept Waste Solutions.

---

## Visão Geral

Aplicação web estática (single-page) que centraliza todos os recursos digitais da Ambiconcept, organizada em dois perfis de acesso e quatro categorias de conteúdo.

### Perfis

| Perfil | Descrição |
|--------|-----------|
| **Distribuidor** | Acesso completo — galeria, documentação técnica e comercial, redes sociais |
| **Parceiro** | Municípios e entidades — galeria, documentação técnica (sem logística), redes sociais com foco em campanhas de reciclagem. Sem tab de Documentação Comercial. |

### Categorias

| Categoria | Conteúdo |
|-----------|----------|
| **Galeria de Produto** | Render branco/transparente, render ambiente real, fotografia, vídeos (produto, utilização, manutenção, montagem) |
| **Documentação Técnica** | Ficha técnica, manuais (instalação, utilização, montagem), certificados/ensaios/declarações, ficha de logística (Distribuidor) |
| **Documentação Comercial** | Catálogo Geral 2025 *(Distribuidor only)* |
| **Redes Sociais** | LinkedIn, Instagram, Facebook, TikTok, YouTube, Banners Web — com formatos standard por plataforma |

### Produtos disponíveis

- Contentor 120 L / 240 L / 360 L / 660 L / 1100 L
- Papeleira Urbana
- Ambi 2.5 · Ambi 3.0 · Ambi 2.7 Inter · Ambi 1.0

---

## Stack Técnica

| | |
|-|-|
| **Tipo** | Aplicação estática — HTML + CSS + JS vanilla (sem dependências) |
| **Fontes** | Poppins via Google Fonts |
| **Ícones** | SVG inline (Feather/Lucide style, stroke-based) |
| **Logótipo** | PNG com transparência embutido em base64 |
| **Deploy** | Vercel (static) |

> Sem build step, sem npm, sem bundler. Um único ficheiro `index.html` auto-contido.

---

## Estrutura do Repositório

```
ambiconcept-kit-digital/
├── index.html       # Aplicação completa (self-contained)
├── vercel.json      # Configuração de deploy Vercel
├── .gitignore
└── README.md
```

---

## Deploy no Vercel

### Opção A — Via Interface Web (recomendado)

1. Fazer push deste repositório para o GitHub
2. Aceder a [vercel.com](https://vercel.com) → **Add New Project**
3. Importar o repositório GitHub
4. Framework Preset: **Other**
5. Build Command: *(deixar vazio)*
6. Output Directory: *(deixar vazio ou `.`)*
7. Clicar **Deploy**

### Opção B — Via Vercel CLI

```bash
npm i -g vercel
vercel login
vercel --prod
```

---

## Desenvolvimento Local

Sem dependências. Abrir directamente no browser:

```bash
# Opção 1 — abrir directamente
open index.html

# Opção 2 — servidor local simples (Python)
python3 -m http.server 8080
# → http://localhost:8080

# Opção 3 — servidor local (Node)
npx serve .
# → http://localhost:3000
```

---

## Actualização de Conteúdo

Todo o conteúdo está definido como arrays de objectos JavaScript dentro do `index.html`. Não requer back-end.

### Adicionar um novo produto

Localizar o array `PRODS` e adicionar uma entrada:

```javascript
const PRODS = [
  // ... produtos existentes ...
  { id: 'novo_id', label: 'Nome do Produto' },
];
```

O sistema gera automaticamente todos os cards para esse produto em todas as categorias (Galeria + Documentação Técnica).

### Adicionar um recurso a uma categoria

**Galeria** → array `GAL`  
**Documentação Técnica (ambos perfis)** → array `TEC_BASE`  
**Documentação Técnica (Distribuidor only)** → array `TEC_DIST_EXTRA`  
**Documentação Técnica (Parceiro — secção estática)** → array `TEC_PARTNER_STATIC`  
**Comercial** → array `COM_DIST`  
**Redes Sociais** → objecto `NET_CARDS[rede]`

Estrutura de um card:

```javascript
{
  title: 'Nome do Recurso',
  desc:  'Descrição geral',   // ou usar dD/dP para textos por perfil
  dD:    'Texto Distribuidor', // alternativa a desc
  dP:    'Texto Parceiro',     // alternativa a desc
  dims:  '1080 × 1080 px',    // opcional — para formatos de redes sociais
  fmts:  [{ l: 'PDF' }, { l: 'PNG', g: 1 }],  // g:1 = badge verde
  sz:    '~5 MB',
  tags:  'palavras chave pesquisa',
  badge: 'Novo',              // opcional
}
```

### Actualizar o logótipo

Substituir a string base64 na variável `logo_uri` (aparece 3× no HTML — entry, header, footer).

---

## Próximos Passos

### 🔐 Sistema de Login *(a implementar)*

Ponto de entrada planeado para autenticação. Opções a considerar:

| Abordagem | Complexidade | Adequado para |
|-----------|-------------|---------------|
| **Password simples + localStorage** | Baixa | Acesso protegido básico por perfil |
| **Vercel Edge Middleware + cookie** | Média | Protecção server-side sem back-end dedicado |
| **Supabase Auth** | Média | Login com e-mail, gestão de utilizadores |
| **Clerk / Auth0** | Baixa-Média | Login social, gestão delegada |

A estrutura actual (seleção de perfil no ecrã de entrada) está preparada para receber uma camada de autenticação à frente — o `enterAs('dist')` / `enterAs('partner')` pode ser chamado após validação de credenciais sem alterar a lógica interna da aplicação.

---

## Paleta de Cores

| Token | Hex | Uso |
|-------|-----|-----|
| `--gd` | `#006847` | Verde escuro da marca (botões, tabs activas, pills, borders activos) |
| `--g`  | `#6EC43A` | Verde claro da marca (badges de formato PNG) |
| `--s`  | `#3D5266` | Slate (texto secundário, badge de perfil) |
| `--tx` | `#1a2b22` | Texto principal |
| `--mu` | `#5a7566` | Texto muted |
| `--wh` | `#ffffff` | Superfícies de card |
| `--off`| `#f6f9f7` | Fundo da página |

---

## Contacto

**Ambiconcept Waste Solutions**  
geral@ambiconcept.pt  
[www.ambiconcept.pt](https://www.ambiconcept.pt)
