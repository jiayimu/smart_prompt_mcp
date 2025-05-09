# Smart Prompt MCP

一个基于MCP协议的智能提示词模板管理工具。

## 功能特点

- 支持提示词模板的添加、更新、删除和查询
- 支持使用双中括号语法引用模板，如 `[[模板名]]`
- 配置文件自动保存和加载
- 支持自定义配置文件路径
- 提供调试模式

## 快速开始

### 方式一：直接运行（无需安装）

```bash
# 克隆仓库
git clone https://github.com/jiayimu/smart_prompt_mcp.git
cd smart_prompt_mcp

# 安装依赖
pip3 install -r requirements.txt

# 直接运行
python3 smart_prompt_mcp/__main__.py [--config CONFIG_FILE] [--debug]
```

### 方式二：安装后运行

1. 安装步骤：
```bash
# 克隆仓库
git clone https://github.com/jiayimu/smart_prompt_mcp.git
cd smart_prompt_mcp

# 安装依赖并安装包
pip3 install -r requirements.txt
pip3 install .
```

### 方式三：直接使用pip安装

```bash
# 安装包
pip3 install smart-prompt-mcp

# 运行
python3 -m smart_prompt_mcp [--config CONFIG_FILE] [--debug]
```

## 卸载说明

如果遇到以下情况：
```bash
Found existing installation: smart_prompt_mcp 0.1.4
Can't uninstall 'smart_prompt_mcp'. No files were found to uninstall.
```

这表示包的记录存在但文件已丢失，解决方法：
```bash
# 1. 使用 pip 强制重新安装
pip3 install --force-reinstall smart_prompt_mcp

# 2. 然后再次卸载
pip3 uninstall smart_prompt_mcp -y

# 或者直接清除 pip 的包记录（如果上述方法不起作用）
pip3 install pip-autoremove
pip-autoremove smart_prompt_mcp -y
```

## 使用方法

### 1. 启动服务器

```bash
python3 -m smart_prompt_mcp [--config CONFIG_FILE] [--debug]
```

参数说明:
- `--config`: 指定配置文件路径（可选，默认为 ~/prompt_templates.json）
- `--debug`: 启用调试日志（可选）

### 2. 可用工具

- `smart_template`: 替换输入中的关键词
  - 输入: 包含 `[[关键字]]` 的文本
  - 输出: 替换后的文本

- `add_template`: 添加新的关键词和提示词
  - 参数: 
    - keyword: 关键字
    - prompt: 提示词内容

- `reset_template`: 更新已存在的关键词对应的提示词
  - 参数:
    - keyword: 关键字
    - prompt: 新的提示词内容

- `show_template`: 显示特定关键词的提示词
  - 参数:
    - keyword: 关键字

- `show_all_templates`: 显示所有存储的关键词和提示词

- `delete_template`: 删除特定的关键词和提示词
  - 参数:
    - keyword: 要删除的关键字

### 3. 使用示例

```python
# 添加模板
add_template("接口分析", "分析该接口的入参、出参、业务逻辑和注意事项")
add_template("代码优化", "分析代码的性能瓶颈，提供优化建议")

# 使用模板
smart_template("请帮我[[接口分析]]")
smart_template("这段代码需要[[代码优化]]，请帮我看看")

# 更新模板
reset_template("接口分析", "详细分析该接口的：\n1. 请求参数\n2. 响应结构\n3. 业务流程\n4. 异常处理\n5. 性能考虑")

# 查看特定模板
show_template("接口分析")

# 查看所有模板
show_all_templates()

# 删除模板
delete_template("代码优化")

# 复杂示例：组合多个模板
smart_template("这个接口需要[[接口分析]]，同时也需要[[性能优化]]和[[安全检查]]")
```

## 配置文件格式

配置文件为JSON格式，结构如下:

```json
{
  "关键字1": "提示词内容1",
  "关键字2": "提示词内容2"
}
```

## 依赖

- Python >= 3.10
- fastmcp >= 0.1.0

建议使用Python 3.10或更高版本以获得最佳性能和兼容性。

## 许可证

MIT License
