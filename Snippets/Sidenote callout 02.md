↪[Collection](Collection.md)

# Sidenote callout 02

---

- author:: FireIsGood
- source:: https://discord.com/channels/686053708261228577/702656734631821413/1145768722431225926

---

cover:: ![[Snippets/0eed513bc753e3bf0630c9d3dd9577e0_MD5.gif]]

```css
/*
author: FireIsGood
source: https://discord.com/channels/686053708261228577/702656734631821413/1145768722431225926
*/

:root {
  --tooltip-size: 250px;
}

.markdown-preview-view {
  container-name: page;
  container-type: inline-size;
}

@container page (width > 1200px) {
  .markdown-reading-view .callout[data-callout="epic"] {
    --p-spacing: 0;
    position: absolute;
    width: var(--tooltip-size);
    translate: calc(-1 * (var(--tooltip-size) + 1rem)) 0;
  }
}
```
