# Latex 入门

``` shell
xelatex *.tex
bibtex *.tex
xelatex *.tex
xelatex *.tex
```

$\mathbb{Z}$

$$
 \mathbb{a}  =  \mathbf{abc} 
$$

$a,b,c \in \mathbb{R}$

$\mathbf{w} \in \mathbb{R}^{d}, \mathbf{x} \in \mathbb{R}^d$

``` latex
\begin{figure}[h]
    \centering
    \includegraphics[width=0.75\textwidth]{mesh}
    \caption{A nice plot.}
    \label{fig:mesh1}
\end{figure}
```

在这段 LaTeX 代码中，`[h]` 是一个浮动体放置选项，用来指定图形的位置。具体来说：

- `[h]` 表示 "here"，即尽可能在当前位置放置图形。
- 除了 `[h]` 之外，还有其他几个选项可以使用：
  - `[t]` 表示 "top"，即将图形放置在页面的顶部。
  - `[b]` 表示 "bottom"，即将图形放置在页面的底部。
  - `[p]` 表示 "page"，即将图形放置在一个单独的浮动页上。
  - `[H]` 表示强制图形放置在当前位置（需要使用 `\usepackage{float}` 宏包）。

通常，这些选项可以组合使用，比如 `[htbp]`，表示 LaTeX 可以选择最合适的位置从这里、顶部、底部或单独的页面中进行放置。

## 见 overleaf 的 google account 账号


## 应该还有一些公式