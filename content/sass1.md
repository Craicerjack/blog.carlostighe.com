---
title: Sass1
image: /images/sass.png
imageMeta:
  attribution:
  attributionLink:
featured: true
author: carlos
date: Tue Aug 07 2018 14:54:32 GMT+0100 (IST)
tags:
  - programming
  - html
  - css3
  - sass
---

# Sass

https://sass-lang.com/  

Sass written in Ruby so you need Ruby installed

#### Syntax

`sass` or `scss`. The later is the newer.  
`sass` doesnt use `{}` or `;` it uses `whitespace` and `newlines`  
can comment using `//` but doesnt get compiled  


#### Nesting

You can nest properties under other properties `p { a {}}` becomes `p a {}`  
`&:hover` - compiles to `parent_selector:hover`  - the ampersand gets replaced by the parent selector.   

parent-selector can be used at any stage of the attribute.  

```  
#demo {
    &-child { margin: .5em; }
    &child { margin: .5em; }
    &.child { margin: .5em; }
    & .child { margin: .5em; }
}  

/* compiles to  */
#demo-child { margin: .5em; }
#demochild  { margin: .5em; }
#demo.child { margin: .5em; }
#demo .child { margin: .5em; }
}
```  
