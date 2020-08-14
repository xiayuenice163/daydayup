**在线文档**

## 文档工具

定位：能支撑大型技术手册的撰写与发布。

实现的效果：支持多人协同开发文档；支持快捷修改和更新文档，并且改动追踪到人；文档实现类似代码的模块化开发，后期二次利用高效，后期二次改动高效。

+ Markdown，其优点：实现类似代码的模块化开发，后期二次利用高效，后期二次改动高效；支持导出常用格式pdf  html  mobi  word ；Word的基本功能，新工具基本能实现（可支持代码块；解决Word的二进制格式 github 不支持此种格式的问题。其语法上手快，易用性强。Markdown使用方法请您参考：https://www.zhihu.com/question/20409634
+ vscode,书写markdown文件的书写工具，其兼容所有平台，插件丰富，一键集成git; 下载链接：vscode官网工具下载安装https://code.visualstudio.com/
+ markdown写作效率很高，但不适合大篇幅的手册、书籍、文档编辑。要实现书籍级别的写作，必须实现有效的子文档分解和集成，类似LaTeX。gitbook软件平台实现了这一功能。Github能解决协同开发、版本控制、快捷更新、修改追踪到人的问题，Git 是什么请参考：https://zhuanlan.zhihu.com/p/63321080。理解工具的背景之后，上手其实只有一步！注册公司gitlab账号，地址：     http://192.168.84.254:1680

+ 最终的工作步骤:下载：git、vscode、使用公司邮箱注册内网的gitlab账号，外网的github账号，基于 Node.js 的命令行工具安装 GitBook，（基于 Node.js 的命令行工具的 GitBook 使用入门，参考链接：https://blog.didiyun.com/index.php/2019/03/14/node-js-gitbook/）
使用vscode工具编写md文件，利用gitbook 来集成和发布，将md转化为在线文档，每次更新的文件提交到github/gitlab上，进行版本管理。

## 文档维护
现状：中文版目前集成到了产品界面的help按钮和官网在线文档上，英文版目前集成到了英文官网，但是没有集成到产品界面的help按钮上，请知晓。
维护：一共五个版本，五个仓库

+ 中文版help文档源文件，版本管理采用gitlab，master分支, 仓库地址：http://192.168.88.47:1680/STU/help-zh-origin-gitlab.git
+ 中文版官网在线版源文件，版本管理采用gitlab，master分支, 仓库地址：http://192.168.88.47:1680/STU/doc-zh-origin-gitlab.git
+ 中文版官网在线版推送版本文件，版本管理采用github，gh-pages分支， 仓库地址：https://github.com/CloudChef/doc.git
+ 英文版源文件，版本管理采用gitlab，master分支, 仓库地址：http://192.168.88.47:1680/STU/help-en.git
+ 英文版推送版，版本管理采用github，gh-pages分支， 仓库地址：https://github.com/CloudChef/doc-en.git

1. doc-zh-origin-gitlab 
doc中文版是集成到官网的，采用 gitlab 管理， 用的思怡账号创建的gitlab仓库，仓库地址：http://192.168.88.47:1680/STU/doc-zh-origin-gitlab.git
目前，需要思怡给夏月推送的权限，新人提交需要思怡授权。

第一步: 需要将远程仓库doc-zh-origin-gitlab的内容 clone到本地，此处省略安装本地git的过程。
新建文件夹 doc-zh-origin-gitlab ，右键，打开git bash ，执行克隆命令，
$ git clone http://192.168.88.47:1680/STU/doc-zh-origin-gitlab.git
第二步：gitlab账号邮箱配置
$ git config user.name STU
$ git config user.email siyi.tu@cloudchef.io
第三步：在vscode工作区中打开，拉下来的文件夹，做一个提交测试，在拉取下来的本地文件，修改一段文字，例如：
云资源分析 # 数据中心概览，修改一个错别字
第四步：在vscode中，执行
gitbook serve
打开localhost:4000
确认修改生效后
第五步，在vscode中，提交到gitlab的 master分支
至此整个中文文档源文件的更新，版本控制和推送完成了
备注：新人，请他注册gitlab公司账号，然后思怡在设置 人员出，给他提交master 的权限

2. doc-zh-gh-pages-github
使这个在线文档 https://cloudchef.github.io/doc/ 更新生效的步骤

第一步：这个仓库采用 github 管理， 用的方老板账号创建的github仓库，仓库地址：https://github.com/CloudChef/doc.git
目前，思怡已经拥有推送的权限，新人提交需要夏飞授权。
第二步：新建一个文件夹， doc-zh-gh-pages-github
右键，打开git bash ，执行克隆命令，
$ git clone https://github.com/CloudChef/doc.git
github账号邮箱配置
$ git config user.name SiyiTu
$ git config user.email siyi.tu@cloudchef.io
把修改之后生成的 _book 下面的修改文件复制到这里来，然后推送到 gh-pages分支。
注意：每次版本更新，我们首先在help文档里面，修改AdminDoc、foundationConcepts、UserDoc，没问题之后，直接复制到
doc-zh-gh-pages-github文件下，再在doc-zh-gh-pages-github里面 生成的_book 文件，需要做两件事情
1. 将链接地址全局替换
http://CMP-PUBLIC-IP/help/
替换为
https://cloudchef.github.io/doc/
2. 官网在线版和help文档的区别是，官网在线版有一系列的 发布说明 releaseNotes文件夹，PDF文件夹
注意事项：git status 或者 git init 以此来识别 git的状态生效，注意提交时，要切换到gh-pages
3. help-zh-origin-gitlab 
help中文版是集成到界面的help按钮的，采用 gitlab 管理， 用的思怡账号创建的gitlab仓库，仓库地址：http://192.168.88.47:1680/STU/help-zh-origin-gitlab.git    目前，新人提交需要思怡授权。

第一步：$ git clone http://192.168.88.47:1680/STU/help-zh-origin-gitlab.git
第二步：gitlab账号邮箱配置
$ git config user.name STU
$ git config user.email siyi.tu@cloudchef.io
gitbook插件
常用的插件，请参考：https://www.cnblogs.com/mingyue5826/p/10307051.html#autoid-1-3-0

## help文档升级
目前中英文help文档，提交到master分支，提交最新的代码不能自动触发build,需要测试手动执行build脚本
替换IP地址的脚本命令，详见wiki:    http://192.168.1.107:8090/pages/viewpage.action?pageId=19660874



备注： word与markdown
+ <a href="https://xiayuenice163.github.io/book/source/文档工具介绍.pdf" >文档工具介绍</a>

+ 基本安装、发布、常用操作参考网址：
https://tonydeng.github.io/gitbook-zh/gitbook-howtouse/howtouse/gitbookcli.html
https://blog.didiyun.com/index.php/2019/05/09/gitbook-1/#%E6%9E%84%E5%BB%BA%E4%B9%A6%E7%B1%8D

+ 插件：
https://www.cnblogs.com/mingyue5826/p/10307051.html#autoid-1-3-0
丰富的插件网站：  https://www.npmjs.com/package/ebook-convert

+ 基础技能
github 基本操作
markdown基本写法
