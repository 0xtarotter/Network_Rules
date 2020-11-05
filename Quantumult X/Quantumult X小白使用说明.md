**最开始使用shadowrocket，一开一关超简单**

**感谢各位大佬无私分享的关于 Quantumult X 的各种教程，让我慢慢上手 Quantumult X ；终于决定在他们的各种教程/脚本的基础上，试着根据自己的理解、结合大佬们的东西，写一个能让像我一样的小白能很容易看懂的教程 (希望是这样的)。**

**感谢教程提供(不分先后)：**[Shawn](https://www.notion.so/Quantumult-X-1d32ddc6e61c4892ad2ec5ea47f00917)、**[Sabrina](https://merlinblog.xyz/)**、[毒奶](https://limbopro.xyz/)

**感谢规则、脚本等提供(不分先后)：** [GeQ1an](https://github.com/GeQ1an)、[NobyDa](https://github.com/NobyDa)、[lhie1](https://github.com/lhie1)、[chavyleung](https://github.com/chavyleung)、[lxk0301](https://github.com/lxk0301)、[yichahucha](https://github.com/yichahucha)、[Flydreams](https://gitee.com/Sunert)

**感谢icon资源提供(不分先后)：**[Koolson](https://github.com/Koolson)、[Orz-3](https://github.com/Orz-3)

---

**1. 导入(下载 )配置文件**

配置文件保存在用户本地，可通过远程链接进行下载、可通过 IOS文件/icloud 直接导入

一份完整的配置文件内包含的内容有：



1. 通用设置 / *不需要你了解*

   > - [general]
   >
   > - [dns]



2. **策略组** 

   > **`[policy]`**
   >
   > **策略组** 将 **分流规则** 传递过来的 **网络请求** 进行分发
   >
   > > - 策略组 包含 若干节点，也可包含 子策略(组)
   > >
   > > - 策略组 服务于 分流规则
   > >
   > > - 不同策略组可根据用户个人习惯进行先后排序
   >
   > 1. **策略组：Quantumult X 内置提供了 4 种策略组**
   >
   >    > **static** / 静态策略组
   >    >
   >    > Available / 健康检查策略组 (略)
   >    >
   >    > Robin / 轮询策略 (略)
   >    >
   >    > SSID / 服务集策略 (略)
   >
   > 2. **策略：Quantumult X 内置提供了 3 种策略**
   >
   >    > **Proxy** / 代理
   >    >
   >    > **Direct** / 直连
   >    >
   >    > **Reject** / 拒绝
   >
   > 3. **添加策略组(举例说明)：**
   >
   >    > - ```
   >    >   static=GMedia, Outside, proxy, direct, img-url=https://raw.githubusercontent.com/GeQ1an/Rules/master/QuantumultX/IconSet/GMedia.png
   >    >   ```
   >    >
   >    >   >static：这是一条 静态策略组
   >    >   >
   >    >   >=GMedia,：策略组命名为 GMedia
   >    >   >
   >    >   >Outside, proxy, direct：表示在 GMedia 这条策略组下可以选择用哪些策略(组)或节点
   >    >   >
   >    >   >img-url=：策略组在Quantumult X首页采用的图标(icon)
   >    >
   >    >   这是一条名称为 GMedia 的、可以选择使用Outside策略(组)、proxy策略、direct策略的策略组
   >    >
   >    >   选中 Outside：将使用 Outside 的策略组中选中的节点进行网络访问
   >    >
   >    >   选中 proxy：将使用 proxy 下选中的节点进行网络访问
   >    >
   >    >   选中 direct：将不使用代理，通过直连的方式进行网络访问
   >    >
   >    > - ```
   >    >   static= US Server, server-tag-regex= 美国|🇺🇸|US, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/US.png
   >    >   ```
   >    >
   >    >   > static：这是一条 静态策略组
   >    >   >
   >    >   > = US Server：策略组命名为 US Server
   >    >   >
   >    >   > server-tag-regex=：根据节点名来筛选节点
   >    >   >
   >    >   > img-url=：策略组在Quantumult X首页采用的图标(icon)
   >    >
   >    >   这是一条筛选节点的策略组，如果导入的节点名称中有[美国]、[🇺🇸]、[US]其中任意一个，该节点将会出现在该策略组下。
   >    >
   >    >   这个策略组对于有多个机场订阅的用户来说，可以更方便的整理节点。



3. **分流规则**

   > **`[filter]`**
   >
   > 根据 **分流规则** 将 **网络请求** 进行分流，**网络请求** 的走向(是否能成功访问)由匹配到的 **策略组** 决定
   >
   > 可以用来进行 `TikTok解锁` 和 `网易云音乐灰色音乐解锁` 等玩法(需开启mitm解密)
   >
   > > - 分流规则 是一个list文件
   > >
   > > - 分流规则A 可以被 分流规则B 包含
   > >
   > > - 分流规则 存在先后顺序，靠前规则优先生效，打乱顺序可能导致规则失效
   > >
   > >   > 例如：GeQ1an 规则中 GMedia.list 中 已经包含了 Netflix.list / Spotify.list / YouTube.list
   > >   >
   > >   > 如果你要对 Netflix.list / Spotify.list / YouTube.list 进行重新排序，请确保它们位于 GMedia.list 前面
   >
   > 1. **分流规则工作原理**
   >
   >    list 文件内包含若干如下的域名列表：
   >
   >    ```
   >    # > ABC
   >    HOST-SUFFIX,edgedatg.com,GMedia
   >    HOST-SUFFIX,go.com,GMedia
   >    
   >    # > Abema TV
   >    USER-AGENT,AbemaTV*,GMedia
   >    HOST-SUFFIX,abema.io,GMedia
   >    HOST-SUFFIX,abema.tv,GMedia
   >    HOST-SUFFIX,akamaized.net,GMedia
   >    HOST-SUFFIX,ameba.jp,GMedia
   >    HOST-SUFFIX,hayabusa.io,GMedia
   >    ```
   >
   >    如果发起的**网络访问 命中**了**分流规则**列表中包含的域名，那么**访问请求**将会被**分发至**这条规则指定的**策略组**。访问成功与否取决于策略组
   >
   > 2. **添加分流规则**
   >
   >    > - **添加** `[filter_remote]` **远程分流规则订阅**
   >    >
   >    >   > - 在软件界面(UI)中直接添加，一次添加一条：
   >    >   >
   >    >   >   > Quantumult X 设置 - 分流：[引用] - 右上角[添加] - 输入资源链接
   >    >   >   >
   >    >   >   > ```
   >    >   >   > https://raw.githubusercontent.com/GeQ1an/Rules/master/QuantumultX/Filter/GMedia.list
   >    >   >   > ```
   >    >   >
   >    >   > - 通过修改配置文件添加，一次可添加多条：
   >    >   >
   >    >   >   > *Quantumult X 设置 - 配置文件 - 编辑 - `[filter_romote]` 模块*
   >    >   >   >
   >    >   >   > 格式：
   >    >   >   >
   >    >   >   > ```
   >    >   >   > https://raw.githubusercontent.com/GeQ1an/Rules/master/QuantumultX/Filter/GMedia.list, tag=GMedia 规则, enabled=true
   >    >   >   > ```
   >    >   >   >
   >    >   >   > tag=：给分流规则命名，建议对应策略命名
   >    >   >   >
   >    >   >   > enabled=：是否启用该分流规则，true/启用、false/停用
   >    >
   >    > - **添加** `[filter_local]` **本地分流规则**
   >    >
   >    >   > - 支持 iCloud 引用，格式为：
   >    >   >
   >    >   >   ```
   >    >   >   advertising.txt, tag=规则名称(可删除)，forcr-policy=策略名称(可删除), enabled=true
   >    >   >   ```
   >    >
   >    > - **如果 远程分流 和 本地分流 遇到相同规则，本地规则优先生效**
   >
   > 3. **为分流规则 指定 策略组**
   >
   >    > - **手动引用(推荐)：**
   >    >
   >    >   > Quantumult X 设置 - 分流：[引用] - 选中规则左滑 - 编辑 - 打开 [策略偏好]
   >    >   >
   >    >   > 在弹出的选项中，选择对应的策略组
   >    >
   >    > - **自动绑定( force-policy 强制)：**
   >    >
   >    >   举例：使用 force-policy 强制让 [GMedia 规则] 分流规则使用 [GMedia] 策略偏好
   >    >
   >    >   ```
   >    >   https://raw.githubusercontent.com/GeQ1an/Rules/master/QuantumultX/Filter/GMedia.list, tag=GMedia 规则, force-policy=GMedia, enabled=true
   >    >   ```
   >    >
   >    >   保存配置后
   >    >
   >    >   > 如果已经存在 [GMedia] 策略组，则 [GMedia 规则] 分流规则与 [GMedia] 策略组绑定；
   >    >   >
   >    >   > 如果不存在 [GMedia] 策略组，则 `force-policy` 将强制自动生成一个只包含direct/直连 和 reject/拒绝 两个内置策略的 [GMedia] 策略组。在App首页长按该策略组图标，可以将已经导入的节点添加到策略组下



4. **节点** 

   > **`[server loacl]` / `[server remote]`**
   >
   > > 支持协议：ss/ssr/trojan/vmess/http(s)
   >
   > 1. **通过软件界面(UI)中 节点模块 进行添加**
   >
   >    > - 添加
   >    >
   >    >   > 单节点添加、只支持ss协议
   >    >
   >    > - SS URI：
   >    >
   >    >   > 单节点添加、支持ss/ssr 以及 Quantumult X 格式的 trojan/vmess/http(s) URI
   >    >
   >    > - 扫码
   >    >
   >    >   > 单节点添加、支持ss/ssr 以及 Quantumult X 格式的 trojan/vmess/http(s) 二维码
   >    >
   >    > - **引用(订阅)**
   >    >
   >    >   > - 支持 ss/ssr 以及 Quantumult X 格式的 trojan/vmess/http(s) 订阅链接
   >    >   >
   >    >   >   > - 示例链接(机场)
   >    >   >   >
   >    >   >   >   ```
   >    >   >   >   https://hxlm.cc/api/v1/client/subscribe?token=example
   >    >   >   >   ```
   >    >   >   >
   >    >   >   > - 如果没有 Quantumult X 格式的订阅链接，可采用在线 API 订阅转换器转换后添加、或直接采取 `资源解析器` (下文有单独介绍)进行添加 
   >    >   >   >
   >    >   >   >   >在线 API 订阅转换器：https://dove.589669.xyz/web
   >    >   >   >   >
   >    >   >   >   >输出类型请选择  `节点订阅` 
   >    >   >
   >    >   > - 支持 iCloud/本地 的 txt 文件导入
   >    >   >
   >    >   >   > - 文件内为 Quantumult X 可识别格式的服务器信息，文件名支持中文
   >    >   >   >
   >    >   >   > - iCloud 导入：
   >    >   >   >
   >    >   >   >   > 需打开 Quantumult X - iCloud，打开方法：设置 - 其他设置 - 资源文件夹，将 iCloud 复选打开
   >    >   >   >   >
   >    >   >   >   > 文件存储路径：iCloud/Quantumult X/Profile
   >    >   >   >   >
   >    >   >   >   > 导入方法：`输入资源链接` 下直接输入  `文件名`(不带 .txt 后缀)
   >    >   >   >
   >    >   >   > - 本地导入：
   >    >   >   >
   >    >   >   >   > 文件存储路径：我的iPhone/Quantumult X/Profile
   >    >   >   >   >
   >    >   >   >   > `输入资源链接` 下直接输入  `文件名.txt`
   >    >   >
   >    >   > - 支持远程 txt 文件导入
   >    >   >
   >    >   >   > - 文件内为 Quantumult X 可识别格式的服务器信息
   >    >   >   >
   >    >   >   > - 示例链接
   >    >   >   >
   >    >   >   >   ```
   >    >   >   >   server.txt, img-url=https://example.com/example.png（可删除）, tag = 我的节点（可删除）, enabled=true
   >    >   >   >   ```
   >    >   >
   >    >   > - 订阅后，订阅信息会出现在配置文件的 `[server_remote]` 部分
   >
   > 2. **通过手动写入 配置文件 `[server_local]` 部分 进行添加**
   >
   >    > - **SS/SSR 节点写法**
   >    >
   >    >   略
   >    >
   >    > - **trojan 节点写法**
   >    >
   >    >   ```
   >    >   trojan=example.com:443, password=pwd, over-tls=true, tls-verification=true, fast-open=false, udp-relay=false, tag=节点名称
   >    >   ```
   >    >
   >    > - **v2ray(vmess) 节点写法**
   >    >
   >    >   ```
   >    >   vmess=example.com:443, method=chacha20-ietf-poly1305, password=pwd, obfs-host=example.com, obfs=wss, obfs-uri=/ws, tls-verification=true,fast-open=false, udp-relay=false, tag=节点名称
   >    >   ```
   >    >
   >    > - **http(s)节点写法**
   >    >
   >    >   ```
   >    >   http(s)=example.com:443(端口号根据实际端口填写), username=可选, password=可选, fast-open=false, udp-relay=false, tag=节点名称
   >    >   ```
   >
   > 3. **通过 `资源解析器` 进行添加**
   >
   >    > - **适用于 Quantumult X (v1.0.8-build253) 版本后**
   >    >
   >    > - **实现原理**
   >    >
   >    >   > 通过 `资源解析器` 将用户新建的 节点(订阅)/分流规则/重写 `配置片段` ，转换成 Quanxtumult X 支持的格式
   >    >
   >    > - **优势**
   >    >
   >    >   使用 `资源解析器` 后支持其它格式的 订阅/节点
   >    >
   >    >   可以通过修改本地节点 `配置片段` 来管理 订阅/节点
   >    >
   >    >   相比常见的在线 API 订阅转换器，`资源解析器` 
   >    >
   >    >   > 本地解析，服务器无暴露风险
   >    >   >
   >    >   > 支持中文参数(空格除外)
   >    >
   >    > - **添加`资源解析器`**
   >    >
   >    >   在Quantumult X 配置文件中 `[general]` 部分，加入
   >    >
   >    >   ```
   >    >   resource_parser_url=https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/resource-parser.js
   >    >   ```
   >    >
   >    >   **详细使用视频教程：**待更新



5. **重写** / **MITM解密**

   > **`[rewrite]` / `[mitm]`  ** 
   >
   > > 简单来说，重写 和 mitm解密 主要用来去广告以及某些重定向，比如将 `google.cn` 重定向 `google.hk`
   >
   > 1. **MITM解密 `mitm`**
   >
   >    > - **官方解释：mitm 根证书用于 https 解析，只有配置了主机名的请求才会被 mitm 模块进行解析。**
   >    >
   >    >   > - 我的理解，它就是一个本地证书，反正开启就行：先生成证书、再配置证书(安装证书、信任证书)、然后打开开关。
   >    >   >
   >    >   > - 想要使用 Quantumult X `解锁TikTok` 等高级玩法，就必须开启 `mitm`。
   >
   > 2. **重写 `rewrite`**
   >
   >    > - **官方解释(我也不懂)：用于修改 HTTP 或 HTTPS 请求和响应**
   >    >
   >    >   > 不需要也没必要搞懂，对于我们这样的小白用户，直接引用各位大佬的重写规则就好了，要啥自行车？
   >    >
   >    > - **添加 `[rewrite_remote]` 远程重写规则订阅**
   >    >
   >    >   > - 反正小白应该也不会自己写规则，建议直接引用远程规则，当然也可以引用本机(我的iPhone) / iCloud 路径下的文件，文件格式为 .conf配置文件
   >    >   >
   >    >   > - 远程规则内包含主机名 `hostname` 以及重写 `rewrite` 规则
   >    >   >
   >    >   > - 远程重写订阅格式
   >    >   >
   >    >   >   ```
   >    >   >   https://raw.githubusercontent.com/ConnersHua/Profiles/master/Quantumult/X/Rewrite.conf, tag = 神机复写规则，enabled=true
   >    >   >   ```
   >    >
   >    > - **添加 `[rewrite_local]` 本地重写规则**
   >    >
   >    >   > - 相当于将 远程重写规则 的内容复制到本地 `[rewrite_local]` 模块下
   >    >   > - 1.0.10+版本支持引用远程路径，文件格式为 .js
   >    >   > - 你会写么规则么？反正我不会，所以直接用大佬们的东西吧，就这样



6. **脚本任务**（构造请求）

   > **[task_local]**
   >
   > > 通过执行 crontab 命令，在固定时间或间隔时间执行指定的 JS 脚本。
   >
   > 1. **crontab 命令简单说明**
   >
   >    > - **格式**：* * * * * /path/example.js
   >    >
   >    > - **意义**：分钟 小时 日 月 星期几 /路径/文件名
   >    >
   >    >   > - 分钟：0-59
   >    >   > - 小时：0-23
   >    >   > - 日：1-31
   >    >   > - 月：1-12
   >    >   > - 星期几：0-7（0和7为星期天）
   >    >
   >    > - **举例**
   >    >
   >    >   ```
   >    >   5 0 * * * https://raw.githubusercontent.com/NobyDa/Script/master/JD-DailyBonus/JD_DailyBonus.js
   >    >   ```
   >    >
   >    >   `每天凌晨0点05分执行` 指定路径下的 `JD_DailyBonus.js 脚本`
   >
   > 2. **添加任务**
   >
   >    > - **本地引用**
   >    >
   >    >   > - 使用本地路径，请打开Quantumult设置中 iCloud 资源文件夹，将js文件下载放置至 `iCloud/Quantumult X/Scripts` 文件夹下，若无此文件夹可自行按照路径创建
   >    >   >
   >    >   > - 格式为 `0 9 * * * example.js`
   >    >
   >    > - **远程引用**
   >    >
   >    >   > - 举例
   >    >   >
   >    >   >   京东多合一签到(by NobyDA)
   >    >   >
   >    >   >   ```
   >    >   >   5 0 * * * https://raw.githubusercontent.com/NobyDa/Script/master/JD-DailyBonus/JD_DailyBonus.js, tag=京东多合一签到, img-url=https://raw.githubusercontent.com/Orz-3/task/master/jd.png, enabled=true
   >    >   >   ```

