---
setup: |
  import Layout from '../../layouts/BlogPost.astro'
  import Cool from '../../components/Author.astro'
title: Hello, world!
publishDate: 2 July 2022
name: Mohammad Yousuf Minhaj Zia
value: 128
description: Welcome to my journal! What is this about?
---

<Cool name={frontmatter.name} href="https://github.com/yzia2000" client:load />

Hi! This is my first journal entry. I created this journal because trying to
create great blog posts is hard and decision paralysis or procrastination are
not great places to be in. This will be raw and informal. Will record events
and ideas so I do not forget.

On a complete side note, this journal was a means for me to try astro. Been
watching a ton of [great videos](https://youtu.be/fp3mYVoMN7w) about it and it
is to my understanding that the creators of the project are fantastic
engineers. So far the experience has been extremely fluid. Greatest concern is
how hard it is to find neovim plugins for it. If you want to dev in neovim, add
this autocmd along with the astro-ls neovim lsp integration: 
```vimscript
autocmd BufRead,BufEnter *.astro set filetype=astro 
```

Can't wait to dive deeper into partial hydration and some SSR. Where should I deploy this?
Maybe netlify or vercel? DM me on twitter if you wanna chat
