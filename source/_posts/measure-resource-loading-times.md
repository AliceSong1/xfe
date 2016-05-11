title: 测量资源加载时间
date: 2016-04-27 13:58:38
tags: [devtool, guide]
author: 宋江霞
categories: devtool
---

> 本文根据 https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading 翻译

使用**Network**面板测量你的站点的网络性能。

![Alt text](network-panel.png)

**Network**面板记录了页面在每一个网络操作的信息，包括详细的时序数据，HTTP请求和响应头，cookies等更多信息。

### Network面板总览


Network面板由五个部分组成：
   1. **Controls**.  使用这些选项可以控制**Network**面板的外观和功能。
   2. **Filters**.  使用这些选项可以控制哪些资源显示在**Requests Table**中。提示：按住cmd，然后点击过滤器，这样可以同时选择多个过滤器。
   3. **Overview**. 该图显示了检索资源的时间线。如果看到多条同时垂直堆叠，意味着这些资源被同时检索。
   4. **Requests Table**. 这个图表列出了每个被检索的资源。默认情况下，该表按时间顺序排序，最早的资源在顶部。点击资源名称的区域可得到有关它的更多信息。提示：右键除了**Timeline **外的任何标题，将添加或删除信息列。
   5. **Summary**.这部分展示了请求总数，传输的数据量和加载时间。

![Alt text](panes.png)

**Requests Table**默认展示了下面几项，你可以[增加或删除选项](#增加和删除表格列)。
- **Name**. 资源的名称。
- **Status**. HTTP状态码。
- **Type**. 请求资源的MIME类型。
- **Initiator**. 引发该请求的对象或进程 它可以有以下值之一：
    - **Parser**. Chrome的HTML解析器发起请求。
    - **Redirect**.一个HTTP重定向发起请求。
    - **Script**. 一个脚本发起的请求。
    - **Other**. 其他的过程或行为发起的请求，例如使用者通过链接导航到的网页，或通过在地址栏输入URL地址。
- **Size**. 响应头（通常为几百个字节）加上响应主体的组合的大小，由服务器传送。
- **Time**. 总的持续时间，从请求开始到接到最后一个字节响应所经历的时间。
- **Timeline**. 这个时间轴显示了所有网络请求的视觉瀑布，点击这列标题显示额外的排序字段的菜单。
### 记录网络活动
当**Network**面板是打开的，默认情况下，DevTools会记录所有的网络活动。为了记录，当面板是打开的只需重新加载页面，或在当前加载的页面上等待网络活动。

你可以通过记录按钮判断Devtools是否正在记录。当它是红色(![Alt text](record-on.png))，DevTools正在记录。当它是灰色的(![Alt text](record-off.png)),DevTools未进行记录。单击此按钮可以启动或停止记录，或按键盘快捷键CMD+ E。

### 捕捉记录过程中的截图
**Network**面板可以在页面加载过程中捕捉截图，这个功能称为**幻灯片**。

单击相机按钮开启幻灯片。 当按钮颜色为灰色，幻灯片被禁用(![Alt text](filmstrip-disabled.png))。当按钮颜色为蓝色，幻灯片可用(![Alt text](filmstrip-enabled.png))。

重新加载页面捕捉截图。截图呈现在**Overview**部门的上面。

![Alt text](filmstrip.png)

当鼠标悬停在某个截图上，这个**Timeline**显示了一条垂直的黄线表示该帧被捕捉。

![Alt text](filmstrip-timeline-overlay.png)

在某个截图上双击可以查看放大版本的截图，当某个截图被放大，使用键盘上的左右箭头在截图之间进行切换。

![Alt text](filmstrip-zoom.png)

### 查看DOMContentLoaded和Load事件信息

**Network**面板强调两个事件：[DOMContentLoaded](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded)和[load](https://developer.mozilla.org/en-US/docs/Web/Events/load)。

当一个页面的初始标记已经完成被解析DOMContentLoaded时事件被触发。它在**Network**面板的两个地方显示：
   1. 在**Overview**部分的蓝色垂直条表示这个事件。
   2. 在**Summary**部分你可以看见这个事件的确切时间。

![Alt text](domcontentloaded.png)

当一个页面完全加载完时这个load事件被触发。它在**Network**面板的三个地方显示：
   1. 在**Overview**部分的红色垂直条表示这个事件。
   2. 在**Requests Table**的红色垂直条表示这个事件。
   3.  在**Summary**部分你可以看见这个事件的确切时间。

![Alt text](load.png)

### 查看单个资源的详细信息
单击某个资源名（在**Requests Table**名称列下）来查看有关该资源的更多详细信息。

根据你选择的资源类型，选项卡发生改变，但是下面四个选项卡是最常用：
- **Headers**.  HTTP头部相关资源。
- **Preview**. JSON，图像和文本资源的预览。
- **Response**. HTTP响应数据（如果有）。
- **Timing**. 资源请求生命周期的一个粒状分解。

![Alt text](network-headers.png)

#### 查看Network timing
单击**Timing**选项卡以查看单个资源的请求生命周期的粒状分解。

生命周期显示了在下列类别中花费的时间：

- 排队
- 阻塞
- 请求/响应
- 请求发送
- 等待（第一个字节的时间（TTFB））
- 内容下载

![Alt text](timing-tab.png)

还可以通过在**Timeline**图中的资源上悬停鼠标来查看此相同信息。

![Alt text](timeline-view-hover.png)

-------------------
相关指南 
[Understanding Resource Timing](https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/understanding-resource-timing)

-------------------

#### 查看HTTP头部

点击**Headers**显示该资源的头部信息。

**Headers**选项显示资源的请求的URL，HTTP方法和响应状态码。此外，它列出了HTTP响应和请求头和他们的值，和一些查询字符串参数。

![Alt text](network-headers.png)

通过点击每个部分相邻的view source或view parsed链接，你可以查看响应头，请求头，或在源文件或在解析格式中的查询字符串参数。

![Alt text](view-header-source.png)

通过点击每个部分相邻的view URL encoded 或 view decoded 链接，你还可以查看在网址编码或解码格式的查询字符串参数。

![Alt text](view-url-encoded.png)

#### 预览资源
单击**Preview**选项卡查看该资源的预览。**Preview**选项卡可能会显示任何有用的信息或不会，这取决于您选择的资源类型。

![Alt text](preview-png.png)

#### 查看HTTP响应内容

单击**Response**选项卡，查看资源的未格式化的HTTP响应的内容。 **Response**选项卡可能会包含任何有用的信息或不会，这取决于您选择的资源类型。

![Alt text](response-json.png)

#### 查看cookies

点击**Cookie**选项卡来查看资源在HTTP请求和响应头间传输的cookie表。当传输cookies，这些选项才显示。

以下是图表中每列的描述：
- **Name**. cookie的名称。
- **Value**. cookie的值。
- **Domain**. cookie所属的域。
- **Path**. cookie来自的URL路径。
- **Expires / Max-Age**. cookie的值有效期或者最长有效期的特性。
- **Size**. 用字节表示cookie的大小。
- **HTTP**. 表明cookie只能通过浏览器进行HTTP请求时设置，并且不能使用JavaScript来访问。
- **Secure**. 此属性的存在表明cookie只能在一个安全的连接上传输。

![Alt text](cookies.png)

#### 查看的WebSocket帧
点击**Frames**选项卡来查看[WebSocket](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API)连接信息。当选定的资源触发WebSocket连接时，此选项卡才可见。

![Alt text](websocket-frames.png)

下面是在**Frames**选项卡上的图表的每一列的描述：
- **Data**. 消息有效载荷。如果这个消息是纯文本，它显示在这里。二进制码，此字段显示操作码的名称和代码。以下是支持的操作码：
    - 连续帧 
    - 二进制帧
    - 连接关闭帧
    - 平帧
    - Pong Frame
- **Length**. 用字节为单位的消息的有效载荷的长度。
- **Time**. 创建消息时的时间戳。

消息是根据他们的类型颜色编码的：
- 输出文本消息是颜色编码的浅绿色。
- 输入的文本消息是白色的。
- WebSocket的操作码是淡黄色。
- 错误是淡红色。

**关于当前执行的注意事项：**
- 在新消息到达后，请单击左边的资源名称，以刷新**Frame**图表。
- 只有最后100个WebSocket消息保存在**Frame**图表。

### 查看资源的触发器和依赖
按住Shift键并将鼠标悬停在一个资源来查看它的触发器和依赖。并把鼠标悬停在的这个资源作为**目标**。

上述绿色的颜色编码的目标的第一资源是目标的触发器。如果存在上述的目标的绿色的颜色编码的第二资源，这是触发器的触发器。在下面的目标中任何红色的颜色编码的资源都是依赖于这个目标。

在下面的截图中，这个目标是 dn/。目标的触发器是以 rs=AA2Y脚本开始的，触发器的触发器 (rs=AA2Y) 是 google.com。最后, dn.js 是依赖于目标 (dn/)。

![Alt text](initiators-dependencies.png)

请记住，对于很多资源的页面有可能，你可能无法看到所有的触发器或依赖。

### 排序请求

默认情况下，**Requests Table **中的资源按每个请求的开始时间进行排序，从顶部的最早请求开始。

点击某一个列的标题，按每个资源的值对该表进行排序。再次单击相同的标题，以更改排序顺序以提升或下降。

**Timeline**列是独一无二的。当单击时，它会显示一个排序字段的菜单：
- **Timeline**.每次网络请求的开始时间排序。这是默认的排序，并且是按开始时间选项排序的。
- **Start Time**.每个网络请求的开始时间排序（同由时间轴选项排序）。
- **Response Time**.按每个请求的响应时间排序。
- **End Time**.每次请求完成时按时间排序。
- **Duration**.按每次请求的总时间排序。选择此筛选器以确定哪些资源需要最长时间来加载。
- **Latency**.按请求的开始和响应的开始时间之间的时间排序。选择这个过滤器来确定哪些资源花费第一个字节时间最长（TTFB）。
- 
![Alt text](timeline-sort-fields.png)

### 过滤器请求
**Network**面板提供了许多方法来过滤哪些资源被显示。点击**filters **选项(![Alt text](filters.png))来隐藏或显示**Filters **部分。

使用内容类型按钮只能显示选定内容类型的资源。
 > 注意
 >  按住Cmd的（Mac）或Ctrl键（Windows/ Linux的），然后单击以同时启用多个过滤器。

![Alt text](multiple-content-type-filters.png)

**filter**文本字段很有用。如果你输入的任意字符串，**Network **面板只显示与给定的字符串匹配的资源的文件名。

![Alt text](resource-name-filtering.png)

**filter**文本字段还支持各种关键字，通过各种属性来排序资源，例如文件大小，使用larger-than关键字。

下面的列表介绍了所有的关键字。
- domain.只显示指定的域的资源。你可以使用通配符( \* ) 包括多个域。例如*.com显示的资源都是来自于以.com结尾的所有域名。 DevTools自动完成填充了所有查到域的下拉菜单。
- has-response-header. 显示包含指定的HTTP响应报头的资源。 DevTools自动完成填充了所有查到响应头的下拉列表。
- is.运行发现的WebSocket资源。
- larger-than.显示大于指定大小的资源，以字节为单位。设定值1000相当于设定值1K。
- method. 显示在特定的HTTP方法类型检索到的资源。 DevTools自动完成填充了所有查到的HTTP方法下拉列表。
- mime-type. 显示在特定的MIME类型的资源。 DevTools自动完成填充了所有查到的MIME类型下拉列表。
- mixed-content. 显示所有混合内容资源（mixed-content:all）或只是当前显示的那些资源（mixed-content:displayed）。
- scheme. 显示资源检索到未受保护的HTTP（scheme:http）或保护（scheme:https）。
- set-cookie-domain. 显示与指定的值相匹配的域属性的Set-Cookie头部的资源。 DevTools自动完成填充了所有查到的cookie域的下拉列表。
- set-cookie-name.显示与指定的值相匹配的名称的Set-Cookie头部的资源。DevTools自动完成填充了所有查到的cookie名的下拉列表。
- set-cookie-value.显示与指定的值相匹配的值的Set-Cookie头部的资源。DevTools自动完成填充了所有查到的cookie值的下拉列表。
- status-code. 只显示资源的HTTP状态码匹配指定的代码。DevTools自动完成填充了所有查到的状态码的下拉列表。

![Alt text](larger-than.png)

上面提到某些关键字的自动完成下拉菜单。要触发自动完成菜单，键入关键字后跟一个冒号。例如，在下面的截图中键入域：触发自动完成下拉菜单。

![Alt text](filter-autocomplete.png)

### 复制、保存和清除网络信息

右键单击**Requests Table**来复制、保存或删除网络信息。有些选项是上下文敏感的，所以如果你想在一个单一的资源进行操作，你需要右键点击这行资源。下面的列表描述了每个选项。
- **Copy Response**.将选定的资源的HTTP响应复制到系统剪贴板中。
- **Copy as cURL**.复制所选资源的网络请求作为一个[cURL](https://curl.haxx.se/)命令字符串到系统剪贴板。参考[复制资源作为cURL命令](#复制资源作为cURL命令)。
- **Copy All as HAR**.  复制所有资源到系统剪贴板作为 HAR数据。一个HAR文件包含一个JSON数据结构，描述了网络的“瀑布”。几个[第三方工具](https://ericduran.github.io/chromeHAR/)可以重建在HAR文件数据网络的瀑布。看到网络性能的工具：查看[HTTP Archive（HAR）](https://www.igvita.com/2012/08/28/web-performance-power-tool-http-archive-har/)的更多信息。
- **Save as HAR with Content**.保存所有的网络数据在每一页一个HAR文件资源上。二进制资源，包括图像，编码为base64编码的文本。
- **Clear Browser Cache**.清除浏览器缓存。 

**注意**
您还可以启用或禁用来自[网络条件](https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/network-conditions#network-conditions)的浏览器缓存。

- **Clear Browser Cookies**.清除浏览器的cookie。
- **Open in Sources Panel**.在**Sources**面板中打开选中的资源。
- **Open Link in New Tab**.在新标签中打开选定的资源。也可以在网络表中双击资源名称。
- **Copy Link Address**.复制资源链接到系统剪贴板。
- **Save**.保存选定的文本资源。只显示在文本资源。
- **Replay XHR**.重新发送选定的XMLHTTPRequest，只显示在XHR资源上。

![Alt text](copy-save-menu.png)

#### 复制资源作为cURL命令

cURL是使用HTTP事务的命令行工具。当你在**Requests Table**的资源右键，然后选择复制为cURL，DevTools重新创建一个HTTP请求（包括HTTP头，SSL证书和查询字符串参数），并把它作为一个cURL的命令字符串复制到剪贴板。然后，你可以粘贴字符串到一个终端窗口（与cRUL的系统上）来执行相同的请求

下面是一个cURL命令行字符串例子，来自谷歌新闻首页的XHR请求。

```javascript
curl 'http://news.google.com/news/xhrd=us' -H 'Accept-Encoding: gzip,deflate,:sdch' -H 'Host: news.google.com' -H 'Accept-Language: en-US,en;q=0.8' -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1510.0 Safari/537.36' -H 'Accept: */*' -H 'Referer: http://news.google.com/nwshp?hl=en&tab=wn' -H 'Cookie: NID=67=eruHSUtoIQA-HldQn7U7G5meGuvZOcY32ixQktdgU1qSz7StUDIjC_Knit2xEcWRa-e8CuvmADminmn6h2_IRpk9rWgWMdRj4np3-DM_ssgfeshItriiKsiEXJVfra4n; PREF=ID=a38f960566524d92:U=af866b8c07132db6:FF=0:TM=1369068317:LM=1369068321:S=vVkfXySFmOcAom1K' -H 'Connection: keep-alive' --compressed
```

### 定制网络面板
默认情况下，**Requests Table**显示资源行很小。单击**Use large resource rows**按钮(![Alt text](large-resource-rows-button.png))增加每行的大小。

大行可以使一些列显示两个文本字段：首要字段和次要字段。列标题表示次要字段的含义。

![Alt text](large-resource-rows.png)

#### 增加和删除表格列
右键单击**Requests Table**中的任何一列，以添加或删除列。

![Alt text](add-remove-columns.png)

#### 保留在导航网络日志

默认情况下，当你重新加载当前页面或加载不同的页面，网络活动记录将被丢弃。启用保留日志复选框以保存在这些场景中的网络日志。新的记录被附加到**Requests Table**的底部。

