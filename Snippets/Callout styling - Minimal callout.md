↪[Collection](Collection.md)

# Callout styling - Minimal callout

---

- author:: rushi
- source::

---

cover:: ![[Snippets/56b3517510f9bdbf09001e7ce7ff4bbe_MD5.png]]

```css
.callout[data-callout="m-callout"] {
  --callout-color: transparent;
  border: none;
  padding: 0;
}

.callout[data-callout="m-callout"] .callout-title {
  display: none;
  padding: 0;
}

.callout[data-callout="m-callout"] .callout-content {
  font-size: 85%;
  text-align: center;
}

.callout[data-callout="m-callout"] .callout-content::after {
  content: "--- ♪ ♪ ♪ ---";
  color: var(--text-accent);
}
```

---

## How to use

```md
> [!m-callout] Title
> Lorem ipsum dolor sit amet consectetur adipisicing elit. Minus assumenda iusto sint officia quas distinctio doloribus harum optio commodi eum!
```
