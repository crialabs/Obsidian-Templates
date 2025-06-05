↪[Collection](Collection.md)

# Kanban styling - background customized

---

- author:: dev-araujo
- source::

---

cover::![[Snippets/bf15ef26870c60185878c9511efb1266_MD5.png]]

```css
/*
author: dev-araujo
*/

/* --- Kanban With Background Customized --- */

.theme-dark .view-content .kanban-plugin::after,
.theme-light .view-content .kanban-plugin::after {
  content: "";
  position: fixed;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  z-index: -1;

  /* Change PATH-FOR-YOUR-BACKGROUND to your image path */
  background-image: url(PATH-FOR-YOUR-BACKGROUND) !important;
  background-repeat: no-repeat;
  background-size: cover;
}
```
