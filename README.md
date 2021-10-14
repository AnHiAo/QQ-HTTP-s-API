# QQhttp(s)API接口整合
## 简介

<p>嘛,如果你能发现到这里就说明你对作者还是有大大滴关注,那么如果在您使用的基础上觉得好用并且想 <strong>分享</strong>其他地方
麻烦带上<strong>本仓库地址</strong><img src="https://pic.stackoverflow.wiki/uploadImages/58/152/85/120/2021/10/14/21/28/0b4f0ba0-ce29-4ef7-86a5-069862c25526.gif" /></p>


<details>
 <summary>find.qq.com 检查指定QQ是否在线(无视隐身状态)<img src="https://pic.stackoverflow.wiki/uploadImages/13/113/104/116/2021/09/05/10/20/580168a9-02a9-4849-8446-d6e9b776143f.svg" width="26.6666666vw"/></summary>
 <p>
 <pre> POST  https://find.qq.com/proxy/domain/cgi.find.qq.com/qqfind/buddy/search_v3</pre>
 <br/>
 
`Headers`
 <br/>

 <pre>
 "Host": "find.qq.com",
 "Connection": "keep-alive",
 "Content-Length": "182",
 "Accept": "application/json, text/javascript, */*; q=0.01",
 "Content-Type": "application/x-www-form-urlencoded; charset=UTF-8",
 "Origin": "https://find.qq.com",
 "User-Agent": "Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) QQ/9.4.9.27847 Chrome/43.0.2357.134 Safari/537.36 QBCore/3.43.1298.400   QQBrowser/9.0.2524.400",
 "X-Requested-With": "XMLHttpRequest",
 "Referer": "https://find.qq.com/index.html?version=1&im_version=5827&width=910&height=610&search_target=0",
 "Accept-Encoding": "gzip, deflate",
 "Accept-Language": "en-US,en;q=0.8",
 "Cookie":"需要获取QQCookie的uin和skey"   //例子 "Cookie": "uin=o100001; skey=Mzq161jo3w;"
</pre>
<br/>



`Data`   （这里采用的是将对应的` key:value ` -->` key1=value1&key2=value2 `）<br/>

<pre>
 "num":"20",
 "page":"0",
 "sessionid":"0",
 "keyword":10001(QQ号),
 "agerg":"0",
 "firston":"1",
 "video":"0",
 "country":"1",
 "province":"44",
 "city":"1",
 "district":"0",
 "hcountry":"1",
 "hprovince":"0",
 "online":"1",
 "ldw":"2144551309"
</pre>

`Response` <br/>
如果 没在线或者`Cookie`失效、对方`发现我的方式`关闭了`通过QQ号发现`<br/>

`{'retcode': 0, 'result': None}`

在线<br/>

`{'retcode': 0, 'result': {'sret': 0, 'exact': 0, 'buddy': {'info_list': [{'uin': '10001', 'nick': 'Pony', 'country': '在深圳', 'province': '', 'city': '', 'gender': 1, 'age': 120, 'url': 'http://thirdqq.qlogo.cn/g?b=oidb&k=ue9m0Xcttd9Yfu065rGBIw&s=100&t1612053871'}], 'exact': '', 'sessionid': 0}, 'qidian': None, 'qiye': None}}`
</p>
</details>

<details>
 <summary>id.qq.com 我的QQ中心<img src="https://pic.stackoverflow.wiki/uploadImages/13/113/104/116/2021/09/05/10/20/3b2fa54f-03b9-4c5a-abcf-845149399700.svg" width="26.6666666vw"/></summary>

 <table>
 <tr>
  <th>name</th>
  <th>url</th>
  <th>stage</th>
  </tr>
  
  <tr>
   </tr>
   <tr>
    <td>get_base_key(获取ldw值)</td>
    <td>https://id.qq.com/cgi-bin/get_base_key?r=随机小数(0-1)</td>
    <td>
    <details>
            <summary>例</summary>
            例:<br/>
            GET<pre>https://id.qq.com/cgi-bin/get_base_key?r=0.5524111020965228</pre>
            headers
            <pre>
   "User-Agent": 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML,  like Gecko) Chrome/94.0.4606.81 Safari/537.36',
    "Referer": "https://id.qq.com",
    "Cookie": "  uin=o0123456; skey=@NYPUcpjXh; p_uin=o0123456;           p_skey=oNmCDeKR8b8rcOpkVPIzR9CAjjj7t-bUxsynqAkalWI_; "
     // 需要修改 uin=o0你的QQ号 skey=自行cookie提取 p_uin=o0你的QQ号 p_skey=自行cookie提取 
            </pre>
            result(该项提取 <mark>header</mark> 里面的 <mark>set-cookie</mark> )
            <pre>
            'set-cookie': 'ldw=7841f781c7f0e7f7acbdd00d53a5f53fa5f0a63d40a0969d; Domain=id.qq.com; Path=/'
            </pre>
    </details>
    </td>
  
  </tr>
  <tr>
  </tr>
  <tr>
   <td>获取QQ成长信息</td>
   <td>https://id.qq.com/cgi-bin/qqlevel?page_type=1&idw=(get_base_key提取出来的值)&r=随机小数(0-1)</td>
   <td>
       <details>
           <summary>例</summary>
         GET<pre>https://id.qq.com/cgi-bin/qqlevel?page_type=1&idw=(get_base_key提取出来的值)&r=0.9265129733481445</pre>
         headers
         <pre>
           "User-Agent": 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36',
        "Referer": "https://id.qq.com",
        "Cookie": `uin=o0123456; skey=@NYPUcpjXh; RK=xcDMmgj+OJ; p_uin=o0123456; p_skey=oNmCDeKR8b8rcOpkVPIzR9CAjjj7t-bUxsynqAkalWI_;ldw=c8cf578ba618815d667dc29e9d9e77459c037f69543f62fb;`
        // 需要修改 uin=o0你的QQ号 skey=自行cookie提取 p_uin=o0你的QQ号 p_skey=自行cookie提取   ldw=(get_base_key提取出来的值)
         </pre>
         result
        <pre style="height:33.333vh;overflow:auto;">
              {
        	"PCMgr": {
        		"cur": 0,
        		"speed": "1"
        	},
        	"QQVipLevel": 0,
        	"QQVipSpeed": "1.0",
        	"QQVipYear": 0,
        	"QplusOnlineTimes": 0,
        	"TYQQCard": {
        		"cur": 0,
        		"speed": "0.2"
        	},
        	"chargeTel": {
        		"cur": 0,
        		"speed": "0.5"
        	}, 
        	"chat": {
        		"cur": 0,
        		"speed": "0.1",
        		"total": 5
        	},
        	"days": 6245, // QQ活跃天数days
        	"ec": 0,
        	"isDaren": 0,
        	"isQQVip": 0, // 是否QQ会员
        	"isSuperQQ": 0,  //是否超级QQ
        	"isSuperVip": 0, // 是否超级会员
        	"latesVersion": {
        		"cur": 0,
        		"speed": "0.1"
        	},
        	"level": 77, // QQ等级
        	"login": {
        		"cur": 0,
        		"speed": "0.1",
        		"total": 6
        	},
        	"medal": {
        		"cur": 0,
        		"speed": "0.2"
        	},
        	"msg": {
        		"cur": 0,
        		"speed": "0.1",
        		"total": 50
        	},
        	"onlineTimes": 0,
        	"onlineTotalTimes": 0,
        	"pinyin": {
        		"cur": 0,
        		"speed": "0.1"
        	},
        	"qplus": {
        		"cur": 0,
        		"speed": "0.1",
        		"total": 5
        	},
        	"remainDays": 151, // "距升级到 (当前等级 + 1) 级原需要 (remainDays) 天
        	"shouQ": { 
        		"onlineTimes": 58291, // 已连续在线(onlineTimes / 3600) -->四舍五入取时间
        		"speedRule": 1
        	},
        	"superQQLevel": 0,
        	"superQQMqing": 0,
        	"superQQRealSpeed": "0.0",
        	"superQQSpeed": "0.0",
        	"superQQYear": 0,
        	"superVipBasicSpeed": 0, //超级会员的成长速度
        	"visible": {   // 非隐身在线数据
        		"cur": 124,
        		"invisible": 0,
        		"speed": "0.2",
        		"total": 120
        	},
        	"weibo": {
        		"cur": 0,
        		"level": 0,
        		"speed": "0.1"
        	},
        	"xiaochu": {
        		"cur": 0,
        		"speed": "0.2"
        	}
        }
        </pre>
       </details>
   </td>
  </tr>
 </table>
 
    

 <br/>
</details>
<details>
 <summary>qun.qq.com QQ群集合 </summary>
 <table>
  <tr>
  <th>name</th>
  <th>url</th>
  <th>stage</th>
  </tr>
  <tr>
   </tr>
  <tr>
   <td>获取群列表</td>
   <td>https://qun.qq.com/cgi-bin/qun_mgr/get_group_list?bkn=获取bkn值<br/>
    也可以通过 <strong>cookie</strong> 的 <strong>skey</strong> 值通过运算出 <strong>bkn值</strong>
   <img src="https://pic.stackoverflow.wiki/uploadImages/218/18/112/68/2021/10/15/04/21/76cb0a3a-5c39-493c-b104-9d56b194abe7.png" />
   </td>
   <td>
    <details>
     <summary>施工中...</summary>
    </details>
   </td>
  </tr>
 
 </table>
</details>
