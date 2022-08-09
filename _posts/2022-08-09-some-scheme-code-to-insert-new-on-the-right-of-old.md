---
title: 一段scheme代码，在“旧”右边插入“新”
---
```scheme
(define tinsertR*
  (lambda (new old l)
    (cond
     ((null? l) (quote ()))
     ((atom? (car l))
      (cond
       ((eq? (car l) old) (cons (car l) (cons new (tinsertR* new old (cdr l)))))
       (else (cons (car l) (tinsertR* new old (cdr l))))))
     (else (cons (tinsertR* new old (car l)) (tinsertR* new old (cdr l)))))))
;; perfect and wonderful
```
```scheme
(tinsertR* 'roast 'chuck
           '((how much (wood))
             could
             ((a (wood) chuck))
             (((chuck)))
             (if (a) ((wood chuck)))
             could chuck wood))
;; test
```
```scheme
((how much (wood))
 could
 ((a (wood) chuck roast))
 (((chuck roast)))
 (if (a) ((wood chuck roast)))
 could chuck roast wood)
;; output
```
注：以上代码，均为《The Little Schemer》第四版中的教学内容，该书英文版ISBN书号为：0-262-56099-2，只有亚马逊才有。代码是我学懂后自己写的，和书中示例代码吻合，开心，所以留点印迹。

![The Little Schemer](pics/The_Little_Schemer_English_version.png)
