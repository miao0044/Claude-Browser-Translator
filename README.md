# Claude 中文翻译 Firefox 扩展

一个简单的 Firefox 扩展，使用本地 Claude API 代理将选中的文字翻译成中文。

## 功能

- **翻译成中文** - 选中任意文字，右键选择"翻译成中文"
- **翻译成英文** - 右键选择 "Translate to English"
- **解释文字** - 右键选择"解释这段文字"获取详细解释
- **快捷键支持** - 选中文字后按快捷键直接翻译，无需右键菜单

## 快捷键

| 快捷键 | 功能 |
|--------|------|
| `Alt+C` | 翻译选中的文字成中文 |
| `Alt+E` | 解释选中的文字 |

### 自定义快捷键

如果默认快捷键与其他软件冲突，可以在 Firefox 中自定义：

1. 打开 `about:addons`
2. 点击右上角齿轮图标 → "管理扩展快捷键"
3. 找到 "Claude 中文翻译" 扩展
4. 点击快捷键输入框，按下你想要的新快捷键组合

## 前提条件

1. 需要运行 LiteLLM 本地代理服务器（参考 litellm-claude-proxy-guide.md）
2. Firefox 浏览器

## 安装步骤

### 方法一：临时加载（开发/测试用）

1. 打开 Firefox
2. 地址栏输入 `about:debugging#/runtime/this-firefox`
3. 点击"临时加载附加组件"
4. 选择这个文件夹中的 `manifest.json` 文件
5. 扩展就会加载

**注意**：临时加载的扩展在 Firefox 重启后会消失，需要重新加载。

### 方法二：打包安装（永久）

1. 将整个文件夹打包成 ZIP 文件：
   ```bash
   cd claude-translator-extension
   zip -r ../claude-translator.xpi *
   ```

2. 在 Firefox 中：
   - 地址栏输入 `about:addons`
   - 点击齿轮图标 → "从文件安装附加组件"
   - 选择 `claude-translator.xpi` 文件

**注意**：Firefox 默认只允许安装 Mozilla 签名的扩展。要安装未签名扩展，需要使用 Firefox Developer Edition 或 Firefox Nightly，并在 `about:config` 中设置 `xpinstall.signatures.required` 为 `false`。

## 使用方法

1. 确保 LiteLLM 代理服务器正在运行：
   ```bash
   ~/.litellm/start-proxy.sh
   ```

2. 在任意网页上选中文字

3. **方式一：右键菜单**
   - 右键点击，选择：
     - "翻译成中文"
     - "Translate to English"  
     - "解释这段文字"

4. **方式二：快捷键（推荐）**
   - `Alt+C` - 直接翻译选中文字
   - `Alt+E` - 解释选中文字

5. 翻译结果会显示在弹窗中，可以点击"复制"按钮复制结果

## 设置

点击浏览器工具栏中的扩展图标可以打开设置面板：

- **代理服务器地址**：默认 `http://localhost:8000`
- **模型**：选择使用的 Claude 模型
- **翻译目标语言**：选择翻译的目标语言

## 故障排除

### 翻译失败

1. 确保 LiteLLM 代理服务器正在运行
2. 在设置面板中点击"测试连接"按钮
3. 检查服务器地址是否正确

### 扩展不工作

1. 检查扩展是否已启用（`about:addons`）
2. 尝试重新加载扩展
3. 检查浏览器控制台是否有错误（F12 → Console）

## 自定义

如果想添加更多翻译目标语言或功能，可以编辑：

- `background.js` - 添加新的右键菜单选项和 prompt
- `popup.html` - 添加新的设置选项
- `content.js` - 修改结果显示方式

## 许可

MIT License - 随意使用和修改
