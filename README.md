# Trenna Distribuição — Site (Edição Setembro Amarelo)

Redesign completo do site da Trenna Distribuição (distribuidora de ferramentas e utilidades, Uberlândia-MG), construído como um **único arquivo HTML autocontido** — sem build step, sem dependências de servidor.

🔗 **Versão publicada:** https://claude.ai/artifact/21ZXdTVW9vjvj7LEacKLE4

---

## Sobre o projeto

Site institucional + catálogo + carrinho de pedidos, com uma campanha ativa de conscientização **Setembro Amarelo** integrada ao tema visual.

## Funcionalidades

- **Home institucional** — hero, indicadores, diferenciais, Missão/Visão/Valores, parceiros, mapa de localização, contato.
- **Catálogo completo pesquisável** — 4.530 produtos extraídos do catálogo oficial (PDF de junho/2026), com busca por nome/código/marca, filtro por departamento (18 categorias) e paginação incremental.
- **Fotos dos produtos** — 4.249 dos 4.530 itens (94%) têm foto real, recortada automaticamente das páginas do catálogo original e associada ao código correspondente.
- **Carrinho de pedidos** — cliente monta o pedido, escolhe a forma de entrega (retirar na empresa ou entrega em até 72h) e envia para o time comercial. **Não exibe preços** (o catálogo é B2B e não lista valores — a cotação é sempre feita com o vendedor).
- **Painel do Vendedor** — duas abas: pedidos recebidos (com atualização de status) e cadastro de promoções (selecionadas a partir dos produtos com foto).
- **Campanha Setembro Amarelo** — tema em tons de amarelo, seção de conscientização, dicas de autocuidado e contato direto com o CVV (188).

## Tecnologia

- HTML + CSS + JavaScript puro (vanilla), tudo em um único arquivo (`index.html`).
- Fontes via Google Fonts (Playfair Display + Inter).
- Sem frameworks, sem bundler, sem `npm install`.

### ⚠️ Sobre a persistência de dados (pedidos e promoções)

O carrinho e o painel do vendedor usam uma API de armazenamento (`window.claude.use('db')`) disponível **apenas dentro do ambiente de Artifacts do Claude**. Isso significa:

- **Hospedado no Claude** (link acima): pedidos e promoções são salvos de verdade e ficam visíveis para qualquer pessoa com acesso ao artefato.
- **Hospedado fora do Claude** (GitHub Pages, servidor próprio, etc.): o site funciona normalmente — catálogo, busca, carrinho, navegação —, mas a chamada a `window.claude.use('db')` falha silenciosamente (`db = null`) e o código já trata isso: o pedido não é salvo, apenas o link de e-mail (`mailto:`) com o resumo do pedido continua funcionando.

Para usar este site em produção **fora do Claude**, é necessário substituir as chamadas a `db.collection(...)` / `db.doc(...)` (busque por `window.claude.use('db')` no arquivo) por uma solução real de backend — por exemplo Firebase, Supabase, ou uma API própria.

## Como usar

Não há instalação. Basta abrir o arquivo `index.html` em qualquer navegador, ou publicar a pasta em qualquer hospedagem de arquivos estáticos:

```bash
# localmente
open index.html          # macOS
xdg-open index.html      # Linux

# ou subir num servidor estático simples
python3 -m http.server 8000
```

### Publicar no GitHub Pages

1. Suba este repositório para o GitHub.
2. Renomeie o arquivo principal para `index.html` (se ainda não estiver assim).
3. Em **Settings → Pages**, selecione a branch e a pasta raiz (`/`).
4. O site ficará disponível em `https://<seu-usuario>.github.io/<repo>/`.

*(Lembre-se da limitação de persistência descrita acima ao usar essa opção.)*

## Origem dos dados

- Textos institucionais, endereço, telefone e e-mail: extraídos do site público e de materiais fornecidos pela empresa.
- Catálogo de produtos: extraído automaticamente de `CATALOGO_2026_JUNHO_FINAL.pdf` (367 páginas, 18 departamentos) via parsing de texto e recorte de imagens.

## Limitações conhecidas

- **Extração de produtos automática:** o PDF não é um banco de dados estruturado — o parsing por texto pode, em casos isolados (produtos com descrições longas ou layout denso), gerar nomes truncados ou levemente incorretos. Recomenda-se revisão antes de uso comercial crítico.
- **Fotos:** 281 produtos (6%) não têm foto associada com confiança suficiente e mostram um selo com as iniciais do departamento no lugar.
- **Sem cálculo de frete/prazo automático:** por decisão do time, isso é feito diretamente com o vendedor.
- **Painel do vendedor sem autenticação:** qualquer pessoa com acesso de edição ao site pode ver pedidos e cadastrar promoções — não há login por usuário.
- **Preços:** o catálogo de origem não lista valores; o site nunca exibe preço de produto, apenas nas promoções cadastradas manualmente pelo vendedor.

## Estrutura

```
.
└── index.html   ← site inteiro (HTML + CSS + JS + dados do catálogo + imagens embutidas em base64)
```

## Contato

**Trenna Distribuição**
R. Londres, 1595 — Tibery, Uberlândia - MG
(34) 3216-9574 · trenna@trenna.com.br
