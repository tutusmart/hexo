title: vscode 常用配置
author: Tutu
tags:
  - vscode
categories:
  - vscode
date: 2019-10-14 14:48:00
---
Visual Studio Code，旨在为所有开发者提供一款专注于代码本身的免费的编辑器。Visual Studio Code的定位还是Editor，一个全功能的Editor，通过Editor反推微软的SDK，.NET(开源，跨平台)等产品铺路。它虽然是Visual Studio家族的一员，但它与传统VS IDE的功能没有太多交集

| 插件名称 | 功能简述 |
|----------|----------|
|Auto Close Tag|自动闭合HTML标签|
|Auto Import|Typescript自动import提示|
| Auto Rename Tag | 修改HTML标签时，自动修改匹配的标签|
|Beautify css/sass/scss/less  |css/sass/less格式化|
|Better Comments  |编写更加人性化的注释|
|Bookmarks  |添加行书签|
|Color Picker  |拾色器|
| Color Highlight |颜色值在代码中高亮显示|
|HTML CSS Support  |css提示（支持vue）|
| PostCss Sorting |css排序|
| Sass |sass插件|
| gitignore |.gitignore文件语法|
| vetur |目前比较好的Vue语法高亮|
| vscode-styled-jsx | vscode-styled-jsx styled-jsx高亮支持|
|Chinese (Simplified) Language|中文插件|
|IntelliSense for CSS class names in HTML |html中css提示|
| Markdown Preview Enhanced|vscode markdown支持|
| One Dark Pro|vscode主题颜色|
| open in browser|html文件支持浏览器打开|
| vscode-icons |vscode 文件文件夹小图标|
|JavaScript (ES6) code snippets|es6代码提示功能|


### 附个人配置文件
```json
{
    // VScode主题配置
    "editor.tabSize": 2,
    "editor.lineHeight": 18,
    "editor.renderLineHighlight": "none",
    "editor.renderWhitespace": "all",
    "editor.fontFamily": "Courier New",
    "editor.fontSize": 14,
    "editor.cursorBlinking": "smooth",
    "editor.multiCursorModifier": "ctrlCmd",
    "editor.formatOnPaste": true,
    // 是否允许自定义的snippet片段提示,比如自定义的vue片段开启后就可以智能提示
    "editor.snippetSuggestions": "top",
    "workbench.iconTheme": "vscode-icons",
    "workbench.startupEditor": "none",

    "files.trimTrailingWhitespace": true,
    // 在react的jsx中添加对emmet的支持
    "emmet.includeLanguages": {
        "jsx-sublime-babel-tags": "javascriptreact"
    },
    "[cpp]": {
        "editor.quickSuggestions": true
    },
    "[c]": {
        "editor.quickSuggestions": true
    },
    "liveServer.settings.port": 5555,
    "window.zoomLevel": 1,
    "javascript.validate.enable": false,
    "vetur.validation.template": false,
    "tslint.autoFixOnSave": false,
    "C_Cpp.errorSquiggles": "Disabled",
    "javascript.implicitProjectConfig.experimentalDecorators": true,
    "workbench.colorTheme": "One Dark Pro",
    "terminal.integrated.shell.windows": "C:\\Windows\\System32\\cmd.exe",
    "liveServer.settings.donotShowInfoMsg": true,
    "[html]": {
        "editor.defaultFormatter": "vscode.html-language-features"
    },
    "explorer.confirmDelete": false
}
```