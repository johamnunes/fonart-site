# fonart-site

Site da fonoaudióloga Natalia Horvath (CRFa 2-21896), hospedado no Cloudflare Workers com arquivos estáticos.

## Estrutura

```
public/
  index.html      página única do site
  404.html        página de erro
  _headers        cabeçalhos de cache e segurança
  img/            logo, fotos, favicon e imagem de compartilhamento (og.jpg)
wrangler.jsonc    configuração do Cloudflare
```

Não há build: o conteúdo de `public/` é publicado como está.

## Ver localmente

```bash
npx wrangler dev
```

## Publicar

```bash
npx wrangler login     # só na primeira vez
npx wrangler deploy
```

O site sai em `https://fonart-site.<sua-conta>.workers.dev`.

## Domínio próprio

1. Adicione `horvathfonoaudiologia.com.br` no painel do Cloudflare e troque os nameservers no Registro.br.
2. Antes de trocar, confira se os registros MX de e-mail foram importados e remova os registros que apontam para o Google Sites.
3. No Worker, em Settings → Domains & Routes, adicione `horvathfonoaudiologia.com.br` e `www.horvathfonoaudiologia.com.br`.

## Pendências

- Trocar as fotos em `public/img/` pelos arquivos originais em alta resolução (as atuais foram capturadas do site antigo).
- Trocar `logo-simbolo.png` pela logo original com fundo transparente.
