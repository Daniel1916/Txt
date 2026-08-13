# Git Notes — editor .txt sincronizado com GitHub

PWA simples: um ecrã, uma caixa de texto, dois botões — **Obter** (lê o ficheiro
do repositório) e **Gravar** (grava as alterações de volta). Instala-se no
ecrã principal do Android como uma app normal.

## Ficheiros

- `index.html` — a app inteira (HTML + CSS + JS)
- `manifest.json` — torna a app instalável
- `service-worker.js` — permite abrir a app offline (o conteúdo do ficheiro só
  sincroniza com ligação à internet)
- `icon-192.png`, `icon-512.png`, `icon-512-maskable.png` — ícones da app

## 1. Publicar os ficheiros (GitHub Pages)

A app precisa de um URL https real — não funciona só a abrir o `index.html`
localmente, porque o service worker e o "instalar app" exigem isso.
A forma mais simples, já que estás a usar GitHub, é o GitHub Pages:

1. Cria um repositório novo (pode ser o mesmo onde vais guardar o `.txt`, ou
   outro só para a app — tanto faz).
2. Envia estes 6 ficheiros para a raiz do repositório (ou para uma pasta
   `/docs`).
3. Em **Settings → Pages**, escolhe a branch e a pasta onde ficaram os
   ficheiros, e grava.
4. Ao fim de um ou dois minutos o GitHub dá-te um URL do género
   `https://teu-user.github.io/nome-do-repo/`.

## 2. Criar o token de acesso

Dentro da app, o botão ⚙ pede um **personal access token**. Cria um em
GitHub → **Settings → Developer settings → Personal access tokens →
Fine-grained tokens**:

- **Repository access**: só o repositório onde está o teu `.txt`
- **Permissions**: `Contents` → **Read and write** (não precisas de mais nada)

Este token fica guardado apenas no armazenamento local do teu telemóvel — a
app fala diretamente com `api.github.com`, sem passar por nenhum servidor
intermédio.

## 3. Instalar no Android

1. Abre o URL do GitHub Pages no Chrome do telemóvel.
2. Toca no botão ⬇ na barra superior (ou no menu ⋮ → "Adicionar ao ecrã
   principal" / "Instalar app").
3. A partir daí abre como uma app normal, com ícone próprio.

## 4. Usar

- Na primeira vez, preenche dono/organização, nome do repositório, caminho do
  ficheiro (ex.: `notas.txt`, ou `pasta/notas.txt`) e o token.
- **Obter** traz a versão mais recente do GitHub.
- **Gravar** faz commit e push das alterações para o repositório.
- Se o ficheiro ainda não existir no repositório, "Gravar" cria-o.
- Se editares o mesmo ficheiro noutro sítio entretanto, a app avisa-te de
  conflito antes de deixares perder alterações.
- O botão 📍 no cabeçalho pede a localização atual do telemóvel (o navegador
  vai pedir permissão na primeira vez) e insere uma linha no texto com data,
  hora, coordenadas e um link do Google Maps — no ponto onde estiver o cursor,
  ou no fim do texto se a caixa não estiver em foco. Isto só insere o texto;
  ainda precisas de tocar em **Gravar** para sincronizar com o GitHub.
  A geolocalização também exige o URL https do passo 1 (não funciona a abrir
  o ficheiro localmente).

## Nota sobre a pré-visualização no chat

A pré-visualização do `index.html` dentro desta conversa serve só para veres
o código — o service worker e o "instalar app" não funcionam dentro do
sandbox do chat. Para a app funcionar a sério (incluindo no telemóvel),
publica os ficheiros como no passo 1.
