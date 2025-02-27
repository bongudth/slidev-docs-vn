# Cú pháp Markdown

Slide được viết trong **một file markdown duy nhất** (theo mặc định là `./slides.md`). 

Bạn có thể sử dụng [các tính năng Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) như bình thường, với sự hỗ trợ bổ sung của các component HTML và Vue. Tạo style bằng [Windi CSS](https://windicss.org) cũng được hỗ trợ. Sử dụng dấu `---` được đệm bằng một dòng mới để tách các slide của bạn.

~~~md
# Slidev

Hello, World!

---

# Page 2

Directly use code blocks for highlighting

//```ts
console.log('Hello, World!')
//```

---

# Page 3

You can directly use Windi CSS and Vue components to style and enrich your slides.

<div class="p-3">
  <Tweet id="20" />
</div>
~~~

## Front Matter & Layout

Bạn có thể chỉ định layout và siêu dữ liệu khác cho mỗi slide bằng cách chuyển đổi các dấu phân cách thành [khối front matter](https://jekyllrb.com/docs/front-matter/). Mỗi front matter bắt đầu bằng dấu ba gạch ngang và kết thúc bằng dấu gạch ngang khác. Văn bản giữa chúng là các đối tượng dữ liệu ở định dạng [YAML](https://www.cloudbees.com/blog/yaml-tutorial-everything-you-need-get-started/). Ví dụ:

~~~md
---
layout: cover
---

# Slidev

This is the cover page.

---
layout: center
background: './images/background-1.png'
class: 'text-white'
---​

# Page 2

This is a page with the layout `center` and a background image.

---

# Page 3

This is a default page without any additional metadata.
~~~

Tham khảo [customization](/custom/) để biết thêm chi tiết.

## Code Blocks

Một lý do lớn mà tôi xây dựng Slidev là làm cho code của tôi trông vừa phải trong các slide. Vì vậy, đúng như bạn mong đợi, bạn có thể sử dụng khối code Markdown để làm nổi bật code của mình.

~~~ts
//```ts
console.log('Hello, World!')
//```
~~~

### Đánh dấu dòng

Để đánh dấu các dòng cụ thể, chỉ cần thêm số dòng trong dấu ngoặc nhọn `{}`. Số dòng bắt đầu đếm từ 1.

~~~ts
//```ts {2,3}
function add(
  a: Ref<number> | number,
  b: Ref<number> | number
) {
  return computed(() => unref(a) + unref(b))
}
//```
~~~

Để thay đổi vùng đánh dấu trong nhiều bước, bạn có thể sử dụng dấu `|` để tách chúng. Ví dụ

~~~ts
//```ts {2-3|5|all}
function add(
  a: Ref<number> | number,
  b: Ref<number> | number
) {
  return computed(() => unref(a) + unref(b))
}
//```
~~~

Đầu tiên, điều này sẽ làm nổi bật `a: Ref<number> | number` và `b: Ref<number> | number`, và sau đó là `return computed(() => unref(a) + unref(b))` sau một cú nhấp chuột, và cuối cùng là toàn bộ khối. Tìm hiểu thêm trong [hướng dẫn về animation click](/guide/animations).

### Trình soạn thảo Monaco

Bất cứ khi nào bạn muốn thực hiện một số sửa đổi trong bản trình bày, chỉ cần thêm `{monaco}` sau ngôn ngữ id - nó biến khối thành một trình soạn thảo Monaco đầy đủ tính năng!

~~~ts
//```ts {monaco}
console.log('HelloWorld')
//```
~~~

Tìm hiểu thêm về [configuring Monaco](/custom/config-monaco).

## Embedded Styles

Bạn có thể sử dụng thẻ `<style>` trong Markdown của mình trực tiếp để ghi đè các kiểu cho **slide hiện tại**.

```md
# This is Red

<style>
h1 {
  color: red
}
</style>

---

# Next slide is not affected
```

Thẻ `<style>` trong Markdown luôn [scoped](https://vue-loader.vuejs.org/guide/scoped-css.html). TĐể ghi đè kiểu toàn cục, hãy xem [phần tùy chỉnh](/custom/directory-structure#style).

Được cung cấp bởi [Windi CSS](https://windicss.org), bạn có thể sử dụng trực tiếp css và [directives](https://windicss.org/features/directives.html) lồng nhau (ví dụ: `@apply`)

```md
# Slidev

> Hello `world`

<style>
blockquote {
  code {
    @apply text-teal-500 dark:text-teal-400;
  }
}
</style>
```

## Lưu ý

Bạn cũng có thể ghi chú cho mỗi slide. Chúng sẽ hiển thị ở [Chế độ trình bày](/guide/presenter-mode) để bạn tham khảo trong khi thuyết trình.

Trong Markdown, khối comment cuối cùng trong mỗi slide sẽ được coi là ghi chú.

~~~md
---
layout: cover
---

# Page 1

This is the cover page.

<!-- This is a note -->

---

# Page 2

<!-- This is NOT a note because it precedes the content of the slide -->

The second page

<!--
This is another note
-->
~~~

## Icons

Slidev cho phép bạn có quyền truy cập vào hầu hết tất cả các bộ icon mã nguồn mở phổ biến **trực tiếp** trong markdown của bạn. Được cung cấp bởi [`vite-plugin-icons`](https://github.com/antfu/vite-plugin-icons) và [Iconify](https://iconify.design/).

Việc đặt tên theo chuyển đổi của [Iconify](https://iconify.design/) `{collection-name}-{icon-name}`. Ví dụ:

- `<mdi-account-circle />` - <mdi-account-circle /> từ [Material Design Icons](https://github.com/Templarian/MaterialDesign)
- `<carbon-badge />` - <carbon-badge /> từ [Carbon](https://github.com/carbon-design-system/carbon/tree/main/packages/icons)
- `<uim-rocket />` - <uim-rocket /> từ [Unicons Monochrome](https://github.com/Iconscout/unicons)
- `<twemoji-cat-with-tears-of-joy />` - <twemoji-cat-with-tears-of-joy /> từ [Twemoji](https://github.com/twitter/twemoji)
- `<logos-vue />` - <logos-vue /> từ [SVG Logos](https://github.com/gilbarbara/logos)
- Và nhiều hơn nữa...

Bạn có thể duyệt và tìm kiếm tất cả các icon có sẵn với [Icônes](https://icones.js.org/).

### Styling Icons

Bạn có thể tạo kiểu cho các icon giống như các element HTML khác. Ví dụ:

```html
<uim-rocket />
<uim-rocket class="text-3xl text-red-400 mx-2" />
<uim-rocket class="text-3xl text-orange-400 animate-ping" />
```

<uim-rocket />
<uim-rocket class="text-3xl text-red-400 mx-2" />
<uim-rocket class="text-3xl text-orange-400 animate-ping ml-2" />

## Slots

> Có hiệu lực từ v0.18

Một số layout có thể cung cấp nhiều điểm đóng góp bằng cách sử dụng [slot được đặt tên của Vue](https://v3.vuejs.org/guide/component-slots.html).

Ví dụ, trong [`two-cols` layout](https://github.com/slidevjs/slidev/blob/main/packages/client/layouts/two-cols.vue), bạn có thể có hai cột bên trái (`default` slot) và bên phải (`right` slot) cạnh nhau.

```md
---
layout: two-cols
---

<template v-slot:default>

# Left

This shows on the left

</template>
<template v-slot:right>

# Right

This shows on the right

<template>
```

<div class="grid grid-cols-2 rounded border border-gray-400 border-opacity-50 px-10 pb-4">
<div>
<h3>Left</h3>
<p>This shows on the left</p>
</div>
<div>
<h3>Right</h3>
<p>This shows on the right</p>
</div>
</div>

Chúng tôi cũng cung cấp cú pháp viết tắt `::name::` cho tên vị trí. Ví dụ sau hoạt động giống hệt như ví dụ trước.

```md
---
layout: two-cols
---

# Left

This shows on the left

::right::

# Right

This shows on the right
```

Bạn cũng có thể chỉ định rõ ràng vị trí mặc định và cung cấp theo thứ tự tùy chỉnh

```md
---
layout: two-cols
---

::right::

# Right

This shows on the right

::default::

# Left

This shows on the left
```

## Cấu hình

Tất cả các cấu hình cần thiết có thể được xác định trong tệp Markdown. Ví dụ:

```md
---
theme: seriph
layout: cover
background: 'https://source.unsplash.com/1600x900/?nature,water'
---

# Slidev

This is the cover page.
```

Tìm hiểu thêm về [cấu hình frontmatter](/custom/#frontmatter-configures).

## LaTeX

Slidev đi kèm với hỗ trợ LaTeX bên ngoài, được cung cấp bởi [KaTeX](https://katex.org/).

<Tweet id="1392246507793915904" />

### Inline

Bao quanh LaTeX của bạn với một ký tự `$` duy nhất ở mỗi bên để hiển thị trong một dòng.

```md
$\sqrt{3x-1}+(1+x)^2$
```

### Block

Sử dụng hai (`$$`) để hiển thị khối. Chế độ này sử dụng các ký hiệu lớn hơn và căn giữa kết quả.

```md
$$
\begin{array}{c}

\nabla \times \vec{\mathbf{B}} -\, \frac1c\, \frac{\partial\vec{\mathbf{E}}}{\partial t} &
= \frac{4\pi}{c}\vec{\mathbf{j}}    \nabla \cdot \vec{\mathbf{E}} & = 4 \pi \rho \\

\nabla \times \vec{\mathbf{E}}\, +\, \frac1c\, \frac{\partial\vec{\mathbf{B}}}{\partial t} & = \vec{\mathbf{0}} \\

\nabla \cdot \vec{\mathbf{B}} & = 0

\end{array}
$$
```

Tìm hiểu thêm: [Demo](https://sli.dev/demo/starter/8) | [KaTeX](https://katex.org/) | [`markdown-it-katex`](https://github.com/waylonflinn/markdown-it-katex)

## Diagrams

Bạn cũng có thể tạo sơ đồ / đồ thị từ mô tả bằng văn bản trong Markdown của mình, được cung cấp bởi [Mermaid](https://mermaid-js.github.io/mermaid).

Code block được đánh dấu là `mermaid` sẽ được chuyển đổi thành digram, ví dụ:

~~~md
//```mermaid
sequenceDiagram
  Alice->John: Hello John, how are you?
  Note over Alice,John: A typical interaction
//```
~~~

Bạn có thể chuyển thêm một đối tượng tùy chọn cho nó để chỉ định tỷ lệ và chia tỷ lệ. Cú pháp của đối tượng là một đối tượng JavaScript theo nghĩa đen, bạn sẽ cần thêm dấu nháy (`'`) cho các chuỗi và sử dụng dấu phẩy (`,`) giữa các khóa.

~~~md
//```mermaid {theme: 'neutral', scale: 0.8}
graph TD
B[Text] --> C{Decision}
C -->|One| D[Result 1]
C -->|Two| E[Result 2]
//```
~~~

Tìm hiểu thêm: [Demo](https://sli.dev/demo/starter/9) | [Mermaid](https://mermaid-js.github.io/mermaid)

## Multiple Entries

> Có hiệu lực từ v0.15

Bạn có thể chia `slides.md` của mình thành nhiều file và sắp xếp chúng theo ý muốn.

`slides.md` :

```md
# Page 1

This is a normal page

---
src: ./subpage2.md
---

<!-- this page will be loaded from './subpage2.md' -->
Inline content will be ignored
```

`subpage2.md` :

```md
# Page 2

This page is from another file
```

### Frontmatter Merging

Bạn có thể cung cấp frontmatters từ cả mục nhập chính và các trang markdown pages. bên ngoài. Nếu có các khóa giống nhau trong chúng, thì những khóa từ **mục nhập chính có mức độ ưu tiên cao hơn**. Ví dụ

`slides.md` :

```md
---
src: ./cover.md
background: https://sli.dev/bar.png
class: text-center
---
```

`cover.md` :

```md
---
layout: cover
background: https://sli.dev/foo.png
---

# Cover

Cover Page
```

They will end up being equivalent of the following page:

```md
---
layout: cover
background: https://sli.dev/bar.png
class: text-center
---

# Cover

Cover Page
```

### Page Reusing

With the multi-entries support, reusing pages could be straightforward. For example:

```yaml
---
src: ./cover.md
---

---
src: ./intro.md
---

---
src: ./content.md
---

---
# reuse
src: ./content.md
---
```
