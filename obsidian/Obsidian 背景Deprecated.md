# Obsidian 背景废弃

## 可以设置全局背景的 css

``` css
.theme-light .workspace {
    backdrop-filter: brightness(1) blur(5px); /* filter for light mode */
    background-color: transparent;
}
.theme-dark .workspace {
    backdrop-filter: brightness(0.35) blur(5px); /* filter for dark mode */
    background-color: transparent;
}
.horizontal-main-container { /* below is the background image. Change it to whatever you want */
    background: url(https://pic.imgdb.cn/item/66e28445d9c307b7e97ce1b4.png);
    background-size: cover;
}
.workspace-split.mod-root {
    background-color: var(--background-primary);
}

body { 
/* the background-primary makes the main note pane completely transparent. 
You can change it to be semi-transparent if you want. 
I changed background-secondary and divider-width because it
looks a bit cleaner in my opinion. You can delete those modifications if you want.*/
    --background-primary: transparent;
    --background-secondary: transparent;
    --divider-width: 0px;
}
```
