↪[Collection](Collection.md)

# Command palette styling 02

---

- author:: rushi
- source::

---

cover:: ![[Snippets/9ce047f07b16f9bdcfc4a716da59287a_MD5.gif]]

```css
.suggestion-item.is-selected {
  background-color: hsla(var(--interactive-accent-hsl), 0.8);
  border-radius: 6px;
}

.prompt {
  border-radius: 8px;
}

.suggestion-highlight {
  color: var(--text-accent);
}

.suggestion-item.is-selected .suggestion-highlight {
  color: white !important;
}

input.prompt-input {
  box-shadow: rgba(0, 0, 0, 0.2) 0px 60px 40px -7px !important;
}
```
