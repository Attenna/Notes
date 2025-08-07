# 火山引擎 SDK 使用说明

## 📖 目录

1. **前置说明**
2. **SDK 地址**
3. **接口类型与调用步骤**
4. **示例代码**
   - [同步接口](#同步接口)
   - [异步接口](#异步接口)
   - [同步转异步接口](#同步转异步接口)
5. **常见问题**

---

## 1. 前置说明

火山引擎 SDK 提供了多种编程语言的支持，帮助开发者快速集成火山引擎的云服务。

### 接口类型

- **同步接口**：直接返回结果。
- **异步接口**：提交任务后返回 `taskId`，需通过查询接口获取结果。
- **同步转异步接口**：将同步任务转为异步任务，返回 `taskId`。

### 调用步骤

1. 查看接口文档，获取 `Action` 和 `Version`。
	1. 查看接口文档`请求参数-Query`参数中的`Action`及对应`Version`，根据`Action`全局检索`SDK`，找到对应的`example`或参考本文档中的调用示例
2. 根据接口文档构造请求参数。
3. 设置 AK/SK 并运行程序。
4. 调试通过后集成到工程中。

---

## 2. SDK 地址

- **Java**: [volc-sdk-java](https://github.com/volcengine/volc-sdk-java)
- **Python**: [volc-sdk-python](https://github.com/volcengine/volc-sdk-python)
- **Go**: [volc-sdk-golang](https://github.com/volcengine/volc-sdk-golang)
- **PHP**: [volc-sdk-php](https://github.com/volcengine/volc-sdk-php)

---

## 3. 接口类型与调用步骤

### 同步接口

**Action**: `CVProcess`

调用示例：

```java
IVisualService visualService = VisualServiceImpl.getInstance();
visualService.setAccessKey("your ak");
visualService.setSecretKey("your sk");

JSONObject req = new JSONObject();
req.put("req_key", "");

Object response = visualService.cvProcess(req);
System.out.println(JSON.toJSONString(response));
```

---

### 异步接口

**Action**: `CVSubmitTask`

调用示例：

```python
from volcengine.visual.VisualService import VisualService

visual_service = VisualService()
visual_service.set_ak('your ak')
visual_service.set_sk('your sk')

form = {
    "req_key": "xxx",
}

resp = visual_service.cv_submit_task(form)
print(resp)
```

---

### 同步转异步接口

**Action**: `CVSync2AsyncSubmitTask`

调用示例：

```go
package main

import (
    "encoding/json"
    "fmt"
    "github.com/volcengine/volc-sdk-golang/service/visual"
)

func main() {
    visual.DefaultInstance.Client.SetAccessKey("your ak")
    visual.DefaultInstance.Client.SetSecretKey("your sk")

    reqBody := map[string]interface{}{
        "req_key": "",
    }

    resp, status, err := visual.DefaultInstance.CVSync2AsyncSubmitTask(reqBody)
    fmt.Println(status, err)
    b, _ := json.Marshal(resp)
    fmt.Println(string(b))
}
```

---

## 4. 常见问题

### Q1: 如何获取 AK/SK？

- 登录火山引擎控制台，进入 **访问密钥管理** 页面，创建并获取 AK/SK。

### Q2: 签名失败怎么办？

- 确保时间同步，使用 UTC 时间。
- 检查签名参数是否正确。

### Q3: 如何调试 API？

- 使用 `print(response)` 查看返回结果。
- 检查日志，确保请求参数完整。

---

*📝 最后更新：2025年7月30日*
