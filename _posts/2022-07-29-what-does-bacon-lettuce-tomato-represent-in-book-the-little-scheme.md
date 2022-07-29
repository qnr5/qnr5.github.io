---
layout: post
title: "The Little Scheme 中 bacon lettuce tomato 代表什么"
categories: Scheme
---

在《The Little Scheme》中，(bacon lettuce tomato)到底代表什么，把我绕得够晕，总算在最清醒的时候，给琢磨透了。

先定义一个rember函数用于remove member。
```scheme
(define rember
  (lambda (a lat)
    (cond
     ((null? lat) (quote ()))
     (else (cond
            ((eq? (car lat) a) (cdr lat))
            (else (cons (car lat) (rember a (cdr lat)))))))))
;; (rember 'and '(bacon lettuce and tomato))
;; (bacon lettuce tomato)
;; 测试成功
```
求：当a为and，lat为 (bacon lettuce and tomato)时， (rember a lat)值是什么？

分解步骤，可以帮助理解这个很绕的问题。
<pre>
A
when a   and
when lat (bacon lettuce and tomato)
(cons 'bacon B)

B
when a   and
when lat (lettuce and tomato)
(cons 'lettuce C)

C
when a   and
when lat (and tomato)
(tomato)
</pre>

由C步骤往上看，把(rember a (cdr lat))记作Fn：

(tomato)代表lat为(and tomato)时，C=F3的值；

(lettuce tomato)代表lat为(lettuce and tomato)时，F2=lettuce+F3的值；

(bacon lettuce tomato)代表lat为(bacon lettuce and tomato)时，F1=bacon+F2的值。

找到某种特定形式作为记号，可以方便理解教程的逻辑。
