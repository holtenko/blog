---
title: web.xml配置过程中的常见错误
toc: true
date: 2018-02-24 14:58:29
categories: [Java]
tags: [Java,Spring,Wiki]
---

## The content of element type "web-app" must match

### 问题原因

web.xml中`<web-app>`标签的元素个数和排序规则是有限制的，大多数情况下出现该错误的原因是元素排放顺序有误。

### 解决方法

解决其实也很简单，按照要求将各元素排序即可，具体排序如下：

```xml
<!--
The web-app element is the root of the deployment descriptor for
a web application.
-->
<!ELEMENT web-app (icon?, display-name?, description?, distributable?,
context-param*, filter*, filter-mapping*, listener*, servlet*,
servlet-mapping*, session-config?, mime-mapping*, welcome-file-list?,
error-page*, taglib*, resource-env-ref*, resource-ref*, security-constraint*,
login-config?, security-role*, env-entry*, ejb-ref*,  ejb-local-ref*)>
```
