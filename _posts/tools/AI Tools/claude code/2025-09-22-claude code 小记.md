---
categories: [Tools, AI]
tags: [tools, ai]
math: true
mermaid: true
render_with_liquid: true
img_path: 
description:
pin: 
---
  
### Windows 安装  
#### 通过wsl安装ubuntu
* 快捷键`win+x`打开 powershell 管理员
* 执行 `wsl --install`
* 输入账号密码
  
#### 启动ubuntu
* 按`win`键打开菜单，搜索 `ubuntu`
* 终端(cmd也可以)启动 ubuntu `wsl -d ubuntu`
  
  
#### 迁移安装目录
* 打开 powershell（不是ubuntu）
* 执行导出命令 `wsl --export ubuntu X:\导出包的存放路径\wsl-ubuntu24.04.tar`  (路径为导出包的路径，自定义)
* 注销当前wsl `wsl --unregister ubuntu`
* 在新的目录重新导入 
    * `wsl --import ubuntu X:\安装的路径\ubuntu X:\导出包的路径\wsl-ubuntu24.04.tar`
* [启动ubuntu](#启动ubuntu)
  
#### 安装Claude Code
1. 更新软件源
    * `sudo apt upgrade && sudo apt update -y`
2. 安装nodejs  
    * 
```shell
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt-get install -y nodejs
```
3. 安装claude code
    * 
```shell
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo bash -
sudo apt-get install -y nodejs
node --version
```
4. 配置API
    * 方法1 配置路径：`~/.claude/settings.json`
        * 
```json
{
  "env": {
    "ANTHROPIC_AUTH_TOKEN": "粘贴为Claude Code专用分组令牌key",
    "ANTHROPIC_BASE_URL": "Claude Code 代理url",
    "CLAUDE_CODE_MAX_OUTPUT_TOKENS": "32000",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1",
    "API_TIMEOUT_MS": "600000",
    "BASH_DEFAULT_TIMEOUT_MS": "600000",
    "BASH_MAX_TIMEOUT_MS": "600000",
    "MCP_TIMEOUT": "30000",
    "MCP_TOOL_TIMEOUT": "600000",
    "CLAUDE_API_TIMEOUT": "600000"
  },
  "permissions": {
    "allow": [],
    "deny": []
  }
}
```
{: file='settings.json'}
    * 方法2 配置环境变量
        * 
```shell
echo 'export ANTHROPIC_AUTH_TOKEN="sk-xxx"' >> ~/.bashrc
echo 'export ANTHROPIC_BASE_URL="https://jp.duckcoding.com"' >> ~/.bashrc
source ~/.bashrc
```
5. 启动claude 
    * 进入工程目录 `cd your-forject-folder`
    * 运行命令`claude`


### 基础操作
* 选择具体文件 `@`
    * `Tab`选择
* 切换工作模式 `shift+tab`