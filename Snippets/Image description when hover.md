↪[Collection](Collection.md)

# Image description when hover

---

- author:: sailKite
- source:: https://discord.com/channels/686053708261228577/694233507500916796/1169731141813674075

---

cover:: ![[Snippets/f037ec25f820fcf1276a753045ee9b5f_MD5.gif]]

```css
/*
author: sailKite
source: https://discord.com/channels/686053708261228577/694233507500916796/1169731141813674075
*/

.internal-embed.image-embed {
  position: relative;

  &:hover::after {
    content: attr(alt);
    display: block;
    position: absolute;
    background-color: var(--background-primary);
    border: 1px solid var(--color-base-30);
    border-radius: var(--size-2-2);
    padding: 0.5em;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
}
```

---

## Usage

```md
![[image 01.jpg|Lorem, ipsum dolor sit amet consectetur, adipisicing elit.]]
```
