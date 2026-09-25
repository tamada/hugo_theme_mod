# hugo_them_mod

## :speaking_head: Overview

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

This is a Hugo theme template repository for my websites.
The base of this theme is [Blowfish][blowfish]

This theme modified some partial layout codes from [Blowfish][blowfish] and appended some custom shortcodes.
Also, this theme compiles CSS from [Blowfish][blowfish]'s SCSS files and adds extra Tailwind CSS utilities.

[blowfish]: https://blowfish.page

## :runner: Use this theme

Add the following entries into your Hugo site's `config/_default/hugo.toml` file.

```toml
[module]
  [[module.imports]]
    path = "github.com/tamada/hugo_theme_mod"
```

## Appended Shortcodes

### `commentout`

This shortcode comments out the content inside it.
Usage:

```markdown
{{< commentout >}}
This content will be a comment in the resultant HTML file, and does not render.
{{< /commentout >}}
```

### `status_badge`

```markdown
{{< status_badge href="https://url.to/link" label="label" value="value" color="123456" icon="github" >}}
```

### `paper`

This shortcode renders the paper of the given id, obtained from the papers API
(<https://tamadalab.github.io/api/papers> by default).

```markdown
{{< paper "2026wsse_fedorov" >}}
{{< paper id="2026wsse_fedorov" >}}
{{< paper id="2026wsse_fedorov,2026tse_fedorov" >}}
{{< paper id="2026wsse_fedorov" badges="false" >}}
{{< paper id="2026wsse_fedorov" field="title" >}}
```

| parameter | description |
|-----------|-------------|
| `id` (or the first positional parameter) | the id(s) of the paper(s), separated by commas. Note that Hugo does not allow mixing positional and named parameters. |
| `field` | print the raw value of the given key (`title`, `year`, `authors`, ...) instead of the citation. |
| `badges` | give `false` to suppress the badges of the links (default: `true`). |

The API is accessed **once per build**, not once per shortcode:
`layouts/partials/papers/data.html` fetches the endpoint by
[`resources.GetRemote`][getremote], which stores the response in Hugo's
`getresource` file cache, and the shortcode reads it through
[`partialCached`][partialcached], which unmarshals the JSON only once.
The cached response is reused by the succeeding builds as well; run
`hugo --ignoreCache` to fetch it again.

[getremote]: https://gohugo.io/functions/resources/getremote/
[partialcached]: https://gohugo.io/functions/partials/includecached/

The following parameters are available in `config/_default/params.toml` of your
site. Note that `[caches]` is not merged from the theme, hence set it in the
`hugo.toml` of your site if you want the cache to expire.

```toml
[params.api]
  papers = "https://tamadalab.github.io/api/papers"
  # set it to render the badges downloading the paper/poster PDFs.
  # momonga = "https://momonga.example.com"

# in hugo.toml; the default maxAge is -1, which means the response never expires.
[caches.getresource]
  dir = ':cacheDir/:project'
  maxAge = '24h'
```

