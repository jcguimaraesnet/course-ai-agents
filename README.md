# Curso: Agentes de IA com Python

Apresentação (slides) do curso **Fundamentos de Agentes com Python e APIs — Desenvolvimento de Agentes Inteligentes**.

🔗 **Slides online:** https://jcguimaraesnet.github.io/course-ai-agents/

Construído com [Slidev](https://sli.dev).

## Rodando localmente

```bash
pnpm install
pnpm dev
```

Abre em <http://localhost:3030>.

## Scripts

| Comando | O que faz |
|---------|-----------|
| `pnpm dev` | Servidor de desenvolvimento (hot-reload) |
| `pnpm build` | Gera o site estático em `dist/` (com `--base /course-ai-agents/`) |
| `pnpm export` | Exporta os slides para PDF |

## Estrutura

| Caminho | Descrição |
|---------|-----------|
| `slides.md` | O deck (entrada do Slidev) |
| `layouts/` | Layouts customizados (`custom-author`, `image-x`) |
| `components/` | Componentes Vue (`GitHubIcon`) |
| `slide-bottom.vue` | Barra inferior com número da página e fonte (todos os slides) |
| `global-bottom.vue` | Fundo com efeito *glow* (todos os slides) |
| `styles/index.css` | Estilos globais (prefixo `#` nos títulos) |
| `public/` | Imagens |

## Publicação

O deploy é automático: a cada push na branch `main`, o workflow
[`.github/workflows/deploy.yml`](.github/workflows/deploy.yml) faz o build e publica no GitHub Pages.

> ⚠️ Como este é um *project site* (servido em `/course-ai-agents/`), o build **precisa** do
> `--base /course-ai-agents/` — já configurado no script `build`.

## Autor

**Júlio César Guimarães** · [LinkedIn](https://linkedin.com/in/jcguimaraesnet) · [GitHub](https://github.com/jcguimaraesnet)
