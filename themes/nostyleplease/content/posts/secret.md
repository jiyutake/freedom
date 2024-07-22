---
title: "secret"
custom_js: [mouse_coords]
date: 2024-07-06T17:06:21-03:00
draft: true
---

This is a somewhat strange post. You might not even be allowed in here. Everything displayed here should be working without any issues whatsoever.

## Headings

# h1

Wow that's really big. as the size of the title even! **Don't** use this on places other than the page title, it would be a bit awkward...

## h2

Not that small i'd say. Use this for most sections in articles.

### h3

Subdivisions.

## Lists
- item
- item

1. item with a cool number
    - *Tricks you into believing this contains really useful information*
2. item with a pair number.. wow
    1. subitem with another number
    4. blaze it (should display as 2 even though it's 4 in the markdown file.)

## Blockquotes
> tif my goat
> --- Vivi, 2024

## Table
What do i even say about this. Have the default example, too much of a hassle to write markdown without Obsidian anyways :P
| Table Heading 1 | Table Heading 2 | Center align    | Right align     | Table Heading 5 |
| :-------------- | :-------------- | :-------------: | --------------: | :-------------- |
| Item 1          | Item 2          | Item 3          | Item 4          | Item 5          |
| Item 1          | Item 2          | Item 3          | Item 4          | Item 5          |
| Item 1          | Item 2          | Item 3          | Item 4          | Item 5          |
| Item 1          | Item 2          | Item 3          | Item 4          | Item 5          |
| Item 1          | Item 2          | Item 3          | Item 4          | Item 5          |

## Code
This shows `Inline` code, useful for putting small commands as `git clone https://github.com/siduck/st`.
This shows code with syntax highlighting 

```scss
@media (prefers-color-scheme: dark) {
  body[a="auto"] { @include dark-appearance; }
  h1#fancy {
    background: linear1-gradient(275deg, #DDDDDD,  #4070AA);
    background: -webkit-linear-gradient(275deg, #DDDDDD,  #4070AA);
  }
}
```

One-liner:
```bash
cd ~; du -sh ~/.cache/ | echo &>/dev/null
```

Sorry, too lazy to fix the width issue, refer to the browser's default way of handling scrollbars.

## Other inline elements

- *this is italic text*
- **this is bold text**
    - ***this is bold and italic together***
- [this is a link](/click_me)
[[Back to top]](#top)

\subtext??\

## Media / Caption

{{< figure 
    src="https://static.wikia.nocookie.net/vocaloid/images/5/50/Ofclboxart_cfm_Hatsune_Miku-illu.png"
    alt="Hatsune Miku"
    caption="Her."
    >}}

[![video](https://i1.ytimg.com/vi/duPJqfKiA78/hqdefault.jpg)](https://www.youtube.com/watch?v=duPJqfKiA78)
<text align='center'>^click it!

## Tex
Inline math: {{< texi `\varphi` >}}

Displayed math: 
{{< texd `\begin{aligned}
\varphi &\Rightarrow \psi \\
\varnothing &\rightarrow A
\end{aligned}` >}}

$$
R_{\mu \nu} - {1 \over 2}g_{\mu \nu}\,R + g_{\mu \nu} \Lambda
= {8 \pi G \over c^4} T_{\mu \nu}
$$

The equation $$(x_i \cdot x_j)^2$$ is called kernel function and is often written as $$k(x_i, x_j)$$

$$
\arg\max_\alpha \sum_j \alpha_j - \frac{1}{2} \sum_{j,k} \alpha_j, \alpha_k y_j y_k (x_j \cdot x_k)
$$

- (The error above is a demo for incorrect formulas.)
- Yeah i stole the default tex demo file
- Yeah it's broken. &nbsp; &nbsp; :(

## Javascript