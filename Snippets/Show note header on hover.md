↪[Collection](Collection.md)
# Show note header on hover

___

- author:: sailKite
- source:: https://discord.com/channels/686053708261228577/702656734631821413/1170914511788724254

___

cover:: ![[Snippets/2ec0e8f48505b2c06988b0f5e1273895_MD5.gif]]

```css
/*
author: sailKite
source: https://discord.com/channels/686053708261228577/702656734631821413/1170914511788724254
*/

.workspace-tabs:not(.mod-top) .workspace-tab-header-container {
    height: 0px;
    transition: height 200ms ease-in;

    &:hover {
        height: var(--header-height);
    }

    &::after {
        content: "";
        display: block;
        width: 100%;
        height: var(--size-4-4);
        top: 100%;
        position: absolute;
        z-index: 1;
    }
}
```


