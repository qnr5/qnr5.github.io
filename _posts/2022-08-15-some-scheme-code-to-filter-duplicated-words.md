---
title: 一段scheme代码，去除重复的单词
---

当收集单词时，常会出现重复现象。去除重复单词，是主动收集单词时的刚需。处理词表前先清除[^a-z]，把非a-z的字符替换为空格。用scheme去除重复单词的代码如下。

```scheme
(define tmember?
  (lambda (a lat)
    (cond
     ((null? lat) #f)
     ((eq? (car lat) a) #t)
     (else (tmember? a (cdr lat))))))

(define tunique
  (lambda (lat)
    (cond
     ((null? lat) (quote ()))
     ((tmember? (car lat) (cdr lat)) (tunique (cdr lat)))
     (else (cons (car lat) (tunique (cdr lat)))))))

(tunique '(
every decision a person makes stems from the person s values and goals people can have many different goals and values fame profit love survival fun and freedom are just some of the goals that a good person might have when the goal is a matter of principle we call that idealism))
```

```scheme
;; output
every decision makes stems from s people can many different values fame profit love survival fun and freedom are just some goals good person might have when the goal is a matter of principle we call that idealism
```
