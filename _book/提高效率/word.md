+ 需求
一百多页的标书word文档，内容是从旧文档、网站、ppt和产品截图各种复制粘贴，呼，长舒一口气，揉揉发胀的眼睛，终于搞完了内容。剩下样式排版，然后一个个从头到尾刷格式刷，一不小心刷掉了哪个样式，还不容易发现漏掉了。
请问，万能的谷歌，万能的友圈，谁的样式模板用的贼溜，在模板中，定义好字体样式、图片样式、标题、段落、无序列表、封皮、页眉、页脚等等，导入模板，内容自动都按照定义的样式形成。
+ 操劳一次，得永生的方法
类似前端写好css,要用就link引用就完事了。类似代码的模块开发，操劳写一次，哪里要用哪里import，导入万事大吉。
word就没有这种模块化的工具嘛，或者为什么不搞得开放一些，像ppt支持islide插件那样，支持个好用的插件。。。
标准化快捷键的办公技能，通过标准化的Word文档以及标题、正文等快捷键的设置，加速工作的办公效率。
这种模板或者插件不仅良好支持window系统还要良好支持mac ！！！


骞云科技文档normal模板Normal.dotm，定义好了一套标准的字体样式、图片样式、标题、段落、无序列表、封皮、页眉、页脚等等。  normal.dotm模板保存路径： win10路径：C:\Users\admin\AppData\Roaming\Microsoft\Templates
 <a href="https://xiayuenice163.github.io/book/source/Normal.dotm" >骞云科技文档normal模板</a>

具体如何使用，模板中有相应的快捷键说明；将附件中的normal.dotm模板替换word原有的模板,替换后，再新建word文档直接就使用模板的格式内容。

+ 快捷键学习说明
+ <a href="https://xiayuenice163.github.io/book/source/快捷键学习说明.pdf" >快捷键学习说明</a>
+ 实践：我新建一个word 确实发现模板已经按照新建的样式生成在这个基础上修改样式集


+ 将字体修改为 Verdana将图片页眉页脚相继修改为英文，编辑完成英文的模板
+ <a href="https://xiayuenice163.github.io/book/source/Normal-en.dotm" >骞云科技文档normal-en模板</a>
> 注意：1.在这个模板里 图片 无序列表 表格 不太好定义
> 2.全局粘贴之后为什么会带上样式集，我明明选择的使用目标主题 为什么正文样式是错的，那个样式集的设计，管理样式里面学问很大，一个神奇的发现，我统一把正文样式修改正确，全局都改了，剩下无序列表，我可以选择三百多个使用无序列表的地方，统一修改，但是图片和表格样式好像很特别 找不到这种统一选择的入口

进一步研究图片和表格，发现VB 宏的功能


# 自定义宏 
谷歌大法好-- 
+ word图片调整：怎么用word VBA统一调整图片大小
https://zhuanlan.zhihu.com/p/42588748

Sub setpicsize()

Dim n '图片个数

On Error Resume Next '忽略错误

For n = 1 To ActiveDocument.InlineShapes.Count 'InlineShapes 类型 图片

ActiveDocument.InlineShapes(n).Height = 310 '设置图片高度

ActiveDocument.InlineShapes(n).Width = 410 '设置图片宽度

Next n

End Sub


+ 参考链接：
http://www.360doc.com/content/16/1130/06/36441389_610632066.shtml

https://www.jianshu.com/p/61b88c8607da

https://www.bilibili.com/video/av11904630/

+ 中英文标点互换  


Sub ToggleInterpunction() 
Dim ChineseInterpunction() As Variant, EnglishInterpunction() As Variant
Dim myArray1() As Variant, myArray2() As Variant, strFind As String, strRep As String
Dim msgResult As VbMsgBoxResult, N As Byte
'定义一个中文标点的数组对象
ChineseInterpunction = Array("、", "。", "，", ";", "：", "？", "！", "……", "—", "～", "（", "）", "《", "》","￥")
'定义一个英文标点的数组对象
EnglishInterpunction = Array(",", ".", ",", ";", ":", "?", "!", "…", "-", "~", "(", ")", "<", ">","$")
'提示用户交互的MSGBOX对话框
msgResult = MsgBox("您正在使用中英标点互换功能，按Y将中文标点转为英文标点,按N将英文标点转为中文标点!退出请点击右上角关闭按钮", vbYesNoCancel)
Select Case msgResult
Case vbCancel
Exit Sub '如果用户选择了取消按钮,则退出程序运行
Case vbYes '如果用户选择了YES,则将中文标点转换为英文标点
myArray1 = ChineseInterpunction
myArray2 = EnglishInterpunction
strFind = "“(*)”"
strRep = """\1"""
Case vbNo '如果用户选择了NO,则将英文标点转换为中文标点
myArray1 = EnglishInterpunction
myArray2 = ChineseInterpunction
strFind = """(*)"""
strRep = "“\1”"
End Select
Application.ScreenUpdating = False '关闭屏幕更新
For N = 0 To UBound(ChineseInterpunction) '从数组的下标到上标间作一个循环
With ActiveDocument.Content.Find
.ClearFormatting '不限定查找格式
.MatchWildcards = False '不使用通配符
'查找相应的英文标点,替换为对应的中文标点
.Execute findtext:=myArray1(N), replacewith:=myArray2(N), Replace:=wdReplaceAll
End With
Next
With ActiveDocument.Content.Find
.ClearFormatting '不限定查找格式
.MatchWildcards = True '使用通配符
.Execute findtext:=strFind, replacewith:=strRep, Replace:=wdReplaceAll
End With
Application.ScreenUpdating = True '恢复屏幕更新
End Sub


+ 选择所有表格
Sub 选择所有表格()

    Dim tempTable As Table
    Application.ScreenUpdating = False
    If ActiveDocument.ProtectionType = wdAllowOnlyFormFields Then
        MsgBox "文档已保护，此时不能选中多个表格！"
        Exit Sub
    End If
    ActiveDocument.DeleteAllEditableRanges wdEditorEveryone
    For Each tempTable In ActiveDocument.Tables
        tempTable.Range.Editors.Add wdEditorEveryone
    Next
    ActiveDocument.SelectAllEditableRanges wdEditorEveryone
    ActiveDocument.DeleteAllEditableRanges wdEditorEveryone
    Application.ScreenUpdating = True

End Sub


# 录制宏问题

录制宏  我怎么也不能选择图片 ，和图片是否是插入和直接贴的没有关系
是word产品功能的不完善
在2003版本的.doc格式中可以选择图片，做一个对齐方式的修改，边框改不了，其余的都改不了，对齐也只能改几张图。。。






我们都知道在Word中的查找与替换中，通配符“^g”只能匹配嵌入式图片，而且在word中嵌入式图片就像文字一样，可以很好得编辑。如何将非嵌入式图片转为嵌入式图片呢？

+ 非嵌入式图片转为嵌入式图片
Sub ()
Dim oShape As Shape
For Each oShape In ActiveDocument.Shapes
oShape.ConvertToInlineShape
Next
End Sub






