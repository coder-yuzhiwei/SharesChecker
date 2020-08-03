# SharesChecker

能够批量检测百度网盘分享链接是否有效的小工具。

目前仅支持检测百度网盘的分享链接，但此项目原理简单。只要读懂了原理，我相信你一定能很快改出检测其他网盘分享链接的代码。所以，本项目很适合python网络编程初学者练手。



### 维护情况

---

程序最后调试日期为2020/7/4，windows10，chrome，python3环境下可以正常检测百度网盘链接。



### 使用方法

---

#### 环境

> windows10
>
> python3
>
> 浏览器以及对应的webdriver



#### 安装依赖

1. 下载对应版本的浏览器驱动，并将其路径配置为环境变量。

   主流浏览器驱动下载地址如下：

   | **Chrome**  | https://sites.google.com/a/chromium.org/chromedriver/downloads |
   | ----------- | ------------------------------------------------------------ |
   | **Edge**    | https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/ |
   | **Firefox** | https://github.com/mozilla/geckodriver/releases              |
   | **Safari**  | https://webkit.org/blog/6900/webdriver-support-in-safari-10/ |

   然后将驱动所在的路径设为环境变量。

2. 安装Python的相关依赖库

   ```python
   # 使用python控制浏览器驱动
   pip install selenium
   
   # 操作xlsx
   pip install openpyxl
   ```

   

#### 运行

1. 将所有需要检测的链接集合到一个xlsx文件，形式如下

   ![image](https://github.com/coder-yuzhiwei/SharesChecker/blob/master/images/img1.png?raw=true)

   第一行为表头，往下每行都是一条分享链接，目前只支持百度网盘分享链接。

   

2. 在命令行运行 **share_checker.py**

   ![image](https://github.com/coder-yuzhiwei/SharesChecker/blob/master/images/img2.png?raw=true)

   输入xlsx文件的路径，绝对路径或相对路径均可。

   回车，程序开始执行。

   

3. 运行效率与结果

   平均检测一条链接需要5秒，可以挂机等结果。

   运行结束后会在输入路径下生成一个 xxx(已检测).xlsx，结构与输入的xlsx相同，状态信息会更新。

   ![image](https://github.com/coder-yuzhiwei/SharesChecker/blob/master/images/img3.png?raw=true)

   失效链接：状态为 “失效”

   无法识别的链接：状态为 “未检测”

   有效链接：状态为空

   

#### 原理

1. 从xlsx文件中提取出分享链接
2. 用selenium模块以无界面模式的浏览器访问链接
3. 在返回的html字符串中查找是否存在 "*给您加密分享了文件*"，存在则有效，否则无效
4. 将结果写入xxx(已检测).xlsx，并打印本次检测的统计结果



为什么不用python requests库访问分享链接？

百度分享链接的页面是浏览器执行脚本的结果，用requests库返回的html仅有大量<script>，无法检测。



#### 待开发

- 检测其他网盘的分享链接
- 用户界面

欢迎 pull requests!

#### LICENSE

MIT





