---
title: 一段scheme代码，检验两个list是否相同
---
```scheme
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
;; 以上为测试用例，测试皆通过
