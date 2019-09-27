# 监控

> IP(独立IP)： 即Internet Protocol,指独立IP数。00:00-24:00内相同IP地址之被计算一次。
> PV([访问量](https://www.baidu.com/s?wd=访问量&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao))： 即Page View, 即页面浏览量或[点击量](https://www.baidu.com/s?wd=点击量&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)，用户每次刷新即被计算一次。
> UV(独立访客)：即Unique Visitor,访问您网站的一台[电脑客户端](https://www.baidu.com/s?wd=电脑客户端&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)为一个访客。00:00-24:00内相同的客户端只被计算一次。
>
> ip,pv,uv的区别
>
> IP(独立IP)：某IP地址的计算机访问网站的次数。这种统计方式很容易实现，具有真实性。所以是衡量[网站流量](https://www.baidu.com/s?wd=网站流量&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)的重要指标。
>
> PV(访问量)：PV反映的是浏览某网站的页面数，所以每刷新一次也算一次。就是说PV与来访者的数量成正比，但PV并不是页面的来访者数量，而是网站被访问的页面数量。
>
> UV(独立访客)：可以理解成访问某网站的电脑的数量。网站判断来访电脑的身份是通过来访电脑的cookies实现的。如果更换了IP后但不清除cookies，再访问相同网站，该网站的统计中UV数是不变的  

### 页面埋点

页面埋点应该是大家最常写的监控了，一般起码会监控以下几个数据：

- [PV](https://baike.baidu.com/item/pv/402) / [UV](https://baike.baidu.com/item/%E7%8B%AC%E7%AB%8B%E8%AE%BF%E5%AE%A2/523828?fromtitle=UV&fromid=59745)
- 停留时长
- 流量来源
- 用户交互

对于这几类统计，一般的实现思路大致可以分为两种，分别为手写埋点和无埋点的方式。

相信第一种方式也是大家最常用的方式，可以**自主选择需要监控的数据然后在相应的地方写入代码**。这种方式的灵活性很大，但是唯一的缺点就是**工作量较大**，每个需要监控的地方都得插入代码。

另一种无埋点的方式基本**不需要开发者手写埋点**了，而是统计所有的事件并且定时上报。这种方式虽然没有前一种方式繁琐了，但是因为统计的是所有事件，所以还需要**后期过滤出**需要的数据。

### 性能监控

性能监控来说，其实我们只需要调用 `performance.getEntriesByType('navigation')` 这行代码就行了

![img](./watch/168c82e5cc721387)

### 异常监控

1. 对于代码运行错误，通常的办法是使用 `window.onerror` 拦截报错。该方法能拦截到大部分的详细报错信息
2. 对于跨域的代码运行错误会显示 `Script error.` 对于这种情况我们需要给 `script` 标签添加 `crossorigin` 属性
3. 对于某些浏览器可能不会显示调用栈信息，这种情况可以通过 `arguments.callee.caller` 来做栈递归
4. 对于异步代码来说，可以使用 `catch` 的方式捕获错误。比如 `Promise` 可以直接使用 `catch` 函数，`async await` 可以使用 `try catch`。

对于捕获的错误需要上传给服务器，通常可以通过 `img` 标签的 `src` 发起一个请求。

另外接口异常就相对来说简单了，可以列举出出错的状态码。一旦出现此类的状态码就可以立即上报出错。接口异常上报可以让开发人员迅速知道有哪些接口出现了大面积的报错，以便迅速修复问题。