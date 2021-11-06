---
title: เราสามารถ bind style ใน Vue ได้แล้วนะ
description: ชีวิตดี๊ดีเมื่อเราไม่จำเป็นต้องใช้ inline style มากนัก
date: 2021-11-06
tags:
  - vue
  - frontend
  - css
layout: layouts/post.njk
---
หลังจากที่ไม่ได้แตะ Vue มานานเลย ทำให้พลาดอะไรไปหลายอย่างมาก โดยเฉพาะ​ Vue 3 ที่ features เพิ่มมาเยอะเหมือนกัน อย่างตอนนี้เราสามารถ bind style กับ Vue ได้แล้วนะครับ

ถ้าเป็นเมื่อก่อนโค้ดของเราจะเป็นประมาณนี้
```html
<template>
  <div :style="style">
     This is dynamic
  </div>
</template>
<script>
export default {
  computed: {
    style() {
      // Pretend that it is dynamic.
      return {
        color: "rgb(12,18,23)"
      }
    }
  }
}
</script>
```

แต่ตอนนี้เราสามารถทำแบบนี้ได้
```html
<template>
  <div class="styled">
    Styled
   </div>
</template>
<script>
  export default {
    computed: {
      color() {
        return `rgb(12,18,23)`
      }
    }
  }
</script>
<style>
  .styled {
    color: v-bind(color)
  }
</style>
```

ถ้าทำแบบนี้โค้ดเราจะ expressive มากขึ้น ประมาณว่ารู้ว่าตัวแปรนี้เอาไว้ทำ css นะ ไม่ต้อง inline ตลอด Vue ใช้ความสามารถของ CSS Variable เข้ามาช่วย แต่ก็จะมีตัว CSS Variable ติดมาด้วยตอนนี้ inspect

แต่อย่าลืมว่าอันนี้ของ Vue 3 นะครับ