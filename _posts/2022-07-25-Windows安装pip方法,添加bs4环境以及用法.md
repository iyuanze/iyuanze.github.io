---
layout: mypost
title: Windows安装pip方法,添加bs4环境以及用法
categories: [windows,pip,bs4,python]
---
pip是一款非常方便的python包管理工具，本文主要介绍在windows 10下安装pip方法（电脑上已经安装好了python）。
#### 一，windows安装pip

##### 1. 下载pip
地址：https://pypi.python.org/pypi/pip#downloads

注意选择tar.gz压缩包，目前最新版本为22.2，这里选择的版本是：pip-22.2.tar.gz 
点击：[下载](https://files.pythonhosted.org/packages/cd/b6/cf07132d631444dd7ce0ed199f2327eb34e2418f1675145e5b10e1ee65cd/pip-22.2.tar.gz)

##### 2. 解压安装
解压下载的压缩包至工作目录下（如D:\），打开Windows cmd，运行如下命令进入解压后的pip目录

cd /d D:\pip-22.2

使用如下命令进行安装

```
python setup.py install
```


如果你解压在二级目录，比如G盘的\pip-22.2\pip-22.2，那么进入目录的方式为：

```
cd /d G:\pip-22.2\pip-22.2
```


##### 3. 添加环境变量
添加windows系统环境变量，与安装python时添加的方法一样。(python已经添加了环境变量，此处没有添加，pip也可以运行)

如我的python目录是：F:\Python27\;

则添加如下2个目录到系统环境变量里：F:\Python27\;F:\Python27\Scripts。

##### 4. pip常用命令
安装成功后，重新进入CMD后运行pip，可以看到帮助文档：

```
C:\Users\jingge>pip

Usage:
  pip <command> [options]

Commands:
  install                     Install packages.
  download                    Download packages.
  uninstall                   Uninstall packages.
  freeze                      Output installed packages in requirements format.
  list                        List installed packages.
  show                        Show information about installed packages.
  check                       Verify installed packages have compatible dependencies.
  config                      Manage local and global configuration.
  search                      Search PyPI for packages.
  cache                       Inspect and manage pip's wheel cache.
  index                       Inspect information available from package indexes.
  wheel                       Build wheels from your requirements.
  hash                        Compute hashes of package archives.
  completion                  A helper command used for command completion.
  debug                       Show information useful for debugging.
  help                        Show help for commands.

General Options:
  -h, --help                  Show help.
  --debug                     Let unhandled exceptions propagate outside the main subroutine, instead of logging them
                              to stderr.
  --isolated                  Run pip in an isolated mode, ignoring environment variables and user configuration.
  --require-virtualenv        Allow pip to only run in a virtual environment; exit with an error otherwise.
  -v, --verbose               Give more output. Option is additive, and can be used up to 3 times.
  -V, --version               Show version and exit.
  -q, --quiet                 Give less output. Option is additive, and can be used up to 3 times (corresponding to
                              WARNING, ERROR, and CRITICAL logging levels).
  --log <path>                Path to a verbose appending log.
  --no-input                  Disable prompting for input.
  --proxy <proxy>             Specify a proxy in the form [user:passwd@]proxy.server:port.
  --retries <retries>         Maximum number of retries each connection should attempt (default 5 times).
  --timeout <sec>             Set the socket timeout (default 15 seconds).
  --exists-action <action>    Default action when a path already exists: (s)witch, (i)gnore, (w)ipe, (b)ackup,
                              (a)bort.
  --trusted-host <hostname>   Mark this host or host:port pair as trusted, even though it does not have valid or any
                              HTTPS.
  --cert <path>               Path to PEM-encoded CA certificate bundle. If provided, overrides the default. See 'SSL
                              Certificate Verification' in pip documentation for more information.
  --client-cert <path>        Path to SSL client certificate, a single file containing the private key and the
                              certificate in PEM format.
  --cache-dir <dir>           Store the cache data in <dir>.
  --no-cache-dir              Disable the cache.
  --disable-pip-version-check
                              Don't periodically check PyPI to determine whether a new version of pip is available for
                              download. Implied with --no-index.
  --no-color                  Suppress colored output.
  --no-python-version-warning
                              Silence deprecation warnings for upcoming unsupported Pythons.
  --use-feature <feature>     Enable new functionality, that may be backward incompatible.
  --use-deprecated <feature>  Enable deprecated functionality, that will be removed in the future.
```
pip常用命令如下：

```
#安装包
pip install xxx

#升级包，可以使用-U 或者 --upgrade
pip install -U xxx

#卸载包
pip uninstall xxx

#列出已安装的包
pip list
```
##### 5. 常见问题
最近遇到过使用pip命令时报错AttributeError: 'module' object has no attribute 'wraps'，发现是pip安装版本错误导致，使用上述方法重新安装最新版本pip即可解决。

##### 6. 执行python setup.py install报错
python错误：ImportError: No module named setuptools
这句错误提示的表面意思是：没有setuptools的模块，说明python缺少这个模块，那我们只要安装这个模块即可解决此问题，下面我们来安装一下：
1.下载setuptools包：https://pypi.python.org/pypi/setuptools
2.解压setuptools包
3.编译setuptools ：python setup.py build
4.开始执行setuptools安装：python setup.py install

这时再执行：python setup.py install就可以了。

#### 二，pip安装bs4环境及使用方法
bs4解析
bs4：

##### 1，环境安装：
- lxml
- bs4
##### 2，bs4编码流程：
- 1.实例化一个bs4对象，且将页面源码数据加载到该对象中
- 2.bs相关的方法或者属性实现标签定位
- 3.取文本或者取属性
##### 3，bs的属性和方法：
soup.tagName
tagName.string/text/get_text()
tagName[attrName]
find(tagName,attrName='value')
select('层级选择器') > 空格

```
- 环境的安装：
    - pip install lxml
    - pip install bs4
- bs4解析原理：
    - 实例化一个bs对象，且将页面源码数据加载到该对象中。
    - 使用bs对象中封装好的属性或者方法实现标签定位
    - 将定位到的标签中的文本（属性）取出
```

##### 4，bs4用法:

```
import requests
from bs4 import BeautifulSoup
headers = {
    'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/72.0.3626.121 Safari/537.36'
}
```


```
#将本地的一个test.html文档中的源码数据加载到bs对象中
soup = BeautifulSoup(open('./test.html','r',encoding='utf-8'),'lxml')
soup.p #定位到源码中第一个p标签
```
```
soup.a['href']  #取属性
soup.img['src']
# 取文本  返回字符串
soup.p.get_text()
# 取标签
soup.div
#
soup.div.string  #string直接获取标签的直系文本内容
soup.div.text # 取文本
soup.ul.text
# 查找 只查找第一个元素
soup.find('li')   #soup.li
#属性定位
soup.find('div',class_='song')
# 查找所有的 div标签
soup.find_all('div')[0]
# 通过选择器查找  返回列表
soup.select('#feng')
# 获取 内容
soup.select('ul > li > a')[3].string
```

##### 5，案例：bs4 爬取某某诗词网
#需求：某某诗词网中的三国演义小说进行爬取：http://www.*****.com/book/sanguoyanyi.html
import requests
from bs4 import BeautifulSoup
headers = {
    'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) 
```
Chrome/72.0.3626.121 Safari/537.36'
}
url = 'http://www.****.com/book/sanguoyanyi.html'
page_text = requests.get(url=url,headers=headers).text

#数据解析
soup = BeautifulSoup(page_text,'lxml')
#解析出章节和详情页的url
li_list = soup.select('.book-mulu > ul > li')

fp = open('./三国演义.txt','w',encoding='utf-8')
for li in li_list:
    title = li.a.string
    detail_url = 'http://www.**********.com'+li.a['href']
    #获取了详情页的页面源码数据
    detail_page_text = requests.get(url=detail_url,headers=headers).text
    soup = BeautifulSoup(detail_page_text,'lxml')
    #解析出章节对应的内容
    content = soup.find('div',class_='chapter_content').text
    fp.write(title+'\n'+content)
    print(title,'下载完毕')
    
fp.close()
```

