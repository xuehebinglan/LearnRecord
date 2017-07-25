
# qunar 实习工作总结
## 一、 项目列表
- 1 修改部分浏览器返回不刷新页面，loading一直存在问题【为什么】
- 2 增加 登录按钮
- 3 航班列表优化（从“只有前一天后一天”到“可以显示最近5天”）
- 4 默认显示中转报价
- 5 qmall商城
- 6 紧急换掉线上链接
- 7 大数据风险平台
- 8 修改工商e生活style

## 二、项目细节

### 1 修改部分浏览器返回不刷新页面，loading一直存在问题【为什么】
> 问题：一般返回loading不都应该继续存在吗？为什么会消失？为什么会不消失？

---
### 2 增加 登录按钮

#### 1、 技术要点

- 使用java的vm模板（比较古老）
- 调用函数不能用js的api，需要写java函数来对数据进行处理
- 修改一些样式（绝对定位到顶端）

#### 2、学习到了什么
- 这是我刚来实习的给我分配的比较简单的需求，因为是java工程，所以选择使用IDEA这个软件来打开工程，是用里面的MAVEN；
- 因为项目比较古老，是用的是java的vm模板，项目一直在慢慢重构中，我写的需求部门还没有改过来；
- 因为要增加登录功能，我便在整个工程中来搜索哪个对象存储了相关信息，以及使用方法；
- 学习到了：环境配置方法、搜索定位的能力；
#### 3、时间
- 1天

`clean package -U -Pdevtc1 -Djetty.port=8080 jetty:run`

`#set($loginUrl = "//user.qunar.com/mobile/login.jsp?ret=" + $URLUtil.encode($!req.url))`

```java
public class URLUtil {
	private static final Logger LOG = LoggerFactory.getLogger(URLUtil.class);
	private static final String CHARSET_DEFAULT = "utf-8";

    private static final Pattern CHINESE_PATTERN = Pattern.compile("=([\\u4e00-\\u9fa5]+)");

	/**
	 * 字符串编码 指定编码
	 * @param str
	 * @param charset
	 * @return
	 */
	public static String encode(String str, String charset) {
			if (StringUtils.isBlank(str)) {
				return null;
			}
			try {
				return URLEncoder.encode(str, charset);
			} catch (UnsupportedEncodingException e) {
				LOG.error("TouchStringUtil.encode UnsupportedEncodingException error,str:"+ str, e);
			} catch (IllegalArgumentException e) {
				LOG.error("TouchStringUtil.encode IllegalArgumentException error,str:"+ str, e);
			}
			return null;
	}
}
```




---
### 3 航班列表优化（从“只有前一天后一天”到“可以显示最近5天”）
#### 1、 需求：
- 每页显示5个日期，一般展示中间的那个日期
- 如果到最近一天或最后一天不再继续滑动
- 希望点击多次只发送最后一次请求；
- 希望多次点击时候只显示一个loading；

#### 2、技术方案：
- 有的网站官网是用直接往html上面显示300多个
- 我思考显示9个，也就是五个左边右边都多放2个，滑动之后再换
- 父元素relative，9个子元素absolute，父元素transform:translateX()
- 子元素滑动几个就改变开头或结尾到相对的开头或者结尾
- 函数防抖：
 
```javascript
//函数防抖，输入一个方法，返回防抖后的方法,最后一个参数用于是否立即执行
export function debounce(method, context, delay, immediate) {
    let timer,calling,callingTimer;
    return (a) =>{
        if(immediate) {
            if(calling) {
                clearTimeout(callingTimer);
                callingTimer = setTimeout(()=>{
                    calling = false;
                },delay);
            } else {
                method.call(context,a);
                calling = true;
                callingTimer = setTimeout(()=>{
                    calling = false;
                },delay);
            }
        } else {
            clearTimeout(timer);
            timer = setTimeout(() =>{
                method.call(context,a);
            }, delay);
        }
    }
}
```


#### 3、时间
- 4天

#### 4、学习到了什么
- 因为这个技术方案比较复杂，数学逻辑比较复杂，我同时还有别的需求在身，写出了自己的本地demo，但最后没有让我写进工程里面；
- 但最后的还尝试过最开始显示9个，点到后面在多append几个div进去，这个方案也没用；
- 最后是使用的9个是用margin-left，直接变的方案，这个方案较简单，会闪一下，但用户看不出来；


---
### 4 默认显示中转报价
#### 1、需求
- 这是跟后台一起规定好的接口，之前默认是直达数据，点击页面下面的按钮才会变成显示中转数据；
- 现在需要改成 后台显示什么就显示什么；

#### 2、问题
- 本来在工程开头的一个跟后台规定好的接口 改个值 就好了；
- 但是由于按钮展示方式哪块的代码的设计和接口设计方式并不符合，所以不能只改一个值；
- 于是我将相关代码逻辑改进了的同时，删除了一些没必要的代码；

#### 3、学习到了什么
- 这中间使用的是react-redux，redux的基础知识并不熟悉，所以照猫画虎的修改了代码，
`mapStateToProps` `action` `state` `reduce`
- 后来又熟悉了下redux


### 5 qmall商城
#### 1、需求
- 这是一个公司封装的框架，是1.0版本，使用的还是es5，`require`,`module.exports`；
- 库存组件增加库存显示功能；
- 增加活动判断，登录，是否会员，是否学生；
- 调用弹窗组件；
- 返回按钮恢复默认返回浏览器历史纪录（即回到其他跳转过来的页面）；
- 修改线上bug；
- 重构页面后台录入模板，样式；
- 修改公司工程判断中的严重阻断代码；

#### 2、遇到的问题
- 工程使用的是公司封装的不再维护的老框架，我需要学习里面的基本使用方式，以及看懂代码结构找到对应的需求代码的位置，刚开始花费了不少时间来学习；
- 需要调用后台接口，怎么来用这个架构来发送get请求，怎么来判断，怎么跳转，这所有的逻辑也是之前没有怎么接触过的；
- 商品id的跳转，是根据页面hash值改变来跳转的，而使用`location.href`改变url，如果仅仅改变的是`#`后面的值，页面并不刷新跳转，需要手动刷新(`location.reload()`)，如果跳转的是不一样的域名,加了`location.reload`又会导致页面跳转失败，最后解决方案是：判断域名是否变化，再来决定是否`reload()`;

#### 3、学习到了什么
- 由于这个项目虽然是在以前的基础上增加的一些需求，但依旧是自己一个人负责，所以全程为了找到对应的代码的位置，debug的能力提升了很多；
- 感觉自己看代码定位问题的能力比我刚实习的时候提高了很多，以前对不是自己写的代码感觉很恐惧，但现在提出了问题所在，已经可以很快通过“用chrome看接口、工程信息”，“工程里搜索相关关键字”，“通过设置断点寻找问题代码行”，“通过chrome开发者工具查看相关对象值，设置相关值来改变”，“css问题通过computed查看被设置的具体css定位”等方式来解决问题，感觉自己再也不畏惧看任何复杂的工程；
- 这也是我第一次独立跟后台同学接触联调，商量接口信息等，自己在前后端配合，请求后端接口等方面有了很大的提高，自己对get，post数据传输方式进行了较深入的理解；

#### 4、时间
- 好几周

### 6 紧急换掉线上链接
#### 1、需求
- 之前发现公司网站被chrome浏览器判定为含有危险链接的网站，后来排查是Android手机下载链接里出现了问题，换下了网站所有安卓的链接；
- 现在要求我紧急换上去；

#### 2、学到了什么
- 其实这是个比较简单的问题，但是由于时间紧迫，之前也不是我换下去的，我也并不知道到底哪些地方改动了，需要去询问人，紧急调用qa资源（   qa资源比较紧缺），还要配置环境来自测，感觉到了比较大的压力，自己的抗压能力得到了提升；
- 之前在排查这个问题的时候，自己也尝试发现问题，猜到了可能是app的问题，后来果然是


### 7 大数据风险平台
#### 1、需求
- 制作一个大数据风险展示平台
- 内容包括：导航，数据折线图展示，数据表格展示，页面之间数据相互跳转

#### 2、难点
- 对于我来说最大的难点是怎么开始这个项目；
- 我不能像以前自己随便写几个html，因为是公司的项目；
- 而且，因为每个页面也有能复用的部分，肯定需要写成模块化；
- 咨询了tl，建议我使用handlebar,jquery,ykit(公司封装的webpack)，自己没有使用过，需要学习；
- 没有ui设计，只有文字版需求文档，我只能看着写；
- 给的时间只有几天，就要联调，感觉只有自己亚历山大；
- 大leader希望我全都用之前写好的一个table查询组件来写，但经过学习之后，发现并不能完美的完成需求，跟后端商量需求也需要一些时间；

#### 3、学习到了什么
- 从头开启一个项目，学习如何使用公司的ykit来开启一个项目，学习如何
使用handlebar，学习如何使用handlebar的loader来解析；
- 最开始先尝试使用写html基本的页面，然后封装成一个一个组件，然后进行优化；
- 写成模块化，`require``module.exports`互相引用js；
- 把css改写成scss；
- 页面写成单页面，根据hash值来判断页面渲染内容；

### 8 修改工商e生活style
#### 1、需求
- 工行app增加qunar机票首页链接，根据cookie判断接入接口，然后将页面风格改成工行的样子；
- 除了css，还要去掉一些指定的广告；
- 返回按钮要改成调用工行的返回的js；

#### 2、 技术难点，遇到的问题
- 调用样式是先将请求发送到node工程，node工程根据页面传参来判断接入app，然后返回对应的css文件到页面，从而更改页面的样式；
- 页面首页是java工程，最开始无脑将所有类似的接入都改成新的接入，后来才知道大部分代码都已经被重构了，然后我又一个一个改回来；
- node工程的调试弄了好久，我将router.js文件从头到尾调式了一遍，看懂了原理，同时知道了原来nodejs也可以debugger；
- nginx和charles都更熟练了；
- 