# 通过结构体名找到所有实例化的指针变量

```
import cpp

from Variable var, Struct stru, PointerType ptype

where stru.getName() = "Webs" and
var.getType() = ptype and
ptype.stripType() = stru

select var
```