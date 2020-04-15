# 根据类名查找所有子类

在java中，包含完整包名的类名可以区分不同的类，比如`javax.el.ValueExpression`，在codeql for java 中，我也可以这样来精确描述一个类。所以查询它的所有子类，我可以写成
```
import java

from Class parent, Class son
where parent.getQualifiedName()="javax.el.ValueExpression" and
son.hasSupertype*(parent)
select parent, son
```
或者
```
import java

from Class parent, Class son
where parent.getQualifiedName()="javax.el.ValueExpression" and
parent.hasSubtype*(son)
select parent, son
```
