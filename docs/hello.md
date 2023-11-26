---
tags:
  - HTML5
  - JavaScript
  - CSS
---


# 1. 简单

换行需要两个空格  
`emoji`:
:smile: :laughing: :dizzy_face: :sob: :cold_sweat: :sweat_smile: :cry: :triumph: :heart_eyes: :relaxed: :sunglasses: :weary: :sweat: :confounded: :flushed: :mask: :innocent: :smiling_imp: :imp: :joy: :fearful: :cold_sweat: :sob: :heart_eyes: :sweat_smile: :cry: :sob: :cold_sweat: :sweat_smile: :cry: :sob: :cold_sweat: :sweat_smile: :cry: :sob: :cold_sweat: :sweat_smile: :cry: :sob: :cold_sweat: :sweat_smile: :cry: :sob: :cold_sweat: :sweat_smile: :cry: :sob: :cold_sweat: :sweat_smile: :cry: :sob: :cold_sweat: :sweat_smile: :cry: :sob: :cold_sweat: :sweat_smile: :cry: :sob: :cold_sweat: :sweat_smile: :cry:

---
加重链接
__[MkDocs]__
  [MkDocs]: https://www.youtube.com/watch?v=Q-YA_dA8C20
---

# 2.数学公式 
$$
\begin{equation}
  x = a_0 + \cfrac{1}{a_1 
          + \cfrac{1}{a_2 
          + \cfrac{1}{a_3 + \cfrac{1}{a_4} } } }
\end{equation}
$$
行内公式 $x = a_0 + \cfrac{1}{a_1 + \cfrac{1}{a_2 + \cfrac{1}{a_3 + \cfrac{1}{a_4} } } }$ 行内公式  
矩阵乘法 $A_{m\times n} \times B_{n\times p} = C_{m\times p}$

# 代码
``` py
print("hello world")
print("hello world")
```
``` py title="bubble_sort.py"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

```{python hl_lines="3 5" linenums="1"}
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
    return items    
```


``` yaml
theme:
  features:
    - content.code.annotate # (1)
```

1.  :man_raising_hand: I'm a code annotation! I can contain `code`, __formatted
    text__, images, ... basically anything that can be written in Markdown.


``` py linenums="1"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```
The `#!python range()` function is used to generate a sequence of numbers.


# 表格
| 1    | 2    | 3    |  
| ---- | ---- | ---- |
| 1    | 2    | 3    |
| 1    | 2    | 3    |
 

# 框
!!! example
    This is an example of a blockquote.
        ``` markdown
        * Sed sagittis eleifend rutrum
        * Donec vitae suscipit est
        * Nulla tempor lobortis orci
        ```


!!! note
    This is an example of a blockquote.
        ``` markdown
        * Sed sagittis eleifend rutrum
        * Donec vitae suscipit est
        * Nulla tempor lobortis orci
        ```
!!! warning
    This is an example of a blockquote.
        ``` markdown
        * Sed sagittis eleifend rutrum
        * Donec vitae suscipit est
        * Nulla tempor lobortis orci
        ```
!!! danger
    This is an example of a blockquote.
        ``` markdown
        * Sed sagittis eleifend rutrum
        * Donec vitae suscipit est
        * Nulla tempor lobortis orci
        ```
!!! bug
    This is an example of a blockquote.
        ``` markdown
        * Sed sagittis eleifend rutrum
        * Donec vitae suscipit est
        * Nulla tempor lobortis orci
        ```
!!! quote
    This is an example of a blockquote.
        ``` markdown
        * Sed sagittis eleifend rutrum
        * Donec vitae suscipit est
        * Nulla tempor lobortis orci
        ```
!!! success
    This is an example of a blockquote.
        ``` markdown
        * Sed sagittis eleifend rutrum
        * Donec vitae suscipit est
        * Nulla tempor lobortis orci
        ```
!!! faq
    This is an example of a blockquote.
        ``` markdown
        * Sed sagittis eleifend rutrum
        * Donec vitae suscipit est
        * Nulla tempor lobortis orci
        ```
!!! abstract
    This is an example of a blockquote.
        ``` markdown
        * Sed sagittis eleifend rutrum
        * Donec vitae suscipit est
        * Nulla tempor lobortis orci
        ```
