# 皮卡丘靶场-xss之htmlspecialchars

## 一、基本信息

- 漏洞模块：xss
- 子漏洞：xss之htmlspecialchars
- 工具：浏览器
- 目的：复现漏洞，通过复现漏洞了解xss之htmlspecialchars的原理与完整流程

## 二、漏洞原理

  本身htmlspecialchars()函数是用来转义敏感字符的，比如<、>、&、''、""这种，这个函数默认转义尖括号、取地址符、双引号这些，如果添加了ENT_QUOTES单引号也是可以转义，但是像是javascript:alert(0)这种伪协议还是可以绕过。

## 三、复现步骤

1. 在pikachu平台xss之htmlspecialchars页面输入'onclick='alert(0)'//，点击提交
2. 点击页面上动态加载的文本'onclick='alert(0)'//
3. 页面弹出内容为0的提示框

## 四、结果与总结

- **结果**：成功复现漏洞，得到预期结果。
- **总结**：该种漏洞本质上是转义这种数据处理操作存在一定的局限性，对于javascript:这种伪协议的话处理不了，但这种伪协议本身局限于src、href这类属性场景，这时可采取黑名单/白名单校验，过滤拦截这些伪协议，可以采取过滤和转义双重处理，来提升整体的安全性。

