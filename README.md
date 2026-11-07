# Portfólio Wanderson Santana

Site estático (um único `index.html`), pronto para o GitHub Pages.

## Estrutura

```
index.html      ← o site inteiro (HTML, CSS e JS)
videos/         ← MP4 curtos em loop para a home
frames/         ← stills de cada projeto
.nojekyll       ← faz o GitHub Pages servir os arquivos sem processar
```

## Publicar no GitHub Pages

1. Crie um repositório público no GitHub. Se der o nome `seu-usuario.github.io`, o site fica em `https://seu-usuario.github.io`. Com qualquer outro nome, fica em `https://seu-usuario.github.io/nome-do-repo`.
2. Envie os arquivos desta pasta. Pelo navegador: **Add file → Upload files** e arraste tudo. Pelo terminal:
   ```bash
   git init
   git add .
   git commit -m "Primeira versão do portfólio"
   git branch -M main
   git remote add origin https://github.com/SEU-USUARIO/NOME-DO-REPO.git
   git push -u origin main
   ```
3. No repositório, vá em **Settings → Pages**. Em *Source*, escolha **Deploy from a branch**, branch `main`, pasta `/ (root)`, e clique em **Save**.
4. Em um ou dois minutos o link aparece no topo da mesma tela.

## Trocar os projetos de exemplo pelos seus

Abra o `index.html` e edite a lista `PROJECTS`, que fica no começo do `<script>`. Para cada projeto:

```js
{
  slug: "mare-alta",                 // vira o endereço: seusite.com/#mare-alta
  artist: "Lua Ferraz",
  title: "Maré Alta",
  cat: "videoclipes",                // videoclipes | comerciais | curtas
  year: 2026,
  dur: "03:41",
  about: "Uma ou duas frases sobre o projeto.",
  credits: [["Direção","Marina Costa"], ["Montagem","Wanderson Santana"]],
  look: { mode: "horizon", c: ["#0b1320","#1f4e6b","#e0865a","#ffd7a0"] },
  wide: true,                        // ocupa a linha inteira na home
  preview: "videos/mare-alta.mp4",   // loop da home
  embed: "https://vimeo.com/123456789",
  stills: [
    { src: "frames/mare-alta-01.jpg", tc: "00:00:27:15" },
    { src: "frames/mare-alta-02.jpg", tc: "00:01:04:02" }
  ]
}
```

- **`preview` vazio:** a home mostra a animação gerada com as cores de `look.c`.
- **`embed` vazio:** a página do clipe mostra essa mesma animação no player.
- **`stills` vazio:** aparecem 7 frames gerados.
- **`look`:** só é usado enquanto faltar vídeo ou frame.

Os dados de contato ficam em `CONTACT`, logo abaixo de `PROJECTS`.

## Dicas de arquivo

**Loops da home (`videos/`)**
- 5 a 10 segundos, sem áudio, H.264.
- 1280 px de largura.
- Até uns 3 MB cada.

No DaVinci, exporte em H.264 sem áudio. Para converter com ffmpeg:

```bash
ffmpeg -i entrada.mov -an -vf scale=1280:-2 -c:v libx264 -preset veryfast -crf 26 -movflags +faststart videos/nome.mp4
```

**Frames (`frames/`)**
- JPG ou WebP, com 1600 a 1920 px de largura.
- Os frames de número 1, 4 e 7 aparecem em largura total, cortados em 2.39:1. Use planos abertos nessas posições.

**Limites do GitHub**
- No máximo 100 MB por arquivo, e o repositório deve ficar abaixo de 1 GB.
- Vídeos completos vão no Vimeo ou YouTube, pelo campo `embed`. No repositório ficam só os loops curtos.
