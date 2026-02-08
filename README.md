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

