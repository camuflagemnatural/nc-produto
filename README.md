# Natural Camouflage — Frontend em vários repositórios

Cada pasta `nc-*` é **um repositório do GitHub** (GitHub Pages). O backend continua no Render, sem mudanças.

| Repositório | Página | URL |
|---|---|---|
| nc-core | visual, carrinho, catálogo, API (compartilhado) | /nc-core/ |
| nc-home | Home | /nc-home/ |
| nc-categorias | Categorias / coleção (filtro e ordenação) | /nc-categorias/ |
| nc-busca | Busca | /nc-busca/?q=preta |
| nc-produto | Produto | /nc-produto/?id=2 |
| nc-favoritos | Favoritos | /nc-favoritos/ |
| nc-carrinho | Carrinho | /nc-carrinho/ |
| nc-checkout | Checkout (Pix + cartão, Mercado Pago) | /nc-checkout/ |
| nc-confirmacao | Confirmação do pedido | /nc-confirmacao/?pedido=NC-... |
| nc-minha-conta | Minha conta | /nc-minha-conta/ |
| nc-rastreio | Rastrear pedido | /nc-rastreio/ |
| nc-institucional | Sobre, trocas, privacidade, termos, contato | /nc-institucional/?p=trocas |

## Como os repositórios se ligam
1. **Mesma origem.** Todos os repos de uma conta ficam em `https://USUARIO.github.io/nc-xxx/`. Origem igual = o `localStorage` é compartilhado. Carrinho, favoritos, CEP e pedidos passam de uma página para outra assim.
2. **nc-core.** Toda página carrega `/nc-core/css/core.css` e `/nc-core/js/core.js`. Mudou o visual, o catálogo ou o cabeçalho? Edite só o `nc-core`.
3. **Links.** Todos os caminhos entre páginas estão em `nc-core/js/core.js` (objeto `R`). Se renomear um repositório, mude só ali.
4. **Backend.** `API` em `core.js` aponta para o Render. O CORS do backend já libera `https://camuflagemnatural.github.io`; como todos os repos usam essa origem, **não precisa mexer no Render**. Se mudar de conta ou usar domínio próprio, ajuste `FRONTEND_ORIGIN` no Render.

## Publicar
Para cada pasta: criar o repositório com o mesmo nome (ex.: `nc-home`), enviar o conteúdo da pasta na raiz, e em Settings > Pages escolher branch `main`, pasta `/ (root)`.
Ou use `publicar.sh` (precisa do GitHub CLI `gh` logado).

**Home na raiz do site:** renomeie o repo da home para `USUARIO.github.io` e troque `home: '/nc-home/'` por `home: '/'` em `core.js`.

## Testar no computador
Na pasta que contém todos os `nc-*`:
`npx serve .` e abra http://localhost:3000/nc-home/
(os caminhos começam com `/nc-...`, então abrir o arquivo direto no navegador não funciona).

## Pendências / limites desta fase (só frontend)
- **Catálogo:** fica em `core.js` (ids iguais ao `catalog.json` do backend). Quando houver API de produtos, troque por fetch.
- **Minha conta:** sem login. Dados e pedidos ficam só neste navegador (CPF não é salvo).
- **Rastreio:** mostra "pedido recebido" e "pagamento aprovado" via backend. Separação/envio/entrega dependem do painel admin.
- **Sem cupons:** o backend ainda não aceita cupom.
- **Textos institucionais:** são modelos. Revise antes de divulgar. Preencha `CONTACT` em `core.js` (WhatsApp, Instagram, e-mail).
- **Banners:** ver `nc-core/assets/banners/LEIA-ME.md`. Sem imagem, as páginas usam um fundo camuflado.
