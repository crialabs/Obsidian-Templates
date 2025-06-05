↪[Collection](Collection.md)

# Checkboxes - Priority checkboxes

---

- author:: rushi
- source::

---

cover:: ![[Snippets/b7976f2059c95e4a415c6559c7edf140_MD5.png]]

```css
.HyperMD-list-line:has(.cm-tag-p1) .task-list-label {
  --checkbox-border-color: red;
}
.task-list-item:has([href="#p1"]) {
  --checkbox-border-color: red;
}

.HyperMD-list-line:has(.cm-tag-p2) .task-list-label {
  --checkbox-border-color: gold;
}
.task-list-item:has([href="#p2"]) {
  --checkbox-border-color: gold;
}

.HyperMD-list-line:has(.cm-tag-p3) .task-list-label {
  --checkbox-border-color: #1895f5;
}
.task-list-item:has([href="#p3"]) {
  --checkbox-border-color: #1895f5;
}
```

---

## How to use

```md
- [ ] High priority #p1
- [ ] Medium priority #p2
- [ ] Low priority #p3
```
