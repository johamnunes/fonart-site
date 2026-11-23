# fonart-site

Site da fonoaudióloga Natalia Horvath (CRFa 2-21896), hospedado no Cloudflare Workers com arquivos estáticos.

## Estrutura

```
public/
  index.html      página única do site
  404.html        página de erro
  _headers        cabeçalhos de cache e segurança
  robots.txt      liberação para buscadores e endereço do sitemap
  sitemap.xml     mapa do site
  img/            logo, fotos (WebP), favicon e imagem de compartilhamento (og.jpg)
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

## SEO

Já no código:

- `<title>`, meta description, canonical e Open Graph em `public/index.html`
- Dados estruturados (JSON-LD): `MedicalBusiness`, `Person` (com o CRFa) e `FAQPage`, gerado a partir das perguntas visíveis na página
- `robots.txt` e `sitemap.xml`
- Um único `h1` com profissão e bairros, imagens em WebP com `width`/`height` e lazy loading abaixo da dobra

Depois de publicar no domínio:

1. **Google Search Console**: adicionar o domínio, verificar pelo DNS no Cloudflare e enviar `https://www.horvathfonoaudiologia.com.br/sitemap.xml`.
2. **Perfil da Empresa no Google** (Google Business Profile): é o que mais pesa para aparecer em buscas como "fonoaudióloga na Vila Mariana". Usar a mesma grafia de nome, telefone e bairros do site e colocar o link do site.
3. **Redirecionar o domínio sem www para o www** no Cloudflare (Rules → Redirect Rules), já que o canonical usa `www`.
4. Testar os dados estruturados em https://search.google.com/test/rich-results.

## Pendências

- Trocar as fotos em `public/img/` pelos arquivos originais em alta resolução (as atuais foram capturadas do site antigo).
- Trocar `logo-simbolo.png` pela logo original com fundo transparente.
