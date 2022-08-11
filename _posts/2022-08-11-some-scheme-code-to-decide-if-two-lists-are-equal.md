---
title: 一段scheme代码，检验两个list是否相同
---
```scheme
;; my code
(define teqan?
  (lambda (l1 l2)
    (cond
     ((and (null? l1) (null? l2)))
     ((or (and (atom? l1) (not (atom? l2))) (and (not (atom? l1)) (atom? l2))) #f) ;只有一个为atom则不等
     ((or (and (null? l1) (not (null? l2))) (and (not (null? l1)) (null? l2))) #f) ;只有一个为空表则不等
     ((atom? (car l1))
      (cond
       ((eq? (car l1) (car l2)) (teqan? (cdr l1) (cdr l2)))
       (else #f)))
     (else (and (teqan? (car l1) (car l2)) (teqan? (cdr l1) (cdr l2)))))))
```
```scheme
;; 测试用例，皆通过
(teqan? '(a 1 (x y) *)
        '(a 1 (x y) *)) ;#t

(teqan? '(a 1 (x y))
        '(a 1 *)) ;#f

(teqan? '()
        '(123)) ;#f

(teqan? '(ab (c d (ef) gh) i)
        '(ab (c d (ef) gh) i)) ;#t

(teqan? '(ab (c d (ef gh) i))
        '(some (noodle rice (cola spirits) water))) ;#f

(teqan? '(天 時 (地 (利)) (ren he))
        '(天 時 (地 (利)) (ren he))) ;#t

(teqan? '(一 去 二 三 里)
        '(烟 村 四 五 家)) ;#f
```

```scheme
;; code in the book the_little_schemer
(define eqan?
  (lambda (a1 a2)
    (cond
     ((and (number? a1) (number? a2)) (= a1 a2))
     ((or (number? a1) (number? a2)) #f)
     (else (eq? a1 a2)))))

;; (eqan? '3 '3) ;#t
;; (eqan? 'sth '3) ;#f

(define eqlist?
  (lambda (l1 l2)
    (cond
     ((and (null? l1) (null? l2)) #t)
     ((and (null? l1) (atom? (car l2))) #f)
     ((null? l1) #f) ;why

     ((and (atom? (car l1)) (null? l2)) #f)
     ((and (atom? (car l1)) (atom? (car l2)))
      (and (eqan? (car l1) (car l2))
           ;; eqan? 指对比两个atom是否相同的函数，书中预设
           ;; teqan?是对比两个list是否相同的函数，它们不同
           (eqlist? (cdr l1) (cdr l2))))
     ((atom? (car l1)) #f)

     ((null? l2) #f)
     ((atom? (car l2)) #f)

     (else
      (and (eqlist? (car l1) (car l2))
           (eqlist? (cdr l1) (cdr l2)))))))
```
```scheme
;; 测试用例，皆通过
(eqlist? '(a 1 (x y) *)
         '(a 1 (x y) *)) ;#t

(eqlist? '(a 1 (x y))
         '(a 1 *)) ;#f

(eqlist? '()
         '(123)) ;#f

(eqlist? '(ab (c d (ef) gh) i)
         '(ab (c d (ef) gh) i)) ;#t

(eqlist? '(ab (c d (ef gh) i))
         '(some (noodle rice (cola spirits) water))) ;#f

(eqlist? '(天 時 (地 (利)) (ren he))
         '(天 時 (地 (利)) (ren he))) ;#t

(eqlist? '(一 去 二 三 里)
         '(烟 村 四 五 家)) ;#f
```
