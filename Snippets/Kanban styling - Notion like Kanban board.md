↪[Collection](Collection.md)

# Kanban styling - Notion like Kanban board

---

- author:: Anubis
- source:: https://github.com/AnubisNekhet/AnuPpuccin/blob/main/snippets/notion-cards.css

---

cover:: ![[Snippets/3f9da8e93b848c205eaa8f1049b09579_MD5.png]]

```css
/* AGPLv3 License
Notion-Styled Kanban
Author: AnubisNekhet
Note: If you decide to implement it in your theme or redistribute it, please keep this comment (Especially for *certain* individuals who may try to rebrand it as their own :))
Support me: https://buymeacoffee.com/AnubisNekhet
*/
body.theme-light {
  --notion-kanban-card: var(--background-primary);
  --notion-kanban-card-hover: var(--background-primary-alt);
  --notion-kanban-darken: var(--background-primary);
  --notion-kanban-darken-hover: var(--background-primary-alt);
}

body.theme-dark {
  --notion-kanban-card: var(--color-base-30);
  --notion-kanban-card-hover: var(--color-base-35);
  --notion-kanban-darken: rgba(var(--ctp-crust, 0, 0, 0), 0.3);
  --notion-kanban-darken-hover: rgba(var(--ctp-crust, 0, 0, 0), 0.2);
}

body {
  --kanban-transition: 100ms ease-out 0s;
}
body .kanban-plugin__lane {
  background-color: transparent;
  border: none;
  border-radius: 0;
}
body .kanban-plugin__lane .kanban-plugin__lane-header-wrapper {
  border-bottom: none;
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-header-wrapper
  .kanban-plugin__lane-grip {
  color: var(--text-muted);
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-header-wrapper
  .kanban-plugin__lane-grip:hover {
  color: var(--text-normal);
  background-color: var(--background-modifier-hover);
  border-radius: var(--radius-s);
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-header-wrapper
  .kanban-plugin__lane-title {
  flex-grow: 0;
  width: auto;
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-header-wrapper
  .kanban-plugin__lane-title
  .kanban-plugin__lane-title-text {
  flex-grow: 0;
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-header-wrapper
  .kanban-plugin__lane-settings-button-wrapper {
  opacity: 0;
  transition: opacity var(--kanban-transition);
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-header-wrapper
  .kanban-plugin__lane-settings-button-wrapper
  .kanban-plugin__lane-settings-button
  .kanban-plugin__icon {
  rotate: 90deg;
}
body
  .kanban-plugin__lane:has(.kanban-plugin__placeholder:only-child):not(
    :has(.kanban-plugin__item)
  )
  .kanban-plugin__item-button-wrapper {
  padding: 0;
}
body
  .kanban-plugin__lane:has(.kanban-plugin__placeholder:only-child):not(
    :has(.kanban-plugin__item)
  )
  .kanban-plugin__item-button-wrapper
  .kanban-plugin__new-item-button {
  padding: 0 10px;
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items.kanban-plugin__scroll-container.kanban-plugin__vertical {
  background-color: transparent;
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__placeholder {
  border: none;
  height: 5px;
  margin-bottom: 0;
  margin-top: 0;
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item {
  border: none;
  box-shadow: rgba(15, 15, 15, 0.1) 0px 0px 0px 1px, rgba(15, 15, 15, 0.1) 0px 2px
      4px;
  transition: background var(--kanban-transition) !important;
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item.is-complete
  .kanban-plugin__item-markdown {
  text-decoration: line-through;
  color: var(--text-faint);
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item
  .kanban-plugin__item-content-wrapper {
  background: var(--notion-kanban-card);
  transition: background var(--kanban-transition) !important;
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item
  .kanban-plugin__item-content-wrapper
  .kanban-plugin__item-title-wrapper {
  background: var(--notion-kanban-darken);
  transition: background var(--kanban-transition) !important;
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item
  .kanban-plugin__item-content-wrapper
  .kanban-plugin__item-title-wrapper
  .kanban-plugin__item-prefix-button-wrapper {
  margin-right: 6px;
  box-shadow: rgba(15, 15, 15, 0.1) 0px 0px 0px 1px, rgba(15, 15, 15, 0.1) 0px 2px
      4px;
  border-radius: 3px;
  background: var(--notion-kanban-card);
  transition: background var(--kanban-transition) !important;
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item
  .kanban-plugin__item-content-wrapper
  .kanban-plugin__item-title-wrapper
  .kanban-plugin__item-prefix-button-wrapper:hover {
  transition: background var(--kanban-transition) !important;
  background: var(--notion-kanban-card-hover);
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item
  .kanban-plugin__item-content-wrapper
  .kanban-plugin__item-title-wrapper
  .kanban-plugin__item-prefix-button-wrapper:hover
  .kanban-plugin__item-prefix-button {
  background-color: transparent;
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item
  .kanban-plugin__item-content-wrapper
  .kanban-plugin__item-title-wrapper
  .kanban-plugin__item-prefix-button-wrapper
  .kanban-plugin__item-prefix-button {
  left: 0;
  background-color: var(--background-primary);
  padding: var(--size-2-3);
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item
  .kanban-plugin__item-content-wrapper
  .kanban-plugin__item-postfix-button-wrapper {
  box-shadow: rgba(15, 15, 15, 0.1) 0px 0px 0px 1px, rgba(15, 15, 15, 0.1) 0px 2px
      4px;
  border-radius: 3px;
  background-color: var(--notion-kanban-card);
  opacity: 0;
  transition: opacity var(--kanban-transition), background-color var(--kanban-transition);
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item
  .kanban-plugin__item-content-wrapper
  .kanban-plugin__item-postfix-button-wrapper:hover {
  background-color: var(--notion-kanban-card-hover);
  transition: background-color var(--kanban-transition);
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item
  .kanban-plugin__item-content-wrapper
  .kanban-plugin__item-postfix-button-wrapper:hover
  .kanban-plugin__item-postfix-button {
  background-color: transparent;
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item
  .kanban-plugin__item-content-wrapper
  .kanban-plugin__item-postfix-button-wrapper
  .kanban-plugin__item-postfix-button {
  right: 0;
  padding: var(--size-2-3);
  background-color: var(--background-primary);
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item
  .kanban-plugin__item-content-wrapper
  .kanban-plugin__item-postfix-button-wrapper
  .kanban-plugin__item-postfix-button
  .kanban-plugin__icon {
  rotate: 90deg;
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item:hover {
  transition: background var(--kanban-transition) !important;
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item:hover
  .kanban-plugin__item-content-wrapper {
  transition: background var(--kanban-transition) !important;
  background-color: var(--notion-kanban-card-hover);
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item:hover
  .kanban-plugin__item-content-wrapper
  .kanban-plugin__item-title-wrapper {
  transition: background var(--kanban-transition) !important;
  background-color: var(--notion-kanban-darken-hover);
}
body
  .kanban-plugin__lane
  .kanban-plugin__lane-items
  .kanban-plugin__item-wrapper
  .kanban-plugin__item:hover
  .kanban-plugin__item-content-wrapper
  .kanban-plugin__item-postfix-button-wrapper {
  opacity: 1;
  transition: opacity var(--kanban-transition), background-color var(--kanban-transition);
}
body .kanban-plugin__lane .kanban-plugin__item-button-wrapper {
  border-top: none;
  padding: 0;
}
body
  .kanban-plugin__lane
  .kanban-plugin__item-button-wrapper
  .kanban-plugin__new-item-button {
  justify-content: flex-start;
  color: transparent;
  box-shadow: none;
  border: none;
  background: transparent;
}
body
  .kanban-plugin__lane
  .kanban-plugin__item-button-wrapper
  .kanban-plugin__new-item-button:hover {
  background: var(--background-modifier-hover);
}
body
  .kanban-plugin__lane
  .kanban-plugin__item-button-wrapper
  .kanban-plugin__new-item-button:hover
  .kanban-plugin__item-button-plus {
  color: var(--text-normal);
}
body
  .kanban-plugin__lane
  .kanban-plugin__item-button-wrapper
  .kanban-plugin__new-item-button
  .kanban-plugin__item-button-plus {
  color: var(--text-muted);
}
body
  .kanban-plugin__lane
  .kanban-plugin__item-button-wrapper
  .kanban-plugin__new-item-button
  .kanban-plugin__item-button-plus::after {
  content: " New";
}
body .kanban-plugin__lane .kanban-plugin__item-form {
  border-top: none;
}
body
  .kanban-plugin__lane:hover
  .kanban-plugin__lane-header-wrapper
  .kanban-plugin__lane-grip {
  opacity: 1;
  transition: opacity var(--kanban-transition);
}
body
  .kanban-plugin__lane:hover
  .kanban-plugin__lane-header-wrapper
  .kanban-plugin__lane-settings-button-wrapper {
  opacity: 1;
  transition: opacity var(--kanban-transition);
}
body
  .kanban-plugin__drag-container
  .kanban-plugin__item-wrapper
  .kanban-plugin__item {
  border: none;
  box-shadow: rgba(15, 15, 15, 0.1) 0px 0px 0px 1px, rgba(15, 15, 15, 0.1) 0px 2px
      4px;
}
body .kanban-plugin__item-input {
  background-color: transparent;
}
```
