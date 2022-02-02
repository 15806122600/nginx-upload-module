# nginx-upload-module


这个模块基于Nginx upload module (v2.3.0)修改，地址：https://github.com/fdintino/nginx-upload-module
；使用帮助，请访问这个地址。


为了能在Windows上编译通过最新的Nginx版本，对代码进行了修改。

----------------------

Windows平台编译，请首先参考官方帮助：http://nginx.org/en/docs/howto_build_on_win32.html

### 注意事项如下：

1、nginx源码请在https://github.com/nginx/nginx 下载，**不要**在Nginx官方网站下载，因为其中auto目录内缺少configure文件，无法编译；

2、perl的版本建议不要低于5.30，并且在path路径建议放在前面，确保能找到正确的perl.exe；因为git、msys2等内置的perl.exe有可能也在path路径中，但无法用于ngnix编译；

3、确保安装了nasm (https://www.nasm.us), 并且在path路径当中；

4、在msys2的mingw64的命令行中，设置当前路径为nginx源码路径，执行auto/configure。供参考编译参数如下
auto/configure --with-cc=cl --builddir=objs --prefix= --conf-path=conf/nginx.conf --pid-path=logs/nginx.pid --http-log-path=logs/access.log --error-log-path=logs/error.log --sbin-path=nginx.exe --http-client-body-temp-path=temp/client_body --http-proxy-temp-path=temp/proxy --http-fastcgi-temp-path=temp/fastcgi --http-scgi-temp-path=temp/scgi --http-uwsgi-temp-path=temp/uwsgi --with-cc-opt=-DFD_SETSIZE=1024 --with-pcre=../lib/pcre --with-zlib=../lib/zlib --with-openssl=../lib/openssl --with-openssl-opt=no-asm --with-select_module --with-http_ssl_module --with-stream --with-stream_ssl_preread_module --add-module=./upload-module 

*请注意*：--with-pcre、--with-zlib、--with-openssl、--add-module 设置为自己实际情况的路径;

5、针对上述参数，执行完毕后。请把objs目录下的Makefile中的CFLAGS去掉"-WX"编译选项；否则在下一步骤的namke中，会报错“nginx error:c2220:警告被视为错误....”；

6、以管理员身份打开Visual Studio的“x64 Native Tools Command Prompt”，设置当前路径为nginx源码路径，执行命令 nmake –f objs/Makefile 

完毕！

-----

下载已编译的 ngnix1.20.2 for win x64 二进制文件:
https://github.com/chnykn/nginx-upload-module/releases



