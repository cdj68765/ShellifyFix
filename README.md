# 概要  
    1.该项目Fork自https://github.com/sailro/Shellify，并做出微小的修复
    2.因该项目的原作者已经将存档设置为只读，所以我无法在原作者那提Issues，因此只能Fork一份单独修改
      该项目的功能是单纯使用.Net读取文件流的方式来解析Windows系统的快捷方式文件，所以不需要调用任何Win系的API，
      这在非Windows系统下读取解析快捷方式文件非常方便。
    3.由于该项目原作者的母语应该是英语，在处理快捷方式解析路径名的时候没有考虑到CodePage以及全角半角存在的情况，
      所以会导致解析快捷方式中存在汉字文字时就变成了乱码。
# 注意事项
    1.使用Shellify.ShellLinkFile.Load(FilePath,936);解析快捷方式时，使用936中文Codepage作为默认Encoding，
      如果需要，可以自行将936修改为其它语系的Codepage
    2.在.Net Core或者.Net 5以上的版本使用该项目时，需调用一次System.Text.Encoding.RegisterProvider(System.Text.CodePagesEncodingProvider.Instance);
    3.在LinkInfo类中添加LocalBasePathUnicode属性，如果快捷方式中存在半角文字的时，会使用Unicode码
      解析目标路径输入LocalBasePathUnicode(注意，这个时候CommonPathSuffix也是存在目标路径值的，但
      是全角部分会解析为？，所以建议如果LocalBasePathUnicode存在值就使用LocalBasePathUnicode，如
      果LocalBasePathUnicode为空则使用CommonPathSuffix)，其它正常情况下，LocalBasePathUnicode为空，目标路径都存在CommonPathSuffix
