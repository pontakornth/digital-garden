---
title: ความสวยงามของ Functional Programming
description: มาเล่าความสวยงามของ Functional Programming
date: 2021-07-31
tags:
  - functional
  - programming
layout: layouts/post.njk
---
## Functional Programming มันช่างสวยงาม

มีช่วงนึงพี่ผมเห่อการเรียนภาษา programming ใหม่ ๆ มาก ลองไปหลายตัวตั้งแต่ Rust, Go, Scala ไปเรื่อย ๆ จนไปเจอกับภาษาพวก Racket, Haskell และก็ Clojure ที่เป็นพวก Functional ผมก็ชอบนะ แต่เสียดายที่ไม่รู้ว่าจะเอาไปทำอะไรต่อเท่านั้นแหละ

## ลองอธิบาย Functional Programming มาหน่อยดิ

อ่า ลองคิดว่ามันเป็นการเขียนโปรแกรมที่เราเอาฟังก์ชั่นมาประกอบ ๆ กันจะได้เป็นการทำงานแบบใหม่ดูครับ มันจะอาจจะไม่เห็นภาพเนอะ ลองคิดดูว่า functional programming สามารถทำให้ function เป็นเหมือนกับ ตัวแปรตัวนึงเลย

```typescript
function createAdder(a: number) {
  return function(b: number) {
    return a + b;
  }
}
const addOne = createAdder(1);
console.log(addOne(2)) // 3
```

จะเห็นว่าในบรรทัดที่ 2 มีการ return `function` ออกมา เหมือนกับค่าตัวแปรเลย ถ้่าเราจะสร้างฟังก์ชั่นใหม่ เราก็แค่ใส่ arguement ลงไปให้ฟังก์ชั่นออกมา functional programming ทำให้ function เหมือนกับค่าตัวแปร ดังนั้นเราสามารถใส่ฟังก์ชั่นเป็น arguement ได้เหมือนกัน

```typescript
const numbers = [10, 12, 8, 4, 8];
const greaterThanFour = numbers.filter(n => n > 4);
console.log(greaterThanFour) // [10, 12, 8, 8]
```

ถ้าเราไม่สามารถรับ function เข้ามาใน function ได้ เราอาจจะต้องเขียน for loop มือหงิกมืองอกันแน่ ๆ ยิ่งถ้าใช้อะไรที่ซับซ้อนกว่านี้ ได้ลูปจนสยองแน่นอน


น่าจะพอเห็นข้อดีของการเขียนให้ function เหมือนกับตัวแปรอื่น ๆ แล้วใช่มะ

## Pure Function

อ่าอันนี้เป็นหัวข้อสำคัญของ functional programming มาก ๆ เลย Pure Function เป็น function ที่ให้ผลตาม arguement ที่ใส่เข้าไป และไม่เกิดผลข้างเคียงหรือ side effect แต่อย่างใด Side Effect คือการทำอะไรก็ตามที่อยู่นอกขอบเขตของฟังก์ชั่นเช่น print หรือว่าทำให้ตัวแปรเปลี่ยนค่า เป็นต้น

```typescript
// Any is a sin but I don't care.
function purePush(array: any[], value: any) {
  return [...array, value];
}

function impurePush(array: any[], value: any) {
  array.push(value)
}
```

จะเห็นว่า `purePush` จะไม่เกิด side effect ใด ๆ เพราะว่าเป็นการ return ค่าใหม่ แต่ว่า `impurePush` จะแก้ค่า array ที่ส่งมาใน function


ข้อดีของการไม่มี side effect คือเราสามารถ test function นั้นได้ง่ายมาก ๆ โดยการดู input กับ output โดยที่ไม่ต้องไปกังวลว่าจะเกิดอะไรที่ไม่คาดคิด ชีวิตดี๊ดี

## ความสวยงามของภาษาที่เน้นเขียน functional

เอาจริง ๆ หลายภาษาเริ่มรองรับการเขียนแบบ function มากขึ้นแล้ว เพราะว่าทำให้ชีวิตดี๊ดีจริง ๆ ภาษาที่เขียนแนว functional มักจะมีเครื่องมืออย่าง pattern matching, type, หรือว่า macro ที่ช่วยให้ชีวิตดี๊ดีขึ้นไปอีก

```haskell
map' _ [] = []
map' f (x:xs) = f x : map' f xs
```

โค้ดอันนี้เป็นภาษา haskell ที่ใช้การ map function ครับ คำอธิบายคือถ้าส่ง list เปล่า ๆ มา ก็ให้ list เปล่า ๆ กับไปโดยที่ไม่สนใจ function แต่ถ้าให้ list ที่มีสมาชิก ก็จะใส่ function กับสมาชิกตัวแรก แล้วเอาไปต่อกับ map ที่ทำกับตัวถัดไป


หรือก็จะเป็นการใช้ macro มาต่อกัน

```clojure
(->> students-data
  (fill-na-score 0)
  (filter ่passed?)
  (chart :pie)
  (report))
```

อันนี้ไม่ใช่ code จริง ๆ นะครับ สมมติว่าเรามี `students-data` เป็น list ของข้อมูลนักเรียนที่ทำข้อสอบวิชานึง แล้วเราก็แทนที่ข้อมูลคะแนนที่ขาดไปด้วย 0 แล้วกรองเฉพาะคนที่ผ่าน นำมาทำเป็น pie chart แล้วก็รายงานออกมา จะเห็นว่าโค้ดเหมือนมีการส่งต่อข้อมูลจากบนลงล่าง แบบนี้คือ threading macro ของ Clojure ที่ทำให้เราไม่ต้องเขียนวงเล็บซ้อน ๆ กันหลายชั้น ถ้า Clojure ไม่สามารถรับ function เป็นเหมือนกับค่าตัวแปรจะไม่สามารถทำแบบนี้ได้


ตอนนี้ผมยอมรับว่าไม่ได้มีความรู้เรื่อง functional programming มากนักหรือเขียนภาษาพวกนี้มากนัก เพราะว่าภาษาใหม่ ๆ หรือเวอร์ชั่นใหม่ ๆ ส่วนใหญ่ support functional programming กันอยู่แล้ว แถมก็ไม่ได้่มีงานหรืออะไรที่เหมาะกับการใช้อยู่ดี (ผมทำ frontend ฮะ ถ้าภาษาที่มีงานใกล้เคียงสุดจะเป็น ClojureScript กับ Reason)