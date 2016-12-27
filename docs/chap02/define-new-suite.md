# 定义新的suite

有多种定义 suite definition 的方法，参看 [Definition creation strategies](https://software.ecmwf.int/wiki/display/ECFLOW/Definition+creation+strategies#strategy)。

本教程介绍下面两种方式：

* 文本方法
* Python方法

## 文本方法

创建 test.def

```bash
windroc@ubuntu:~/course$ vim test.def
```

文本内容

```text
# Definition of the suite test
suite test
   edit ECF_HOME "$HOME/course"  # replace '$HOME' with the path to your home directory
   task t1
endsuite
```

译者注：

> 与之前SMS的定义方式相同，只需要修改变量名，将SMS_XXX修改为 ECF_XXX。

上述文件包含一个名为 test 的 suite 的 suite definition，该 suite 包含一个名为 t1 的 task。

下面逐行解释含义

1. 该行为注释。在 # 后到行尾之间的所有字符都会被忽略。
2. 定义一个名为 test 的新的 suite。
3. 定义一个 ecflow 变量（[variable](https://software.ecmwf.int/wiki/display/ECFLOW/Glossary#term-variable)），叫做 ECF_HOME。该变量定义定义名为 test 的 suite 可以再哪里找到所有的 unix 文件。余下的课程中，所有的文件名都相对于该目录。确保用你的 home 目录替换 $HOME。
4. 定义一个名为 t1 的 task。
5. [endsuite](https://software.ecmwf.int/wiki/display/ECFLOW/Definition+file+Grammar#grammar-token-endsuite) 结束名为 test 的 suite 的定义。

## python方法

创建一个 python 文件，例如命名为 test.py:

```python
#!/usr/bin/env python2.7
import os
import ecflow 
   
print "Creating suite definition"   
defs = ecflow.Defs()
suite = defs.add_suite("test")
suite.add_variable("ECF_HOME", os.path.join(os.getenv("HOME"),  "course"))
suite.add_task("t1")
```

运行脚本

```bash
windroc@ubuntu:~/course$ python test.py 
Creating suite definition
```

接下来的所有 Python 例子都应该用这种方式运行。

## Emos方法

译者注：

> 本方法未经测试

```python
#!/usr/bin/env python2.7
import os
import sys
sys.path.append('/home/ma/emos/def/o/def')
from ecf import *
   
print "Creating suite definition"   
defs = Defs().add(
Suite("test").add(
Variable("ECF_HOME", os.path.join(os.getenv("HOME"),  "course")),
Task("t1"), ))
print defs
```

## 任务

1. 尝试测试两种方法，后续例子将只用python接口
2. 创建并编辑 suite definition 文件