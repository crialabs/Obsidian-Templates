↪[Collection](Collection.md)

# Icon before headings

---

- author:: rushi
- source::

---

> _You can change `§` with something else._

cover:: ![[Snippets/8a0d4fdbf27ba5c200755497d0e85c94_MD5.png]]

```css
:is(
    h1,
    h2,
    h3,
    h4,
    h5,
    h6,
    .HyperMD-header-1,
    .HyperMD-header-2,
    .HyperMD-header-3,
    .HyperMD-header-4,
    .HyperMD-header-5,
    .HyperMD-header-6
  )::before {
  content: "§ ";
  font-size: 0.7em;
  vertical-align: middle;
  color: var(--text-accent);
  font-weight: 500;
}
```
