# Criador de Currículo

Site estático e instalável (PWA) para montar currículos. 13 modelos, editor de layout parecido com o Canva e exportação em PNG e PDF. Sem servidor, sem cadastro, sem build. Os dados ficam só no navegador de quem usa.

## Arquivos

```
index.html              o site inteiro (HTML, CSS e JavaScript)
icon.svg                logo (favicon e cabeçalho)
manifest.webmanifest    nome, cores e ícones do app instalável
sw.js                   service worker (cache e uso offline)
icons/                  ícones PNG: 192, 512, maskable, apple-touch e favicon
```

Tudo na raiz do repositório, com a pasta `icons` ao lado do `index.html`.

## Publicar no GitHub Pages

1. Envie os arquivos para a raiz do repositório.
2. Em **Settings → Pages**, escolha **Deploy from a branch**, branch `main`, pasta `/ (root)`.
3. O site fica em `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/`.

Para testar no computador: `python3 -m http.server 8000` e abra `http://localhost:8000`.

## Editor de layout

Na prévia, clique em **Editar layout**.

- **Mover:** arraste o bloco. Linhas rosas mostram quando ele está alinhado ao centro da página, às margens ou a outro bloco, e o bloco "gruda" nelas. Segure **Alt** para mover sem o ímã. O botão **Guias** liga e desliga.
- **Redimensionar:** círculos dos cantos ampliam ou reduzem (o canto oposto fica parado); os das laterais mudam a largura. Um rótulo mostra a porcentagem.
- **Alinhar:** a barra acima do bloco tem alinhar à esquerda, centralizar, direita, topo, meio e base. Com um bloco, alinha à página; com vários, alinha entre eles.
- **Vários blocos:** Shift + clique, ou arraste numa área vazia da folha. Ctrl + A seleciona tudo.
- **Teclado:** setas movem 1 px (Shift: 10 px), Delete oculta, Esc desmarca, Ctrl + Z desfaz, Ctrl + Y ou Ctrl + Shift + Z refaz.
- **Zoom:** botões + e −, ou Ctrl + roda do mouse. Clique na porcentagem para voltar ao ajuste.
- A aba **Layout** lista os blocos para mostrar de novo os ocultos e tem o botão de voltar ao layout original. O layout fica salvo por modelo.

## Tudo em 1 página

O botão **Tudo em 1 página** (ligado por padrão) reduz o conteúdo até caber em uma folha A4 e avisa a porcentagem usada. Se mesmo no menor tamanho não couber, aparece um aviso. Desligado, o currículo pode ter várias páginas.

## Instalar como app

- **Chrome e Edge:** botão **Instalar app** no cabeçalho.
- **iPhone (Safari):** Compartilhar, depois **Adicionar à Tela de Início**.

Se não instalar: o site precisa estar em HTTPS (GitHub Pages) ou `localhost`, a pasta `icons` precisa estar no repositório e o navegador precisa suportar instalação.

## Publicar uma atualização

Aumente o número de `VERSION` no início do `sw.js` (`v5` para `v6`) para quem já visitou receber a versão nova.

## Observações

- O PDF é gerado a partir de uma imagem da folha, então o texto não pode ser selecionado.
- Bibliotecas: html2canvas e jsPDF (MIT), carregadas de uma CDN. Fontes: Google Fonts (OFL).
