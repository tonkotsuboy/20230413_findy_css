---
marp: true
theme: kano
---

<!--
_class: title
-->

おまけ

---


<!--
_class: title
-->

# セレクタをまとめて指定したい

`:is()`

---

# 複数のセレクタをまとめて指定したい

`.section1`と`.section2`の`a`要素が
hover したとき、focus したときの両方にスタイルを当てたい

```html
<section class="section1">
  <a>Link1</a>
</section>
<section class="section2">
  <a>Link2</a>
</section>
<section class="section3">
  <a>Link3</a>
</section>
```

---

# 従来： 長々としたコードを書いていた

```css
.section1 a:hover,
.section1 a:focus,
.section2 a:hover,
.section2 a:focus {
  color: lightpink;
}
```

---

# 現在：`:is()` で簡潔に書ける

```css
:is(.section1, .section2) a:is(:hover, :focus) {
  color: lightpink;
}
```

---

# `:not()`でも複数セレクタの指定が可能に


`.a`でも`.b`でもない`p`要素だけ色を変える

▼ 従来

```css
p:not(.foo):not(.bar) {
  color: red;
}
```

▼ 現在

```css
p:not(.foo, .bar) {
  color: red;
}
```

---

# `:not()`でも複数セレクタの指定が可能に

```html
<p class="a">A</p>
<p class="b">B</p>
<p>C</p>
```

`.a`でも`.b`でもない`p`要素だけ色を変える現在の方法




---

<!--
_class: title
-->

# TAB キーでのときだけ<br>フォーカスを当てたい

`:focus-visble`

---

- クリック時にはフォーカスを当てくない
- TAB キーでのみフォーカスを当てたい

---

# :focus は NG

button の場合

- TAB キーでフォーカス：フォーカスがあたる 👎
- クリック時：フォーカスがあたる 👍

```css
.button:focus {
  outline: 4px solid black;
  outline-offset: 4px;
}
```

---

# 従来: JavaScript を使っていた

```js
let keyboardFocused = false;

document.addEventListener("keydown", (event) => {
  keyboardFocused = true;
});

document.addEventListener("mousedown", (event) => {
  keyboardFocused = false;
});

document.addEventListener("focusin", (event) => {
  if (keyboardFocused) {
    event.target.classList.add("focus-visible-active");
  }
});

document.addEventListener("focusout", (event) => {
  event.target.classList.remove("focus-visible-active");
});
```

---

# :focus-visible は

button の場合

- TAB キーでフォーカス：フォーカスがあたる 👍
- クリック時：フォーカスがあたらない 👍

```css
.button:focus-visible {
  outline: 4px solid black;
  outline-offset: 4px;
}
```

---

# デモ

---

# outline の角丸は、2023 年 3 月から全ブラウザ対応 💐

