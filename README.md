# IPFS 分享资源快速上手及其适用场景浅议

## 摘要

本文详细介绍了 IPFS（星际文件系统）的使用方法、优缺点及其在资源分享中的应用场景。文章首先讲解了 IPFS 的基本操作，包括文件的上传、固定、分享和下载。随后，介绍了 IPFS 本地文件管理和使用托管平台的方法。最后，文章对比了 IPFS 与传统网盘分享方案，分析了 IPFS 在应对倒卖者问题上的优势。

## 关于 IPFS 的几个要点：

1. IPFS 上传和下载都**不需要公网 IP，也不需要 VPS**，但是注意如果挂了梯子【**不能开启 TUN 模式**】。
2. IPFS 发布文件需要先**固定**（类比磁链的做种），然后可以通过浏览器整合下载。
3. IPFS 除了自己固定（做种），也可以选择**托管平台**托管，代为做种。
3. IPFS 发布的文件大部分都可以**直连下载**。

先在这里下载 IPFS 客户端并安装：https://docs.ipfs.tech/install/ipfs-desktop/#windows
以下是操作流程的详细说明。

## 1. 固定并分享文件

### 1.1. 固定想要共享的文件

![image](https://github.com/user-attachments/assets/7f7f8126-2f68-4414-b830-6eece32f7ac5)


右键点击上传后的文件，设置固定

![image](https://github.com/user-attachments/assets/81be16a6-c017-4a90-834d-f407659caab1)


固定在本地节点

![image](https://github.com/user-attachments/assets/767a1f94-6f62-4e21-8bcd-23e797eb5e7b)


### 1.2. 复制 CID 以发布文件

固定成功后再次点击右键，选择复制 CID ，就可以发布文件了。

CID 的示例如下：
```cid
QmPKhevNWUx89XBU82XF4UYs2xsdxZnG2xPz2uZsA6Yatm
```

CID 在 IPFS 中对应具体文件，类似于磁链中的哈希值，因此分享 CID 就等于分享文件，下载时只需要知道 CID 即可下载文件。

在说明下载前，可以检测一下自己网络的可用性。

此网址可以检查自己的 IPFS 网络的可用性：https://check.ipfs.network/ ，
下面的 4 个检查得至少满足前 3 个，如果你有公网 IP 则会有第 4 个。

![image](https://github.com/user-attachments/assets/1bfb2db5-7d79-4e82-92b2-9b2c4879d5a2)

![image](https://github.com/user-attachments/assets/6464c04c-4d60-47c5-8e97-ead6d8ad91ed)


### 1.3. 开启 DHT 加速

在上传之前可以在配置选项卡中如下修改配置信息，开启 DHT 加速，DHT 加速可以提高连接节点数量，增加效率。

```
"AcceleratedDHTClient": true,
```

![image](https://github.com/user-attachments/assets/74c313cb-fb5b-4eef-b9cd-3db2da3dd1be)


### 1.4. 关于分享文件的可用性

IPFS 类似于磁链，也需要有人“做种”，需要有人固定文件（做种），并且在线，才可以下载。
可以在这个网址中检测 CID 是否可用：

[https://explore.ipld.io/](https://explore.ipld.io/)

![image](https://github.com/user-attachments/assets/890df37c-dd59-4db3-9a90-17a8fe340915)


## 2. 根据 CID 下载文件

下载文件和上传文件是类似的，首先需要导入文件

![image](https://github.com/user-attachments/assets/87b284e0-8699-48fb-a99d-f34e36d01df6)


在弹出的窗口中输入 CID ，可以自行指定文件名

![image](https://github.com/user-attachments/assets/baa5cc24-b28d-4b77-8087-7a1d6d245570)


导入完成后点击右键，选择下载

![image](https://github.com/user-attachments/assets/f2e4dc70-4ad1-4e16-a0e2-b613e22b89da)

接下来会使用浏览器的下载功能进行文件下载

![image](https://github.com/user-attachments/assets/c22da7b1-e50b-49d3-addb-6dd24fc9362c)


如果安装了 IDM、FDM 等下载软件，也可以使用这些软件接管下载，比如我用的是 FDM ：

![image](https://github.com/user-attachments/assets/8735d221-8eea-4c63-9052-8f9a573f4faa)



## 3. IPFS 本地文件管理

### 3.1 移动本地文件仓库

IPFS 安装以后，默认会在用户路径（C:\\Users\\你的用户名）下方创建一个名为 `.ipfs` 的文件夹，用来存放固定的文件，如果 C 盘空间不足，可以选择移动 IPFS 仓库的默认位置。右键任务栏 IPFS 程序的图标，然后选择 Move Repository Location 即可。

![image](https://github.com/user-attachments/assets/966ba251-5df6-4e14-9ce6-09df6953d674)


注意移动仓库以后，之前固定的文件会失效，需要重新根据 CID 固定文件（如果忘了 CID 就没办法了）

### 3.2 清理非固定文件

当 IPFS 的本地文件过多，可以选择任务栏图标中的 Run Garbage Collector 进行清理，这个操作会清理所有没有在文件选项卡中显示的文件释放磁盘空间。

## 4. 使用 IPFS 托管平台托管文件（以 chainsafe 为例）

由于 IPFS 类似磁链，属于去中心化的分享方式，假如没人开机做种，就会导致后续的下载者没有办法下载。这种时候可以使用托管平台托管文件，代为“做种”。用法类似于网盘，但是分享不通过分享系统，而是采用 CID 进行，因此没有审核、举报系统。

托管平台有很多，这里以 https://app.storage.chainsafe.io/ 为例说明：

### 4.1. 注册 chainsafe 账号

![image](https://github.com/user-attachments/assets/5106d2a2-8278-4b9b-9b2b-bf832c2a99fc)


登录以后的界面如下，新注册的账号有 20 GB 的免费额度

![image](https://github.com/user-attachments/assets/10a1e1b1-1cbc-422a-89f5-655851f9c44b)

### 4.2. 上传并固定文件

点击右上角的 Create Bucket，创建一个用于存储文件的 Bucket，然后点击 Upload 选择文件进行上传

**视个人网速上传速度可能会有点慢，耐心等待即可**。

![image](https://github.com/user-attachments/assets/ab44d7f7-91c9-4e71-aba2-49d9b55db8e6)

上传完毕后复制文件的 CID，然后在第 2 个选项卡中固定（PIN）CID，可以给 CID 起名，这个名称是托管平台中显示的名称，与分享的文件名无关。

![](obsidian_img/Clip_2024-06-30_23-18-16.png)


固定后稍等动作完成


![image](https://github.com/user-attachments/assets/79783b64-f634-4626-bc98-74ee18b0e5b8)


### 4.3. 添加网关发布文件

固定完成后，给 CID 加上相应的网关链接，就得到可以直连下载的分享链接了，下载过程与上文完全一致。

下载链接的格式如下：

```
网关 + CID + ?filename=你想要的文件名.你想要的后缀名
```

这里给出此平台两种可以用的网关：

```
https://ipfs.chainsafe.io/ipfs/
https://ipfs-chainsafe.dev/ipfs/
```

分享链接的例子如下：

```
https://ipfs-chainsafe.dev/ipfs/QmPKhevNWUx89XBU82XF4UYs2xsdxZnG2xPz2uZsA6Yatm?filename=COMIC_BAVEL_2023年11月号-你被骗了.mp4
```

## 5. IPFS 的优缺点及适用场景的个人浅见

### 5.1. 资源分享的安全级别排名

本人在之前的文章中讨论过分享的几种安全级别，这里简要带过一下：

1. 多层加密压缩包：可以防止网盘扫描，但是无法防止在线解压（手机端可以解压包括 .7z 在内的所有格式）
2. 分卷压缩包及自解压压缩包：无法被在线解压，安全性高于前者。
3. 专有格式加密文件：如 Veracrypt 加密卷等，相比于通用的压缩文件，安全性更高一些。但无法应对举报造成的强制违规。
4. 隐写文件：无法被在线解压，并且违规可申诉，如果被举报到无法分享/下载，申诉即可。安全性高于前述所有。
5. 磁链、IPFS 等去中心化分享方案：没有审核系统，安全性最高。但缺点是做不到长时有效稳定。

那么上述这么多级别，应该怎么选择呢？

在机器学习领域有一个定理叫做“没有免费午餐定理”（NFL），是说没有一种算法可以在所有问题上都表现最好。比如说如今的大模型领域都试图得到一个通用的模型实现 AGI，但是就目前而言，在具体下游任务上各种微调模型才是主流，今后可以预见的一段时间内应该也是如此。

回到安全分享这个话题，也是类似的，即不可能存在能够同时兼顾所有场景的分享方案，我们总是需要根据特定场景选择最适合的方案。

对于压缩包方案安全级别问题，我在之前的文章中已经讨论过，这里就不再赘述了，感兴趣可以参看我之前的文章，本文我想重点讨论一下 IPFS 方案的适用场景。

### 5.2. IPFS 分享方案的优缺点分析

本人对 IPFS 的研究比较浅薄，就站在使用者的角度发表一些浅见，算是以教代学，有不对的地方大家可以指正。

个人认为，IPFS 分享相比于网盘分享，其最大优势在于无法被举报，虽然做不到网盘那样长时有效稳定，但是其去中心化分享的特点令其在应对倒卖者的举报上具有无与伦比的优势。相比于同属去中心化分享的磁链方案，IPFS 可以选择托管平台，也可以自己做种，在托管平台选得比较靠谱的情况下，也可以做到类似于网盘那样的长期保存。

由于 IPFS 类似磁链的去中心化特点，分享的安全性有了很大的保障。即使托管平台被攻击或者跑路，只要网上还有人固定文件（做种），就仍有机会下载。并且相比于磁链完全靠做种，IPFS 可以选择托管也可以选择做种，具有更佳的灵活性，可以减轻分享者的负担。

不过 IPFS 作为去中心化的分享方案，也自然有其该有的缺点：首先靠谱的托管平台不好找，其次如果资源比较冷门没人长时间固定（做种），也会出现类似于磁链那样死种的情况。但是相比于磁链， IPFS 在保种这个问题上已经有很大程度的改进了，因为可以选择托管，做种也不需要公网 IP。

### 5.3. IPFS 分享方案与网盘分享方案的对比

分析完上述优缺点，我们可以设想一下其适用的最佳场景，在设想之前，我们需要先对比一下网盘分享的方案。

如果我们想进行长期有效稳定的资源分享，网盘一定是最佳选择，因为运营商代替用户保管文件，拿了钱自然要办事。为了更具体的分析，我们需要知道各大个人网盘的市场占比，限于成本问题，只查到了 2022 年的行业报告，虽然不是最新的，也应该能够反映一些问题，我们先看一下各家网盘的知名度：

根据# 2022年中国个人网盘市场研究报告(https://www.iimedia.cn/c400/84607.html)

![image](https://github.com/user-attachments/assets/dc72d947-bb83-43ef-ba53-0cd02f4998c9)

图中的和彩云是现在的中国移动云盘。

我们可以看到，从数据角度，至少在 2022 年，百度网盘仍以绝对的优势占据了榜首。因此，尽管百度网盘一直被人诟病，但是依然是大部分人心目中“网盘”这个概念的体现，因此也是分享的首选（所谓“不是我非得用百度网盘，而是大家都在用百度网盘”）。

所以，就分享资源的长期有效稳定方面考虑，百度网盘必然是最优选择，但是相应地就存在审核机制。

我在这篇文章中所探讨过，百度网盘的审核机制其实并没有想象中那样严格，对于不分享的显然违规的文件，百度网盘通常是不会管的；对于包含违规文件的分享压缩包，只要无法解密，百度网盘也是不会管的。总之，只要分享的文件不能在线解压，显式地定位到违规文件，百度网盘通常是不会管的。

但是存在一个众所周知的问题：有这么一帮潜藏在各个资源站的特殊行业人群，这些人获取资源后非但不会感谢分享者，还会举报分享文件使之违规炸链，保证只有自己一个来源，然后再对此资源开价售卖。

这帮人就是资源倒卖者，俗称“倒狗/倒爷”。

在百度网盘一家独大的情况下，倒卖者对于百度网盘审核机制的研究也最为深入（所谓盗墓的也一定是半个考古学家），他们充分利用了百度网盘的违规机制（即达到举报阈值自动一刀切），创新性地发明了批量转存+脚本举报的技术，即先转存想要使之违规的文件，然后调用举报脚本，先自动化批量创建分享链接，再以大量账号池组成的海量的举报逐一冲垮文件（类似于 DDoS 攻击）。

倒卖者可以做到全程不下载任何文件，直接就能流水线式地在云端进行转存举报等一系列操作，倒卖者也不需要关注具体举报哪个文件，只需要源源不断地把转存后的文件放入举报池中即可，如此构建起一个简单易操作、成本又可控的举报工作流。只要每天开机运行一遍，就可以让所有举报池中的文件违规（隐写文件因为可申诉，时不时会复活，需要每天都举报）。

看到这有人可能会奇怪，怎么我好像跟他们有仇一样，一直关注这件事，那是因为在之前在研究评论区地毯式炸链时我的账号被倒卖者举报了，我在这篇文章中提到我收到了来自百度网盘的警告，但其实我没有说实话，真实情况是百度网盘并没有警告我，而是直接封了我的号。其间各种损失和折腾有多少我就不多提了，总之只要这帮人还在仓库里，这件事我会一直关注下去，长驱鬼魅不休战。

言归正传，目前对于倒卖者的举报，网盘分享方案也确实没有太好的办法，之前试验的各种外网盘（Mega、PikPak、Gofile、ModsFire、MediaFire 等）也纷纷败下阵来。由于外网盘的封禁政策颇为严厉，一炸链就封号，不像国内网盘一般只是禁止该文件分享。出于文件安全角度考虑，分享还是最好选择国内网盘。

不过，根据我最近的一些传火，我发现倒卖者目前处理不了阿里云盘的隐写文件，个人猜测是因为阿里云的举报需要上传截图以及写小作文的原因，想要拿到截图需要下载文件，也需要写小作文跟网盘方说明，这或许导致举报工作流成本不可控。倒卖者是商人，不是恶人，亏本的买卖不好做。不过这也只是目前的结果，毕竟对方可能会孜孜不倦地举报，或者找到了低成本举报的办法，总归是存在隐患。

### 5.4 IPFS 分享方案的适用场景：倒卖者的举报

小结一下，网盘分享方案虽然在长时间维持资源有效性和可用性方面具有优势，但是在面对倒卖者时是无能为力的。

但是与之相反，IPFS 方案在面对这个问题时就具有优势了，在资源发出的时候采用 IPFS + 网盘隐写文件的办法，可以在 IPFS 有效期间保证资源的可用性，当 IPFS 失效或者不稳定以后，通常也过了这个资源的热度，此时除了倒卖者（以及我这样的人）很少会有人关注。

俗话说只有千日做贼没有千日防贼，倒卖者也不可能无限制地累积举报池的文件，迟早有一天会移除失效已久的文件，此时若有人再要资源，只需要申诉隐写文件解除违规，再进行分享即可，不需要重新压缩上传。

解除违规后不急着分享，先观察一天，看有没有再次违规。一天后在文件详情中点一下申诉，如果提示“请勿申诉正常文件”，就证明文件已经被倒卖者移出了举报池，可以分享了。资源生效以后不要在评论区说明，以免被倒卖者注意到。

（需要注意隐写文件的伪装有效性问题，详情参考隐写者软件的文章）。

## 6. 总结

本文详细地总结了 IPFS 作为一种去中心化文件分享方案的特点和使用方法：

1. IPFS 程序操作: 详细介绍了文件上传、固定、分享 CID 和下载的步骤，以及本地文件管理方法。
2. IPFS 托管平台：以 chainsafe 为例，说明了如何使用托管平台来保证文件的长期可用性。
3. IPFS 优缺点分析：IPFS 的主要优势在于其去中心化特性，不怕举报，因此适合应对倒卖者问题；缺点是可能因缺乏固定节点而导致资源失效。
4. IPFS 与网盘对比：相比传统网盘，IPFS 在应对恶意举报方面更有优势，但在长期稳定性上略逊一筹。
5. 应用建议：文章提出了 IPFS 与网盘隐写文件结合使用的策略，以平衡安全性和长期可用性。

这里需要需要强调的是，大部分情况下，网盘+隐写已经足够安全，如果你的分享本身就属于比较安全的资源（普通音乐、普通影视之类），不大可能被倒卖者盯上，那么此时采用隐写甚至 IPFS 就是多余的，反而会增加不必要的负担。此时采用传统的压缩包方案甚至不压缩可能更好一些。

没有免费午餐定理除了告诉我们事物不存在唯一终极解以外，也告诉我们面对问题需要对症下药，过犹不及。

## 7. 参考

```
 [[技巧分享] 用ipfs存储并分享文件](https://cangku.moe/archives/207441)
 [[技巧分享] 关于去中心化文件分享软件的使用与杂谈](https://cangku.moe/archives/212179)
 [[高阶文章] 关于新时代文件分享机制的思考](https://cangku.moe/archives/178593)
 [[工具分享] 隐写者：把资源嵌入MP4文件的隐写工具 [资源防炸链解决方案倡议&规避网盘审查技巧探讨]](https://cangku.moe/archives/211602)
 [[技巧分享] 网盘资源分享的几种安全级别、审核与举报原理、分享建议 [资源防炸链解决方案倡议]](https://cangku.moe/archives/212002)
 [[技巧分享] 关于评论区地毯式炸链现象的一些测试及初步猜想 [资源防炸链解决方案倡议]](https://cangku.moe/archives/211857)
```
