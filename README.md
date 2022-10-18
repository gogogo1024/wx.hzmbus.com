# 项目成因

boss 直聘上面有 boss 联系有偿破解，抱着试试看的心态来弄的，弄出来了，boss 装死了，boss 微信号 a13882344444

## 操作手册

1. 首先把网站的所有 js 文件 download 到本地
2. 处理 download 下的 s.js 文件，里面包含主要的逻辑，对应项目中的 s_origin.js
   1. 利用<http://jsnice.org/> 网站首先格式化 s.js,也可以代码直接请求替换，对应项目中的 s.js
3. 添加 transfer.html，把 2 中得到的 js,一个常量数组，一个自执行闭包函数，以及一个解密函数重命名后为 qs_rc4Bytes，qs_base_data，以及一个闭包自执行的函数复制过来
   1. 主要是利用 qs_rc4Bytes 函数来做一些字符解密，可能会有些解密错误出现怪异符号，可以参照 s1.js 里的方式替换
   2. 复制 transfer.html 中 textarea 结果到 s2.js 中，特别注意需要把一些无关函数注释掉，其实就是为了反调试，比如 debugger,info.console 这类，包括 build 函数
4. 在 app.e8c193475fe4213c11d9.js 中搜索 msk6 函数，找到 withCredentials 位置，同时在 s2.js 中构造 encryptData(此处需要注意 sig,token,sessionId 是阿里云滑块滑动成功的返回值，所以需要先行搞定阿里云滑块，这块在 app js 文件中有在 2392 行，搜索关键字 aliyunCaptcha),函数逻辑同 app.e8c193475fe4213c11d9.js 中 10346 行中函数
5. 新建 result.html，引入需要 md5.min.js,sha1.min.js,以及 s2.js, 打开网页，得到解密结果
6. 还有一个命令行版本，不需要网页，就是 md5.min.js,sha1.min.js,都有对应的包，直接引入，已 nodejs 方式去运行同样得到加密结果
