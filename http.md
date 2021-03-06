# Http

<details>
<summary>XMLHttpRequest</summary>

#### 参考

- [你真的会使用XMLHttpRequest吗](https://segmentfault.com/a/1190000004322487)

</details>

<details>
<summary>浏览器输入URL到展示页面过程</summary>

- 一. 网络通信
  1. 在浏览器中输入URL

    ```
    用户输入URL,例如https://www.baidu.com. 其中https为协议, www.baidu.com为网络地址
    ```

  2. 应用层DNS解析域名

  ```
  客户端先检查本地是否有对应的IP地址,若找到侧返回对应的IP地址.若没有找到则请求上级DNS服务器,直到找到根节点
  ```

  3. 客户端发送https请求

  ```
  HTTP请求包括请求报头和请求主体两个部分,其中请求报头包含了重要的信息,包括请求的方法(GET/ POST), 目标URL, 遵循的协议(http/https/ftp...),返回的信息是否需要缓存,以及客户端是否发送cookie等
  ```

  4. 打开一个socket与目标IP地址, 端口建立TCP连接

  ```
  位于传输层的TCP协议为传输报文提供可靠的字节流服务.它为了方便传输,将大块的数据分割成以报文段为单位的数据进行管理,并为他们编号,方便服务器接受的时候能准确的还原报文信息. TCP协议通过"三次握手"等方法保证传输的可靠性.  

   "三次握手"的过程,发送端先发送一个带SYN标志的数据包给接收端,在一定的延迟时间内等待接受的回复. 接收端收到数据包后,传回一个带SYN/ACK标志的数据包以示传达确认信息. 接收方收到后再发送一个带ACK标志的数据包给接收方以示握手成功. 在这个过程中,如果发送端在规定延迟时间内没有收到回复则默认接受方没有收到请求,而再次发送,知道收到回复为止.
  ```

  5. 网络层IP协议查询MAC地址

  ```
  IP协议的作用就是把TCP分割好的各种数据包传送给接收方.而要保证确实能传到接收方还需要接收方的MAC地址,也就是物理地址. IP地址和MAC地址是一一对应的关系,一个网络设备的IP地址可以更换,但是MAC地址一般是固定不变的. ARP协议可以将IP地址解析成对应的MAC地址. 当通讯的双方不在同一个局域网时,需要多次中转才能到达最终的目标,在中转的过程中需要通过下一个中转站的MAC地址来搜索下一个中转目标.
  ```

  6. 数据到达数据链层(tcp建立连接后,发送http请求)

  ```
  再找到对方的MAC地址后,就将数据发送到数据链层传输. 这时,客户端发送请求的阶段结束.
  ```

  7. 服务器接受数据

  ```
  接收端的服务器在链路层接收到数据包,在层层向上直到应用层. 这过程中包括在运输层通过TCP协议将分段的数据包重新组成原来的HTTP请求报文.
  ```

  8. 服务器响应请求

  ```
  服务器接收到客户端发送的请求,查找客户端请求的资源,并返回响应报文,响应报文中包括一个重要的信息----状态码.状态码有三位数字组成,其中比较常见的200 ok表示请求成功. 301表示永久重定向,即请求的资源已经永久的转移到新的位置. 再返回301状态码的同时,响应报文也会附带重定向的URL,客户端接收到后将http请求的URL做相应的改变再重新发送. 404 not found 表示客户端请求的资源找不到.
  ```

  9. 服务器返回相应的文件

  ```
  对服务器响应进行解码,根据资源类型决定如何处理, 页面渲染.
  ```

- 二. 页面渲染

  ```
  现在浏览器渲染页面的过程是这样的:解析HTML以构建DOM树->构建渲染树->布局渲染树->绘制渲染树

    DOM树是由HTML文件中的标签排列组成,渲染树是在DOM树中加入CSS或HTML中的style样式而形成的.渲染树只包含需要显示在页面中的DOM元素,像<head>元素或display属性值为none的元素都不在渲染树中.

    在浏览器还没有接收到完整的HTML文件时,它就开始渲染页面了,在遇到外部链入的脚本标签或样式标签或图片,会再次发送http请求重复上述的步骤. 在收到CSS文件后会对已经渲染的页面重新渲染,加入他们应有的样式,图片文件加载完成立刻显示在相应的位置. 在这一过程可能会触发页面的重绘或者重排.
  ```

#### 参考

- [浏览器输入URL到展示页面过程](https://www.jianshu.com/p/0a2c35e8e2b7)

</details>