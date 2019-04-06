## 2019-04-06 Tooltip Miss
发现光标放在指令上，提示信息不准了，网上没找到处理方法，遂看了下源码。

原因是：DecompilerTextView.cs::GenerateTooltip 时找不到 MscorlibDocumentation

mscorlib 的文档类型是.xml 在XmlDocLoader.cs里确实没找到，找的其中一个位置是：
	C:\Windows\Microsoft.NET\Framework\v4.0.30319\en\mscorlib.xml
	
查了下，文档装到了别的位置了：
	C:\Program Files (x86)\Reference Assemblies\Microsoft\Framework\.NETFramework\v4.0\zh-Hans

一些文档
> 讨论了这个问题 http://community.sharpdevelop.net/forums/p/12848/34828.aspx
> SharpDevelop的一个fix commit https://github.com/icsharpcode/SharpDevelop/commit/9c5bdcc8012b3f79ace0f3553427d563775a1aa1

### 真实原因
发现问题是文档的目录是 zh-Hans 而不是 en 或者 zh 蛋疼。
用Visual Studio Install 安装个en的语言包，解决了问题。

安装的目录类似：C:\Program Files (x86)\Reference Assemblies\Microsoft\Framework\.NETFramework\v4.0\mscorlib.xml