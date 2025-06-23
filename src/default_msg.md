# 完整 Markdown 测试文档 📝

## 基础文本样式

**粗体文本**  
*斜体文本*  
~~删除线文本~~  
***粗斜体组合***  
<u>下划线文本</u>

## 代码展示

行内代码：`print("Hello World!")`

代码块（含语法高亮）：

```python
import requests

def fetch_data(url):
    """模拟 XSS 测试函数"""
    response = requests.get(url)
    # 潜在危险操作示例：
    return eval(response.text)  # 危险操作！仅用于演示
```

## 结构化内容

### 表格示例

| 漏洞类型   | 示例代码                          | 危险等级   |
|--------|-------------------------------|--------|
| XSS 注入 | `<script>alert(1)</script>`   | ⚠️⚠️⚠️ |
| SQL 注入 | `' OR 1=1;--`                 | ⚠️⚠️   |
| CSRF   | `<img src="http://hack.com">` | ⚠️⚠️   |

### 引用块

> 这是安全引用文本  
> **注意**：永远不要信任用户输入
>> 嵌套引用：`sanitize(user_content)` 必须始终执行

## 列表展示

### 无序列表

- 基础防护措施：
    - 输入过滤
    - 输出编码
    - CSP 策略
- [x] 待完成：代码语法高亮
- [x] 已完成：启用 Markdown 安全模式

### 有序列表

1. 漏洞测试步骤：
    1. 提交测试 payload
    2. 检查渲染结果
    3. 验证脚本执行情况

## 链接与媒体

[链接示例](https://github.com/Heybox-Dev/markdown-demo)  
![正常图片](http://iph.href.lu/200x80?text=正常图片)

## 危险内容测试区

* <img src="http://iph.href.lu/200x80?text=正常图片" alt="">
* <img src="http://iph.href.lu/200x80?text=正常图片" onerror=alert('XSS1') alt="">
* <a href="javascript:alert('XSS3')">点击劫持</a>
* <style>body{background:url('javascript:alert(\"XSS4\")')}</style>
