# 查找漏洞ret的if判断
受gitea1.4那个miss掉的return导致rce的启发，写了个query查询类似这种逻辑错误。由于没有特别好抽象的条件，我只能用"err"来大致区分错误判断，如果变量命名不包含"err"，显然这个query就没有用了，不顾根据命名惯例一般都会带"err"。

## query
```
import go
import semmle.go.Stmt
import semmle.go.Expr
 
from IfStmt ifst
where (ifst.getCond().toString().indexOf("err") >= 0 or ifst.getCond().toString().indexOf("nil") >= 0) and
not exists(ReturnStmt retst | retst.getParent*() = ifst)

select ifst
```