> **1.体验环境**

* 操作手机：iphoneXR
* App名称：手机QQ
* App版本：8.1.0

> **2.产品介绍** 
```
腾讯QQ支持在线聊天、视频通话、点对点断点续传文件、共享文件、网络硬盘、自定义面板、QQ邮箱等多种功能，并可与多种通讯终端相连。
2017年1月5日，腾讯QQ和美的集团在深圳正式签署战略合作协议，双方将共同构建基于IP授权与物联云技术的深度合作，实现家电产品的连接、对话和远程控制。双方合作的第一步，是共同推出基于QQfamilyIP授权和腾讯物联云技术的多款智能家电产品。
2018年12月12日，QQ发布公告，称由于业务调整，webQQ即将在2019年1月1日停止服务，并提示用户下载QQ客户端。
2019年3月13日起，QQ号码可注销 。
2019年03月27日，腾讯QQ宣布推出“鹅的20岁”生日庆典特别栏目，第一期分享了那个企鹅图标的“黑历史”。
2019年4月13日，腾讯QQ正式推送了iOS版的v8.0版本更新，将全新的操作界面带给了正式版用户.
```
* 最新一季的财报也显示QQ的日活，月活相比于去年同期也已逐渐趋于稳定，另外因为QQ看点产品的加入，该部分的社交广告收入也同比增长了28%，为人民币120亿元。
![title](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d5967d76f0b9316e213cc74)

> **3.产品介绍**

（以下年龄、性别、地域数据均来至全国范围 ）

* 3.1 **用户年龄段**：用户最多的年龄段是10-20岁占47.06%；20-30岁的占45.45%排在第二位；第三位是30岁以上的占4.81%；最后还有10岁以下的10后占2.67%。可以很明确的看出来QQ的用户群体总体偏年轻化学生占了很大一部分主体，主要为00后和上一代90后，而30及以上基本没有。
![title](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d596c186f0b9316e213cc79)
![title](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d596d586f0b9316e213cc7a)

* 3.2 **QQ好友群体**：分布最多的群体是学生和同事占75.94%，也正好验证了上述的00后90后的主要群体，而00后主要好友为同学，而90后已经基本走入工作岗位；分布最少的则是家人仅仅为1.6%，也符合用户年龄中30以上很少的逻辑。
![title](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d596e216f0b9316e213cc7b)

> **4.产品设计**

* **功能结构**：QQ主要分为登录注册,消息,聊天,联系人,动态,侧边栏,设置等几大模块。其中消息模块和聊天模块是核心模块。好友动态及联系人属于次核心模块,延续了PC端的界面结构。
整体模块结构如下图所示:
![title](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d5971ea6f0b9316e213cc85)

* 4.1 **消息模块**
消息模块的消息类型繁多复杂。
消息类型包括普通消息,群消息和系统消息。普通消息仅处理一对一聊天的情况,群消息处理群聊天情形。系统消息则根据用户自定义进行个性化推送。
![title](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d59767a6f0b9316e213cc88)
```
1.消息类型处理:
逻辑处理放在后台,客户端只管拉取数据.接口给到消息类型,客户端通过多个CellID进行不同消息类型处理
2.活动,比如抢红包:
后台发送抢红包通知,界面通过TabeleHeaderView进行活动展示,并修改下拉刷新功能,下拉刷新不再对当前消息界面进行刷新,而是对围绕红包弹幕进行功能改造.
3.置顶问题:
QQ的置顶功能是信息存储在本地.将置顶的这一条数据保存到数据库，再次请求数据时将数据与数据库的进行对比，发现相同的就置顶 
```

* 4.2 **聊天模块**
首先看看聊天中的多种消息类型具体如下所示:
![title](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d5978e26f0b9316e213cc8c)
```
聊天界面主要是针对多种类型消息的UI处理.各种消息类型组成一个独立的代码模块,这个模块对每种消息类型提供服务支持.
语音信息和图片信息涉及本地缓存,将语音的ID或图片的名称以及语音(图片)内容进行压缩处理并分别作为key和value进行本地化存储.其他信息进行数据库加密缓存起来.
时间处理方面,发送消息时间通过毫秒处理,并将发送时间一同发给服务器,服务器以发送的时间为准进行排序,而不以接收到消息时间为准.这样避免多个消息出现顺序错乱的现象.
```

* 4.2.1 **语音**
![title](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d597a006f0b9316e213cc8d)
这里通过一个语音模块,并添加长按手势,对不同手势信息进行发送,支持变声，对讲和录音的语音以及取消处理。同时,进行语音本地化存储。

* 4.2.2 **图片发送**
![title](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d597a666f0b9316e213cc8e) 
这里选择图片部分使用一个横向的滑动列表,并且监听系统图片的变化情况,当系统图片增加时(比如这个时候截图),会对这个列表进行实时的刷新.

* 4.2.3 **表情**
![title](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d597b556f0b9316e213cc91)
这里对表情采用了富文本的形式，并且优先展示最近使用，并且支持收藏以及动图等功能。

* 4.2.4 **其他**
![title](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d597aac6f0b9316e213cc8f)
这些按钮控件都对应一个独立功能。比如戳一戳本质是动态图片,当发送后,将动态图片展示到聊天框中,并相对应展示全屏效果。另外还有我的收藏和我的文件等功能。

* 4.3 **登陆模块**
登录问题需要考虑到以下几点:
被迫下线问题:如果在线状态下,其他设备登录,会及时发送当前设备下线通知,不允许用户进行非登录操作。 启动App时会进行免登操作,这时和后台进行交互,如果有被挤下线,提示登录,否则进行免登处理。
是否允许电脑端和手机端同时在线问题:后台存储登录当前设备的信息,比如设备名称,型号等.如果设置允许电脑手机同时在线,后台将对手机和电脑同时提供服务支持,被迫下线问题将被区分单独处理.而如果不允许同时在线,那么被迫下线问题会把电脑,手机视为一体混同处理。

* 5 **优化建议**

* 5.1 **我的装扮-背景边框不一**
![图片标题](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d5980466f0b9316e213cc94)
* 5.2 **收藏里视频不支持保存和像图片那样转发到微信，单个item长按不支持转发**
![图片标题](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d59808d6f0b9316e213cc95)
* 5.3 **名片转发比较难发现**
* 5.4 **表情红包的演示过快**
![图片标题](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d5980cc6f0b9316e213cc97)
* 5.5 **转发定位的时候查看详情和去这里点击不了**
![图片标题](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d59810a6f0b9316e213cc98)
* 5.6 **定位位置不支持收藏**
![图片标题](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d5981416f0b9316e213cc9a)
* 5.7 **美颜可以加在视频聊天窗口下面**
![图片标题](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d59818e6f0b9316e213cc9b)
* 5.8 **特别关心的开关可以直接放在外面**
![图片标题](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d5981c56f0b9316e213cc9c)
* 5.10 **删除聊天记录的这个字体的布局**
![图片标题](https://yunpan.oa.tencent.com/note/api/file/getImage?fileId=5d59823e6f0b9316e213cc9d)
