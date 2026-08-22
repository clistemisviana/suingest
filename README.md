# SuinGest

Sistema de gestão de suinocultura — controle de animais, pesagens, ração, custos,
vendas e indicadores zootécnicos (conversão e eficiência alimentar) por raça.

Desenvolvido para uso pessoal na Suinocultura São José, sob o portfólio
**C.On — Gestão de Resultados**.

## Stack

- HTML + CSS + JavaScript vanilla, arquivo único (`index.html`), sem build step.
- Persistência atual: `localStorage` (navegador).
- Backend planejado: Firebase (plano Spark, gratuito).
- Hospedagem: GitHub Pages.

## Rodando localmente

Não precisa de servidor nem instalação — é um arquivo HTML só:

```bash
# opção 1: abrir direto no navegador
open index.html      # macOS
start index.html      # Windows

# opção 2: servir localmente (evita alguns bloqueios de segurança do navegador)
python3 -m http.server 8000
# depois acesse http://localhost:8000
```

## Desenvolvimento

Este projeto usa o [Claude Code](https://code.claude.com) como ferramenta principal de
desenvolvimento. O arquivo `CLAUDE.md` na raiz tem todo o contexto de domínio, decisões
de arquitetura e convenções — o Claude Code lê ele automaticamente ao iniciar uma sessão
nesta pasta.

## Deploy (GitHub Pages)

Settings → Pages → Deploy from a branch → `main` / `/ (root)`.
O `index.html` na raiz já é o suficiente para o GitHub Pages publicar o site.
