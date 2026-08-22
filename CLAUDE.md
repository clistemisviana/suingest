# SuinGest — instruções para o Claude Code

Este arquivo é lido automaticamente pelo Claude Code no início de cada sessão nesta pasta.
Ele existe pra você não precisar reexplicar o projeto do zero toda vez.

## O que é o projeto

SuinGest é um sistema de gestão de suinocultura para uso pessoal (fazenda do Clistemis,
Suinocultura São José), com potencial futuro de virar micro-SaaS. Faz parte do
portfólio C.On — Gestão de Resultados, junto com outros sistemas em HTML single-file
hospedados no GitHub Pages.

## Estado atual (importante)

- **Um único arquivo `index.html`** — HTML + CSS + JavaScript vanilla, tudo inline, sem
  build step, sem framework, sem dependências externas de runtime. Esse é o padrão usado
  em todos os sistemas do portfólio C.On — mantenha assim, não separe em vários arquivos
  nem introduza bundler (Vite, Webpack etc.) sem que o Clistemis peça.
- **Persistência: `localStorage`, por enquanto.** Isso é esperado nesta fase — o app foi
  desenvolvido como protótipo pessoal antes da migração de ferramenta. A migração para
  Firebase (ver abaixo) ainda **não foi feita**.
- Hospedagem prevista: GitHub Pages (`index.html` na raiz do repositório).

## Decisão de backend (fixada em 01/08/2026)

- Backend definitivo: **Firebase, plano Spark (gratuito)**, enquanto o uso for pessoal/da
  fazenda.
- **Não migrar para Supabase agora.** Só reavaliar armazenamento/hospedagem se e quando o
  sistema virar produto comercial de verdade — não antes disso.
- A migração de `localStorage` → Firebase (Firestore) ainda está pendente. Quando for
  feita, considerar manter `localStorage` como cache/fallback offline, a confirmar com o
  Clistemis antes de implementar.
- Login/controle de usuário também foi conscientemente adiado para esta fase de migração
  web — ainda não existe no app.

## Convenções de domínio (suinocultura) já implementadas

- **Brincos**: cor + número + ano, ex. `AMA 001/26`.
- **Três datas por animal**: nascimento, compra, chegada (chegada opcional).
- **Peso estimado por fita métrica**: `perímetro² × comprimento ÷ 14430` (cm), fator
  configurável em Configurações.
- **Rendimento de carcaça**: padrão 75%, ajustável em Configurações; recalcula tudo
  dinamicamente (peso vivo estimado, ganho, conversão, curva, projeção de 6@).
- **Peso de venda** é sempre peso de carcaça; meta de 6@ = peso de carcaça.
- **Animal de terceiro**: ração vira custo de mão de obra do proprietário do animal; a
  compra, sanidade e receita da venda são do dono, não entram no lucro de quem cria.
- **CA (conversão alimentar)** = kg de ração ÷ kg de ganho de peso vivo.
  **EA (eficiência alimentar)** = 100 ÷ CA, exibida como **gramas de ganho por kg de
  ração** (não em %, decisão explícita — ver histórico de conversa se precisar do porquê).
  Faixas de classificação (referência de mercado, ciclo completo):
  - ≤ 2,40 → Excelente · 2,41–2,55 → Muito boa · 2,56–2,70 → Atenção ·
    2,71–2,90 → Baixa eficiência · > 2,90 → Necessita ação imediata (ou "Resultado
    insatisfatório" se o animal já foi vendido — nunca linguagem de ação para animal já
    vendido).
  - Meta usada nos gráficos: `CA_META = 2.55` (fixa por enquanto).

## Padrão visual (não inventar um novo)

- Fundo `--bg:#EEF2F3`, superfícies brancas, cantos arredondados generosos (`--radius`),
  paleta verde como cor primária (`--primary:#1E7D34`), tons de âmbar/vermelho para
  alertas.
- Cards de estatística usam as classes `.mstat`/`.mv`/`.msub`, com variantes específicas
  `.mv-num`/`.mv-unit` para números em destaque com unidade discreta abaixo (usado em
  CA/EA).
- Ícones são SVGs stroke-based minimalistas, definidos no objeto `ICONS` e renderizados
  via `ic('nome')` — não colar ícones de bibliotecas externas (Lucide, FontAwesome etc.).
- Textos da interface em português (Brasil).

## Próximos passos conhecidos (não fazer sem confirmar prioridade com o Clistemis)

1. Configurar projeto no Firebase Console (Spark) e migrar `localStorage` → Firestore.
2. Decidir se/como fica login (Firebase Auth) — Sistema 12 (100 Anos Vó Cida) já tem um
   padrão de Auth com criação de usuário centralizada em Configurações; pode servir de
   referência de abordagem, mas confirmar antes de replicar.
3. Publicar no GitHub Pages.

## Como trabalhar comigo (Clistemis) nas sessões

- Sou indie maker, forte em frontend/UX, tenho um sócio técnico para backend/infra — mas
  quero aprender a usar o Claude Code bem, então pode ir me explicando o que está fazendo,
  não só executando.
- Prefiro terminologia técnica correta, acompanhada de explicação em linguagem simples.
- Antes de mudanças estruturais grandes (trocar arquitetura, adicionar dependência,
  mudar backend), me avise e explique o porquê antes de implementar.
