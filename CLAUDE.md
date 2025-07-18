# Surge 个人规则配置管理指南

## 项目概述
这是一个个人的 Surge 代理规则配置项目，采用模块化设计，按流量类型和地区进行规则分类管理。

## 文件结构说明

### 主配置文件
- **`main.sgmodule`**: 主要的 Surge 模块配置
  - 定义代理组：OpenAI、PayPal 等特定服务的代理策略
  - 规则集引用：按优先级顺序引用各个 `.list` 文件
  - DNS 和增强模式配置

- **`private.sgmodule`**: 私有配置（本地代理设置）
- **`surge-rule.conf`**: 完整的 Surge 配置文件

### 规则列表文件

#### 按流量处理方式分类：

1. **`direct.list`** (22条) - 直连规则
   - 国内服务：百度网盘、地图、百科
   - 本地应用：UUBooster、WeChat
   - Apple 服务相关域名

2. **`main.list`** (628条) - 主要代理规则
   - 国外主流服务：GitHub、Discord、YouTube、Spotify
   - 开发工具：Docker、NPM、Python 相关
   - 社交媒体：Twitter、Instagram、Facebook
   - 区块链/加密货币相关服务

3. **`reject.list`** (225条) - 拒绝/广告屏蔽规则
   - 广告域名：百度、腾讯、字节跳动广告
   - 追踪统计：各种分析和用户行为追踪
   - 恶意软件：色情、垃圾邮件相关

#### 按地区/服务分类：

4. **`ai.list`** (20条) - AI 相关服务
   - OpenAI、Claude、Cursor 等 AI 服务
   - 使用 OpenAI 代理组

5. **`jp.list`** (16条) - 日本地区专用规则
   - 任天堂、Pixiv、DMM 等日本服务
   - 使用 JP 代理组

6. **`tw.list`** (5条) - 台湾地区专用规则
   - 巴哈姆特等台湾服务
   - 使用 TW 代理组

7. **`disneyplus.list`** (6条) - Disney+ 流媒体规则
   - 流媒体服务优化

### 待整理文件
- **`todo.md`** (93条) - 待分类的规则

## 规则分类标准

### DIRECT（直连）标准
- 国内服务和网站
- 本地应用程序
- Apple 服务（部分）
- 地理位置相关服务

### Proxies（代理）标准
- 国外主流服务
- 开发工具和技术网站
- 社交媒体平台
- 区块链和加密货币服务

### REJECT（拒绝）标准
- 广告和追踪域名
- 恶意软件和垃圾邮件
- 应用内购买验证（部分）
- 不需要的遥测数据

### 地区特定规则
- **AI 服务**: 需要特定优化的 AI 相关服务
- **日本服务**: 需要日本节点的服务
- **台湾服务**: 需要台湾节点的服务
- **香港服务**: 需要香港节点的服务

## 维护原则

### 添加新规则时
1. 确定规则类型和分类
2. 检查是否已存在相同规则
3. 使用标准格式和注释
4. 更新相关文档

### 定期维护
1. 检查规则有效性
2. 移除过时规则
3. 更新分类标准
4. 优化规则性能

## 工具和命令

### 常用 Surge 规则类型
- `DOMAIN`: 完整域名匹配
- `DOMAIN-SUFFIX`: 域名后缀匹配
- `DOMAIN-KEYWORD`: 域名关键字匹配
- `IP-CIDR`: IP 地址段匹配
- `PROCESS-NAME`: 进程名称匹配
- `RULE-SET`: 规则集引用

### 验证命令
```bash
# 检查规则语法
surge-validate-rules

# 测试规则匹配
surge-test-rule <domain>
```

## 注意事项

1. **规则优先级**: 规则按文件引用顺序执行，越早的规则优先级越高
2. **性能考虑**: 避免过多的关键字匹配规则，优先使用域名匹配
3. **隐私保护**: 不要在规则中包含敏感信息
4. **定期更新**: 定期检查和更新规则以适应服务变化

---

## 更新
每次检测 todo.md 里的内容，根据项目情况进行拆分，移动后对比拆分是否合理，有疑问跟用户确认，如果没有问题清空  todo.md 的内容

*最后更新：2025-07-16*
*维护者：个人使用*