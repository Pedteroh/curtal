# Criador de Currículo

Site estático e instalável (PWA) para montar currículos. A pessoa escolhe um dos 8 modelos, preenche os dados, vê o currículo A4 ao vivo e baixa em PNG ou PDF. Não precisa de servidor, cadastro nem build. Os dados ficam só no navegador de quem usa.

## Arquivos

```
index.html              página inteira (HTML, CSS e JavaScript)
manifest.webmanifest    nome, cores e ícones do app instalável
sw.js                   service worker (cache e uso offline)
icon.svg                logo (também usada como favicon)
icons/                  ícones PNG: 192, 512, maskable, apple-touch e favicon
```

## Publicar no GitHub Pages

1. Crie um repositório no GitHub e envie todos os arquivos desta pasta para a raiz do repositório.
2. No repositório, abra **Settings → Pages**.
3. Em **Build and deployment**, escolha **Deploy from a branch**, selecione a branch `main` e a pasta `/ (root)`, e salve.
4. Aguarde cerca de um minuto. O site fica em `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/`.

Todos os caminhos são relativos, então o site funciona dentro de um subdiretório como esse. O service worker exige HTTPS, que o GitHub Pages já oferece.

## Testar no computador

Abra uma pasta no terminal e rode:

```
python3 -m http.server 8000
```

Depois acesse `http://localhost:8000`. O service worker também funciona em `localhost`. Abrir o `index.html` direto com duplo clique mostra a página, mas sem instalação e sem uso offline.

## Instalar como app

- **Chrome e Edge (computador e Android):** clique em **Instalar app** no cabeçalho ou use o ícone de instalar na barra de endereço.
- **iPhone e iPad (Safari):** toque em Compartilhar e depois em **Adicionar à Tela de Início**.

## Uso offline

Na primeira visita, o service worker guarda a página, os ícones, as bibliotecas de exportação (html2canvas e jsPDF) e as fontes. Depois disso o app abre e exporta sem internet. Se a primeira visita for sem conexão, a exportação não funciona até o site carregar uma vez online.

Para não depender de CDN, baixe `html2canvas.min.js` e `jspdf.umd.min.js`, coloque-os numa pasta `libs/`, troque os dois `<script src=...>` do `index.html` pelos caminhos locais e inclua os arquivos na lista `CORE` do `sw.js`.

## Publicar uma atualização

O navegador guarda uma cópia do site. Ao alterar qualquer arquivo, aumente o número de `VERSION` no início do `sw.js` (`v1` para `v2`, e assim por diante) para que quem já visitou receba a versão nova.

## Adicionar um modelo

No `index.html`:

1. Adicione `{id:'meumodelo', name:'Meu modelo', desc:'Descrição curta'}` à lista `TEMPLATES`.
2. Crie a função `meumodelo: function(d){ ... }` dentro de `TPL`. Ela recebe os dados e devolve o HTML do currículo. Os auxiliares `sec`, `expH`, `eduH`, `pills` e `lns` montam as seções.
3. Escreva o CSS com o prefixo `.t-meumodelo`. As cores de destaque vêm das variáveis `--ac`, `--tint`, `--soft`, `--on` e `--on-line`.
4. Adicione uma miniatura em `thumb()`.

A folha mede 794 × 1123 px (A4). Conteúdo além disso vira a página 2 no PDF.

## Observações

- O PDF é gerado a partir de uma imagem da folha, então o texto não pode ser selecionado nem copiado.
- Bibliotecas: [html2canvas](https://html2canvas.hertzen.com/) e [jsPDF](https://github.com/parallax/jsPDF), ambas MIT. Fontes: Google Fonts, licença OFL.
