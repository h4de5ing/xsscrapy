xsscrapy
========

Fast, thorough, XSS/SQLi spider. Give it a URL and it'll test every link it finds for cross-site scripting and some SQL injection vulnerabilities. See FAQ for more details about SQLi detection.


From within the main folder run:

```shell
./xsscrapy.py -u http://example.com
```


If you wish to login then crawl:
```shell
./xsscrapy.py -u http://example.com/login_page -l loginname -p pa$$word
```

If you wish to login with HTTP Basic Auth then crawl:
```shell
./xsscrapy.py -u http://example.com/login_page -l loginname -p pa$$word --basic
```

If you wish to login without storing your password in your history: 
```shell
./xsscrapy.py -u http://example.com/login_page -l loginname
```

If you want to rate limit to 60 requests per minute: 
```shell
./xsscrapy.py -u http://example.com -r 60
```


XSS vulnerabilities are reported in XSS-vulnerable.txt


Dependencies
-------
``` shell
wget -O https://bootstrap.pypa.io/get-pip.py
python get-pip.py
pip install -r requirements.txt
```

Tests
-------
* Cookies
* User-Agent
* Referer
* URL variables
* End of URL
* Forms both hidden and explicit

FAQ
-------

* If it gives an error : ```ImportError: cannot import name LinkExtractor```. This means that you don't have the latest version of scrapy. You can install it using: ```sudo pip install --upgrade scrapy```.
* It's called XSScrapy, so why SQL injection detection too? There is overlap between dangerous XSS chars and dangerous SQL injection characters, namely single and double quotes. Detecting SQL injection errors in a response is also simple and nonCPU-intensive. So although 99% of this script is strongly geared toward high and accurate detection of XSS adding simple SQL injection detection through error message discovery is a simple and effective addition. This script will not test for blind sql injection. Error messages it looks for come straight from w3af's sqli audit plugin.

License
-------

Copyright (c) 2014, Dan McInerney
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:
* Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
* Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
* Neither the name of Dan McInerney nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL <COPYRIGHT HOLDER> BE LIABLE FOR ANY
DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
http://www.freebuf.com/tools/43194.html
快速、直接的XSS漏洞检测爬虫 – XSScrapy
phper @ 工具 2014-09-16 共 23456 人围观，发现 54 个不明物体  +12 Favorite收藏该文
xsscrapySS1.png
XSScrapy是一个快速、直接的XSS漏洞检测爬虫，你只需要一个URL，它便可以帮助你发现XSS跨站脚本漏洞。
XSScrapy的XSS漏洞攻击测试向量将会覆盖

Http头中的Referer字段
User-Agent字段
Cookie
表单（包括隐藏表单）
URL参数
RUL末尾，如 www.example.com/<script>alert(1)</script>
跳转型XSS
因为Scrapy并不是一个浏览器，所以对AJAX无能为力，我将会在未来努力实现这些功能，尽管并不容易:）
使用方法
基本检测命令
./xsscrapy.py -u http://something.com
如果你需要登陆的话，加上账号、密码作为参数即可
./xsscrapy.py -u http://something.com/login_page -l loginname -p pa$$word
检测结果将会存储在XSS-vulnerable.txt.
