# 把DeepSeek接入WPS，高效办公（保姆级教学）

> 来源：[https://ys8xnr7kn3.feishu.cn/docx/HIwzd2nW1ooudix0MrncQONhnTu](https://ys8xnr7kn3.feishu.cn/docx/HIwzd2nW1ooudix0MrncQONhnTu)

## DeepSeek与Word的梦幻联动，将为你开启高效办公的新篇章！熟悉的Word界面中，只需轻点鼠标，就能召唤出强大的DeepSeek，让它为你快速检索信息、精准翻译文本、智能生成内容…… 告别在不同软件间来回切换的繁琐，告别低效的信息获取方式，让办公效率飞起来！

## 效果演示

按照文本教程完成操作后，Word的选项卡中将会出现DeepSeek的生成图标，选中文本并点击生成，即可实现模型回复！例如，我们想要将一段中文文本翻译成英文：

![](img/403a8e1a25fcf78d9cff016269e6d4fb.png)

![](img/a02aa0bde84d698d160ca6f75cf35394.png)

接下来我将详细介绍，如何实现DeepSeek与Word的结合。

# Office AI助手接入方法

# 设置WPS信任

打开WPS-创建一个文档-点左上角的文件-选项-信任中心

![](img/6577fac82b1a311b79fe8775286853f3.png)

启用所有第三方COM加载项，重启WPS后生效(E)，然后点确定

## 安装office Ai插件

下载officeAi助手：https://www.haiyingsec.com/static/introductions/officeai/introduction.html

![](img/367e8e1dc16759e69342d91691bd54fb.png)

下载好后进行安装，安装前要先把WPS关闭

![](img/ee814632d5a94b4bc84df3454c6d6e4c.png)

点击完成后就会自动打开WPS，上方就会出现officeAI，登录-点击设置

![](img/0e39e5758fae840d195dfd6f4fb2d17d.png)

![](img/afa62d67e768947e96f0e22bcb3de5d4.png)

平台选择硅基流动的R1，然后模型选择R1，这里还需要添加一个API_key

## 获取API Key

登录硅基流动：https://cloud.siliconflow.cn/i/FSIqvgQd

![](img/38917b4821ec550f9729ec54c548b486.png)

![](img/33c98a3bf774e32c61f6ab41f90b33d6.png)

![](img/9b9bfeacdd9225586aaf40d654b636f8.png)

选择密钥-新建密钥-随便填写-复制密钥到WPS-保存

![](img/2fd8c4ac4e9c3c1f30f5918fa2edad90.png)

这样就可以在WPS里使用SeepseekR1了

# VBA插件开发方法

## 设置WPS信任

跟上面的方法一样，开始之前还需要先设置一下信任问题

![](img/acd8fa63c7b44c5caad01c238efaa873.png)

设置好后记得点确定

## 配置WPS

安装wps.vba，下载地址：https://pan.quark.cn/s/f0e6145a1ab0

点击工具-开发工具-点击VB 编辑器

![](img/cfa4df355952481c2d33a97c430aeaaf.png)

![](img/50fe6c3176b42f380339a1697ef6fab0.png)

![](img/906df8e5abdb1d13673e4e708ec0a13f.png)

DeepSeek-V3代码：

```
Function CallDeepSeekAPI(api_key As String, inputText As String) As String
    Dim API As String
    Dim SendTxt As String
    Dim Http As Object
    Dim status_code As Integer
    Dim response As String

    API = "https://api.siliconflow.cn/v1/chat/completions"
    SendTxt = "{""model"": ""deepseek-ai/DeepSeek-V3"", ""messages"": [{""role"":""system"", ""content"":""You are a Word assistant""}, {""role"":""user"", ""content"":""" & inputText & """}], ""stream"": false}"

    Set Http = CreateObject("MSXML2.XMLHTTP")
    With Http
        .Open "POST", API, False
        .setRequestHeader "Content-Type", "application/json"
        .setRequestHeader "Authorization", "Bearer " & api_key
        .send SendTxt
        status_code = .Status
        response = .responseText
    End With

    ' 弹出窗口显示 API 响应（调试用）

    ' MsgBox "API Response: " & response, vbInformation, "Debug Info"

    If status_code = 200 Then
        CallDeepSeekAPI = response
    Else
        CallDeepSeekAPI = "Error: " & status_code & " - " & response
    End If

    Set Http = Nothing
End Function

Sub DeepSeekV3()
    Dim api_key As String
    Dim inputText As String
    Dim response As String
    Dim regex As Object
    Dim matches As Object
    Dim originalSelection As Object

    api_key = "替换为你的api key"
    If api_key = "" Then
        MsgBox "Please enter the API key."
        Exit Sub
    ElseIf Selection.Type <> wdSelectionNormal Then
        MsgBox "Please select text."
        Exit Sub
    End If

    ' 保存原始选中的文本
    Set originalSelection = Selection.Range.Duplicate

    inputText = Replace(Replace(Replace(Replace(Replace(Selection.text, "\", "\\"), vbCrLf, ""), vbCr, ""), vbLf, ""), Chr(34), "\""")
    response = CallDeepSeekAPI(api_key, inputText)

    If Left(response, 5) <> "Error" Then
        Set regex = CreateObject("VBScript.RegExp")
        With regex
            .Global = True
            .MultiLine = True
            .IgnoreCase = False
            .Pattern = """content"":""(.*?)"""
        End With
        Set matches = regex.Execute(response)
        If matches.Count > 0 Then
            response = matches(0).SubMatches(0)
            response = Replace(Replace(response, """", Chr(34)), """", Chr(34))

            ' 取消选中原始文本
            Selection.Collapse Direction:=wdCollapseEnd

            ' 将内容插入到选中文字的下一行
            Selection.TypeParagraph ' 插入新行
            Selection.TypeText text:=response

            ' 将光标移回原来选中文本的末尾
            originalSelection.Select
        Else
            MsgBox "Failed to parse API response.", vbExclamation
        End If
    Else
        MsgBox response, vbCritical
    End If
End Sub
```

DeepSeek-R1代码:

```
Function CallDeepSeekAPI(api_key As String, inputText As String) As String
    Dim API As String
    Dim SendTxt As String
    Dim Http As Object
    Dim status_code As Integer
    Dim response As String

    API = "https://api.siliconflow.cn/v1/chat/completions"
    SendTxt = "{""model"": ""deepseek-ai/DeepSeek-R1"", ""messages"": [{""role"":""system"", ""content"":""You are a Word assistant""}, {""role"":""user"", ""content"":""" & inputText & """}], ""stream"": false}"

    Set Http = CreateObject("MSXML2.XMLHTTP")
    With Http
        .Open "POST", API, False
        .setRequestHeader "Content-Type", "application/json"
        .setRequestHeader "Authorization", "Bearer " & api_key
        .send SendTxt
        status_code = .Status
        response = .responseText
    End With

    ' 弹出窗口显示 API 响应（调试用）

    ' MsgBox "API Response: " & response, vbInformation, "Debug Info"

    If status_code = 200 Then
        CallDeepSeekAPI = response
    Else
        CallDeepSeekAPI = "Error: " & status_code & " - " & response
    End If

    Set Http = Nothing
End Function

Sub DeepSeekR1()
    Dim api_key As String
    Dim inputText As String
    Dim response As String
    Dim regex As Object
    Dim matches As Object
    Dim originalSelection As Object

    api_key = "替换为你的api key"
    If api_key = "" Then
        MsgBox "Please enter the API key."
        Exit Sub
    ElseIf Selection.Type <> wdSelectionNormal Then
        MsgBox "Please select text."
        Exit Sub
    End If

    ' 保存原始选中的文本
    Set originalSelection = Selection.Range.Duplicate

    inputText = Replace(Replace(Replace(Replace(Replace(Selection.text, "\", "\\"), vbCrLf, ""), vbCr, ""), vbLf, ""), Chr(34), "\""")
    response = CallDeepSeekAPI(api_key, inputText)

    If Left(response, 5) <> "Error" Then
        Set regex = CreateObject("VBScript.RegExp")
        With regex
            .Global = True
            .MultiLine = True
            .IgnoreCase = False
            .Pattern = """content"":""(.*?)"""
        End With
        Set matches = regex.Execute(response)
        If matches.Count > 0 Then
            response = matches(0).SubMatches(0)
            response = Replace(Replace(response, """", Chr(34)), """", Chr(34))

            ' 取消选中原始文本
            Selection.Collapse Direction:=wdCollapseEnd

            ' 将内容插入到选中文字的下一行
            Selection.TypeParagraph ' 插入新行
            Selection.TypeText text:=response

            ' 将光标移回原来选中文本的末尾
            originalSelection.Select
        Else
            MsgBox "Failed to parse API response.", vbExclamation
        End If
    Else
        MsgBox response, vbCritical
    End If
End Sub
```

选择V3或者R1的代码复制到模块中，记得把代码里面的API key替换成自己的（也就是硅基流动里面复制的）

![](img/a63dc9af5718fb8e0ce3a7fed19c1fe9.png)

点击 文件 -> 选项 -> 工具

选中，点击新建组，右键新建组，点击重命名，将其命名为"DeepSeek"

选择DeepSeek（自定义），在左侧命令中选择"宏"

![](img/509179e6d276eb01622612413bce6f59.png)

![](img/2a49d13382e7092a0c70195f50f23f71.png)

找到并选中"DeepSeekR1"，点击添加，点击重命名，重命名为"运行R1"，点击确定

![](img/26f9032995eb0fe188abe10a473e05df.png)

在文档中输入问题，并选取，然后点击运行，稍等一会，就会成功了

## 将你的文档另存为 Wps 模板 (.dotm)：

点击"文件" → "另存为"

选择保存类型为"Microsoft Word 带宏的模板文件 (*.dotm)"

保存到 Wps 的模板文件夹（通常是 C:\Users\用户名\AppData\Roaming\kingsoft\wps\startup，如C:\Users\Administrator\AppData\Roaming\kingsoft\wps\startup）

![](img/708f6758f94bebc17ace9ecde890ff4f.png)

这样每次打开 Wps 时，宏就会自动可用