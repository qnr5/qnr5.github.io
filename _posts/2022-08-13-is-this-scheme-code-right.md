---
title: 一段scheme代码，求数字表达式的值
---
```scheme
;; knew
(define addl
  (lambda (n)
    (+ n 1)))
(addl 3)
(define subl
  (lambda (n)
    (- n 1)))
(subl 4)
(define o+
  (lambda (n m)
    (cond
     ((zero? m) n)
     (else (addl (o+ n (subl m)))))))
(define ×
  (lambda (n m)
    (cond
     ((zero? m) 0)
     (else (o+ n (× n (subl m)))))))
(× 5 6)
(define ↑
  (lambda (n m)
    (cond
     ((zero? m) 1)
     (else (× n (↑ n (subl m)))))))
(↑ 3 3)

(define t-1st-sub-exp
  (lambda (aexp)
    (car aexp)))
(define t-2nd-sub-exp
  (lambda (aexp)
    (car (cdr aexp))))
(define t-operator
  (lambda (aexp)
    (car aexp)))
```
```scheme
(define qvalue
  (lambda (nexp)
    (cond
     ((atom? nexp) nexp)
     ((eq? (t-operator nexp) (quote +))
      (o+ (qvalue (t-1st-sub-exp nexp)) (qvalue (t-2nd-sub-exp nexp))))
     ((eq? (t-operator nexp) (quote ×))
      (×  (qvalue (t-1st-sub-exp nexp)) (qvalue (t-2nd-sub-exp nexp))))
     (else
      (↑ (qvalue (t-1st-sub-exp nexp)) (qvalue (t-2nd-sub-exp nexp)))))))
(qvalue '(o+ 3 (× 5 (↑ 3 2))))
;; Exception in zero?: o+ is not a number
```
《The Little Schemer》 (page 106) 书中示例如上，似乎并未实现求值的能力。可能接下来的章节还有后续修改，暂时记一笔疑惑。
