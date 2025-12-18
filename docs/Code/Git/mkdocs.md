# Mkdocs

## 常用命令

```powershell
// 新建
mkdocs new .
// 预览
mkdocs serve
// 生成静态网页
mkdocs build
```



## 常见问题

* 列表没有层级：次层级需要 **4** 个空格





## 配置

### mkdocs.yml 



```yaml
site_name: site name
extra_css:
  - stylesheets/extra.css
theme:
  name: material
  features:
    - content.footnote.tooltips
    - navigation.indexes
    - navigation.top
  palette:
    # Palette toggle for automatic mode
    - media: "(prefers-color-scheme)"
      toggle:
        icon: material/brightness-auto
        name: Switch to light mode

    # Palette toggle for light mode
    - media: "(prefers-color-scheme: light)"
      scheme: default
      primary: white
      toggle:
        icon: material/brightness-7
        name: Switch to dark mode

    # Palette toggle for dark mode
    - media: "(prefers-color-scheme: dark)"
      scheme: slate
      primary: black
      toggle:
        icon: material/brightness-4
        name: Switch to system preference

markdown_extensions:
  - footnotes
  - pymdownx.critic
  - pymdownx.caret
  - pymdownx.mark
  - pymdownx.tilde
  - toc:
      permalink: true

plugins:
  - awesome-pages:
      filename: .pages
      collapse_single_pages: true
      strict: false
  - search:
      lang:
        - en
        - ja
      separator: '[\s\-\.]+'

```



### .page

```yaml
nav:
    - index.md
    - ...
collapse: true
# Sorting
order: asc
sort_type: natural
order_by: filename
```





### CSS

```css
:root {
    font-family:
        "Source Han Serif",
        "Noto Serif",
        "Noto Serif SC",
        -apple-system,
        BlinkMacSystemFont,
        "Segoe UI",
        Roboto,
        Oxygen,
        Ubuntu,
        Cantarell,
        "Open Sans",
        "Helvetica Neue",
        sans-serif;
}

p {
    line-height: 1.5rem;
    letter-spacing: 0.02rem;
}
.md-nav__list li {
    margin-top: 0.8rem;
}

.md-header--shadow {
    box-shadow: none;
}

```

