# UUID在线生成器 - 批量生成UUID v4

免费在线UUID生成器，支持UUID v4随机生成，可批量生成1-100个UUID，一键复制功能，适用于数据库主键、API标识、分布式系统等场景。

> 完整图文与持续更新版本：[UUID在线生成器 - 批量生成UUID v4](https://869hr.uk/2026/tools/uuid-generator/)

## 内容信息

- 原文：https://869hr.uk/2026/tools/uuid-generator/
- 更新：2026-01-31
- 分类：工具
- 专题：工具
- 关键词：效率工具、在线工具、开发工具

## 正文

<!-- 文章摘要 -->
> 
UUID在线生成器是一款免费的开发工具，支持批量生成UUID v4格式的通用唯一识别码。可以一次生成1-100个UUID，每个UUID都有独立的复制按钮，还支持随机复制功能。适用于数据库主键、API标识、分布式系统ID、链路追踪等场景。

## UUID在线生成器

<style>
.uuid-generator {
  max-width: 800px;
  margin: 20px auto;
  padding: 30px;
  background: #f8f9fa;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

.uuid-generator h2 {
  text-align: center;
  color: #333;
  margin-bottom: 30px;
}

.control-panel {
  display: flex;
  gap: 15px;
  margin-bottom: 20px;
  flex-wrap: wrap;
  align-items: center;
}

.control-group {
  display: flex;
  align-items: center;
  gap: 10px;
}

.control-group label {
  font-weight: 600;
  color: #555;
}

.control-group input[type="number"] {
  width: 80px;
  padding: 10px;
  border: 2px solid #ddd;
  border-radius: 5px;
  font-size: 16px;
  text-align: center;
}

.btn {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  font-weight: 600;
  transition: all 0.3s;
}

.btn-primary {
  background: #007bff;
  color: white;
}

.btn-primary:hover {
  background: #0056b3;
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0,123,255,0.3);
}

.btn-success {
  background: #28a745;
  color: white;
}

.btn-success:hover {
  background: #218838;
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(40,167,69,0.3);
}

.btn-copy {
  padding: 5px 12px;
  font-size: 14px;
  background: #6c757d;
  color: white;
}

.btn-copy:hover {
  background: #5a6268;
}

.btn-copy.copied {
  background: #28a745;
}

.result-section {
  margin-top: 20px;
}

.result-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 15px;
}

.result-header h3 {
  margin: 0;
  color: #333;
}

.uuid-list {
  background: white;
  border-radius: 8px;
  padding: 20px;
  min-height: 200px;
  max-height: 600px;
  overflow-y: auto;
}

.uuid-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 15px;
  margin-bottom: 10px;
  background: #f8f9fa;
  border-radius: 5px;
  border-left: 4px solid #007bff;
  transition: all 0.3s;
}

.uuid-item:hover {
  background: #e9ecef;
  transform: translateX(5px);
}

.uuid-item:last-child {
  margin-bottom: 0;
}

.uuid-text {
  font-family: 'Courier New', monospace;
  font-size: 16px;
  color: #333;
  word-break: break-all;
}

.copy-btn {
  padding: 6px 15px;
  margin-left: 10px;
  background: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.3s;
  white-space: nowrap;
}

.copy-btn:hover {
  background: #0056b3;
}

.copy-btn.copied {
  background: #28a745;
}

.empty-state {
  text-align: center;
  color: #999;
  padding: 60px 20px;
}

.empty-state svg {
  width: 80px;
  height: 80px;
  margin-bottom: 20px;
  opacity: 0.5;
}

.toast {
  position: fixed;
  top: 20px;
  right: 20px;
  background: #28a745;
  color: white;
  padding: 15px 25px;
  border-radius: 5px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
  z-index: 1000;
  animation: slideIn 0.3s ease-out;
}

@keyframes slideIn {
  from {
    transform: translateX(400px);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

@media (max-width: 768px) {
  .uuid-generator {
    padding: 20px;
  }

  .control-panel {
    flex-direction: column;
    align-items: stretch;
  }

  .control-group {
    justify-content: space-between;
  }

  .uuid-item {
    flex-direction: column;
    align-items: flex-start;
    gap: 10px;
  }

  .copy-btn {
    width: 100%;
  }
}
</style>

<div class="uuid-generator">
  <h2>UUID 在线生成器</h2>

  <div class="control-panel">
    <div class="control-group">
      <label for="uuidCount">生成数量：</label>
      <input type="number" id="uuidCount" min="1" max="100" value="10">
    </div>
    <button class="btn btn-primary" onclick="generateUUIDs()">生成</button>
    <button class="btn btn-success" onclick="copyRandomUUID()">随机复制一个</button>
  </div>

  <div class="result-section">
    <div class="result-header">
      <h3>结果：</h3>
      <button class="btn btn-copy" id="copyAllBtn" onclick="copyAllUUIDs()" style="display: none;">复制全部</button>
    </div>
    <div class="uuid-list" id="uuidList">
      <div class="empty-state">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
        </svg>
        <p>点击"生成"按钮开始生成 UUID</p>
      </div>
    </div>
  </div>
</div>

## 什么是 UUID？

UUID（Universally Unique Identifier）是通用唯一识别码的缩写，是一个 128 位长的标识符。在不需要中央协调机构的情况下，UUID 可以保证在空间和时间上的唯一性。

### UUID 的特点

1. **全局唯一性**：UUID 的设计目标是保证在分布式系统中生成的标识符是唯一的
2. **无需注册**：不需要任何中央机构来管理和分配 UUID
3. **标准化格式**：标准 UUID 格式为 32 个十六进制数字，用连字符分成 5 组，形式为 `8-4-4-4-12`，共 36 个字符
4. **多种版本**：
   - UUID v1：基于时间和 MAC 地址
   - UUID v3：基于命名空间的 MD5 哈希
   - UUID v4：随机生成（最常用）
   - UUID v5：基于命名空间的 SHA-1 哈希

### UUID v4 格式说明

本工具生成的是 **UUID v4** 版本，格式如下：

```
xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx
```

- **x**：随机十六进制数字（0-9，a-f）
- **4**：表示 UUID 版本（版本 4）
- **y**：变体标识，值为 8、9、a 或 b

示例：`f47ac10b-58cc-4372-a567-0e02b2c3d479`

## 应用场景

UUID 在各种场景中都有广泛应用：

1. **数据库主键**：作为分布式数据库表的主键，避免 ID 冲突
2. **API 标识**：RESTful API 中资源的唯一标识符
3. **会话标识**：用户会话或交易 ID
4. **链路追踪**：微服务架构中的请求追踪 ID
5. **文件标识**：云存储中文件的唯一标识
6. **配置标识**：配置项或部署单元的唯一标识

## 使用说明

1. **设置数量**：在"生成数量"输入框中输入要生成的 UUID 数量（1-100）
2. **生成 UUID**：点击"生成"按钮生成指定数量的 UUID
3. **复制单个**：点击每个 UUID 右侧的"复制"按钮复制该 UUID
4. **随机复制**：点击"随机复制一个"按钮，系统会随机选择一个 UUID 并复制
5. **复制全部**：生成后可点击"复制全部"按钮一次性复制所有 UUID

## 技术实现

UUID v4 使用加密强度强的伪随机数生成器生成，通过 RFC 4122 标准定义的算法确保唯一性。理论上，UUID v4 的重复概率为 1/2^122，在实际应用中几乎可以忽略不计。

```javascript
// UUID v4 生成算法示例
function generateUUID() {
  return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function(c) {
    const r = Math.random() * 16 | 0;
    const v = c === 'x' ? r : (r & 0x3 | 0x8);
    return v.toString(16);
  });
}
```

## 注意事项

- UUID 是 128 位的标识符，虽然重复概率极低，但理论上仍存在重复可能
- 对于极高并发的场景，建议使用 UUID v1 或其他分布式 ID 生成方案
- UUID 的字符串形式较长，在某些存储和传输场景下需要考虑性能影响
- 本工具在浏览器端生成，所有 UUID 都在本地计算，不会上传到服务器

## 参考链接

- [RFC 4122 - UUID 规范](https://tools.ietf.org/html/rfc4122)
- [UUID 维基百科](https://zh.wikipedia.org/wiki/UUID)
- [UUID 在线生成器 - 1024Tools](https://1024tools.com/uuid)

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tools/uuid-generator/)
