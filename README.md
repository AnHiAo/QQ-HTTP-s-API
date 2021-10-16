# QQhttp(s)API接口整合

## 更新模式
佛系更新(不急也不慢)🙏
## 分类问题
因为你🐧的接口也是超级乱的,所以每个分类的话是按照实际的<strong>功能效果</strong>去分类而非按照接口的意义去分类
## 简介
<p>嘛,如果你能发现到这里就说明你对作者还是有大大滴关注,那么如果在您使用的基础上觉得好用并且想 <strong>分享</strong>其他地方
麻烦带上<strong>本仓库地址</strong><img src="https://pic.stackoverflow.wiki/uploadImages/58/152/85/120/2021/10/14/21/28/0b4f0ba0-ce29-4ef7-86a5-069862c25526.gif" /></p>

<details><summary>公共关键值操作<img src="https://pic.stackoverflow.wiki/uploadImages/58/152/85/187/2021/10/16/16/12/a1101de2-47d9-4f28-984d-5985ebb8aa6a.svg" width="33.33vw" /></summary>
<table>
	<tr>
	  <th>name</th>
  <th>status</th>
  <th>url</th>
  <th>stage</th>
	</tr>
	<tr></tr>
	<tr>
    <td>get_base_key(ldw值)</td>
    <td><img src="https://pic.stackoverflow.wiki/uploadImages/13/113/104/116/2021/09/05/10/20/3b2fa54f-03b9-4c5a-abcf-845149399700.svg" width="26.6666666vw"/></td>
    <td>https://id.qq.com/cgi-bin/get_base_key?r=随机小数(0-1)</td>
    <td>
    <details>
     <summary>例</summary>
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
	<tr></tr>
	<tr>
		 <td>get_join_k(k值)</td>
		 <td><img src="https://pic.stackoverflow.wiki/uploadImages/13/113/104/116/2021/09/05/10/20/3b2fa54f-03b9-4c5a-abcf-845149399700.svg" width="26.6666666vw"/></td>
		 <td>https://qun.qq.com/proxy/domain/admin.qun.qq.com/cgi-bin/qun_admin/get_join_k</td>
		 <td><details><summary>例</summary>
			 POST<pre>https://qun.qq.com/proxy/domain/admin.qun.qq.com/cgi-bin/qun_admin/get_join_k</pre>
			 headers
			 <pre>
 "User-Agent": 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36',
 "Referer": "https://qun.qq.com/join.html",
 "Cookie": `uin=o114514; skey=MHcvBvCHdT; p_uin=o114514; p_skey=0yJENlMiruFp8XCoHvgi267qbg9j60o65N6gVrJm2Cs_;`,
   // p_uin、uin=o你的QQ号 skey、p_skey自行提取
			 </pre>
			 data
			 <pre>
			 gc=114514114&bkn=714093860
			 // gc QQ群号
			 // bkn 获取bkn值
			 </pre>
			 result
			 <pre>
			 {"ec":0,"errcode":0,"em":"","k":"TemikiPyqA7GFiyMlGv4pC6gAfYIrIs"} //k值
			 </pre>
			 </details></td>
	 </tr>
  <tr>
	 </tr>
	 <tr>
		 <td>getCSRFToken(使用<strong>cookie</strong> 的 <strong>skey</strong>手动算出<strong>bkn值</strong>)</td>
		 <td><img src="https://pic.stackoverflow.wiki/uploadImages/13/113/104/116/2021/09/05/10/20/3b2fa54f-03b9-4c5a-abcf-845149399700.svg" width="26.6666666vw"/></td>
		 <td><img src="https://pic.stackoverflow.wiki/uploadImages/218/18/112/68/2021/10/15/04/21/76cb0a3a-5c39-493c-b104-9d56b194abe7.png"  /></td>
		 <td><details><summary>例</summary></details></td>
	 </tr>
	</table>
</details>
	
	
<details >
 <summary>find.qq.com检查指定QQ是否在线(该项暂时停止)<img src="https://pic.stackoverflow.wiki/uploadImages/13/113/104/116/2021/09/05/10/20/580168a9-02a9-4849-8446-d6e9b776143f.svg" width="26.6666666vw"/></summary>
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
 <summary>QQ个人操作相关<img src="https://pic.stackoverflow.wiki/uploadImages/2400/8902//f03c/92ff/fec3/ed69/2021/10/16/03/16/10934a21-4da7-4e7c-8125-c41cd1e84ac4.svg" width="33.3333vw" /></summary>

 <table>
 <tr>
  <th>name</th>
  <th>status</th>
  <th>url</th>
  <th>stage</th>
  </tr>
  
  <tr>
   </tr>
   

  <tr>
   <td>获取成长信息</td>
   <td><img src="https://pic.stackoverflow.wiki/uploadImages/13/113/104/116/2021/09/05/10/20/3b2fa54f-03b9-4c5a-abcf-845149399700.svg" width="26.6666666vw"/></td>
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
	 <tr></tr>
  <tr>
		 <td>获取好友信息列表</td>
		 <td><img src="https://pic.stackoverflow.wiki/uploadImages/13/113/104/116/2021/09/05/10/20/3b2fa54f-03b9-4c5a-abcf-845149399700.svg" width="26.6666666vw"/></td>
		 <td>https://qun.qq.com/cgi-bin/qun_mgr/get_friend_list?&bkn=(bkn值)</td>
		 <td><details><summary>例</summary>
			 GET<pre>https://qun.qq.com/cgi-bin/qun_mgr/get_friend_list?&bkn=714093871</pre>
			 headers
			 <pre>
 "User-Agent": 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36',
 "Referer": "https://qun.qq.com/cgi-bin/qun_mgr/get_friend_list",
 "Cookie": `uin=o114514; skey=MHcvBvCHdT; p_uin=o114514; p_skey=0yJENlMiruFp8XCoHvgi267qbg9j60o65N6gVrJm2Cs_;`,
 // p_uin、uin=o你的QQ号 skey、p_skey自行提取
			 </pre>
			 result
			 <pre>
 {
	"ec": 0,
	"errcode": 0,
	"em": "",
	"result": {
	    "0": {
		"mems": [{  // name 昵称 uin QQ号
			"name": "babyQ",
			"uin": 66600000
			}]
			
		}
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
 <summary>QQ群操作相关<img src="https://pic.stackoverflow.wiki/uploadImages/2400/8902//f03c/92ff/fec3/ed69/2021/10/16/03/10/f036e328-455c-4cf3-b3e9-4951e1a16b34.svg" width="33.3333vw" /></summary>
 <table>
  <tr>
  <th>name</th>
   <th>status</th>
  <th>url</th>
  <th>stage</th>
  </tr>
	 <tr></tr>
	 
	 
  <tr>
   <td>获取群列表</td>
   <td><img src="https://pic.stackoverflow.wiki/uploadImages/13/113/104/116/2021/09/05/10/20/3b2fa54f-03b9-4c5a-abcf-845149399700.svg" width="26.6666666vw"/></td>
   <td>https://qun.qq.com/cgi-bin/qun_mgr/get_group_list?bkn=(bkn值)
   </td>
   <td>
    <details>
     <summary>例</summary>
     GET<pre>https://qun.qq.com/cgi-bin/qun_mgr/get_group_list?bkn=723150396</pre>
     headers
     <pre>
 "User-Agent": 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36',
 "Referer": "https://qun.qq.com/join.html",
 "Cookie": `uin=o114514; skey=MHcvBvCHdT; p_uin=o114514; p_skey=0yJENlMiruFp8XCoHvgi267qbg9j60o65N6gVrJm2Cs_;`,
  // p_uin、uin=o你的QQ号 skey、p_skey自行提取
     </pre>
     result
     <pre>
 {
"ec": 0,
"errcode": 0,
"em": "",
"join": [{
	"gc": 114154114154,　// 群号
	"gn": "这么说你很勇哦?", // 群名
	"owner": 114154 // 群主QQ号
 }]
}
     </pre>
    </details>
   </td>
  </tr>
	 <tr></tr>
  <tr>
	  <td>获取指定群的<strong>详细信息</strong></td>
	  <td><img src="https://pic.stackoverflow.wiki/uploadImages/13/113/104/116/2021/09/05/10/20/3b2fa54f-03b9-4c5a-abcf-845149399700.svg" width="26.6666666vw"/></td>
	  <td>https://qinfo.clt.qq.com/cgi-bin/qun_info/get_group_info_all?gc=(QQ群号)&bkn=(bkn值)</td>
	  <td><details>
		  <summary>例</summary>
		  GET<pre>https://qinfo.clt.qq.com/cgi-bin/qun_info/get_group_info_all?gc=114514114514&bkn=1841247401</pre>
		  headers
		  <pre>
 "User-Agent": 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36',
 "Referer": "https://qinfo.clt.qq.com/qinfo_v3/member.html?groupuin=",
 "Cookie": `uin=o114514; skey=MHcvBvCHdT; p_uin=o114514; p_skey=0yJENlMiruFp8XCoHvgi267qbg9j60o65N6gVrJm2Cs_;`,
  // p_uin、uin=o你的QQ号 skey、p_skey自行提取
		  </pre>
		  result
		  <pre>
{
    "ec": 0,
    "errcode": 0,
    "em": "",
    "gc": 114514114514, // QQ群号
    "gBoard": "",
    "gOwner": 114514, // QQ群主号
    "gName": "先辈 ~ !", // QQ群名
    "gMemNum": 4, // QQ群成员数
    "gMaxMem": 200, // QQ群最多成员数
    "gLevel": 0, // QQ群活跃等级
    "gCrtTime": 1617205505,
    "gSpeClass": 0,
    "classID": 34,
    "flag": 3,
    "gtype": 0,
    "ac_grade": 0,
    "ac_num": 3,
    "class": "",
    "gIntro": "",
    "gRIntro": "",
    "conf_mGFace": 1,
    "conf_mGName": "1",
    "pos": "0|0.000000|0.000000|",
    "app_privilege_flag": 67698880,
    "search": 0,
    "auth": 0,
    "open": 0,
    "photo": {
        "f": 0
    },
    "share": {
        "f": 0
    },
    "edu": 0,
    "gAdmins": [ // QQ群管理账号列表
        114514114514,
        114514514,
        114114514
    ],
    "ns": {    //群管理和群主混合数据 (账号:昵称)
        "114514114514": "先辈先辈",
        "114514514": "先辈辈",
        "114114514": "先先辈",
        "114514": "先辈"
    },
    "levelname": { // 群等级制度
        "lvln1": "潜水",
        "lvln2": "冒泡",
        "lvln3": "吐槽",
        "lvln4": "活跃",
        "lvln5": "话唠",
        "lvln6": "传说",
        "lvln101": "LV.1",
        "lvln102": "LV.2",
        "lvln103": "LV.3",
        "lvln104": "LV.4",
        "lvln105": "LV.5",
        "lvln106": "LV.6",
        "lvln107": "LV.7",
        "lvln108": "LV.8",
        "lvln109": "LV.9",
        "lvln110": "LV.10",
        "lvln111": "LV.11",
        "lvln112": "LV.12",
        "lvln113": "LV.13",
        "lvln114": "LV.14",
        "lvln115": "LV.15",
        "lvln116": "LV.16",
        "lvln117": "LV.17",
        "lvln118": "LV.18",
        "lvln197": "小酋长",
        "lvln198": "大酋长",
        "lvln199": "首席酋长",
        "lvln10": "一见倾心",
        "lvln11": "超凡脱俗",
        "lvln12": "风华绝代",
        "lvln13": "崭露头角",
        "lvln14": "金玉满堂",
        "lvln15": "富甲一方"
    },
    "level_def": 0,
    "user_show": 1,
    "sys_show": 1,
    "tags": ""
}
		  </pre>
	 </details></td>
	 </tr><tr></tr>
	 <tr>
		 <td>获取群成员群<strong>操作时间</strong>等配置</td>
		 <td><img src="https://pic.stackoverflow.wiki/uploadImages/13/113/104/116/2021/09/05/10/20/3b2fa54f-03b9-4c5a-abcf-845149399700.svg" width="26.6666666vw"/></td>
		 <td>https://qinfo.clt.qq.com/cgi-bin/qun_info/get_members_info_v1?gc=(QQ群号)&bkn=(bkn值)</td>
		 <td><details><summary>例</summary>
			 GET<pre>https://qinfo.clt.qq.com/cgi-bin/qun_info/get_members_info_v1?gc=114514114&bkn=1841247402</pre>
			 headers
			 <pre>
 "User-Agent": 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36',
 "Referer": "https://qinfo.clt.qq.com/qinfo_v3/member.html?groupuin=",
 "Cookie": `uin=o114514; skey=MHcvBvCHdT; p_uin=o114514; p_skey=0yJENlMiruFp8XCoHvgi267qbg9j60o65N6gVrJm2Cs_;`,
 // p_uin、uin=o你的QQ号 skey、p_skey自行提取
			 </pre>
			 result
			 <pre>
			 {
    "ec": 0,
    "errcode": 0,
    "em": "",
    "c": "16 32 45 51 62 ",
    "ext_num": 0,
    "level": 0,
    "mem_num": 4, // 群成员数量
    "max_num": 200, // 群成员最大数量
    "max_admin": 10, // 群管理最大数量
    "owner": 2274671088,
    "adm": [  // 群的绿帽子们(滑稽)
        114514114,
        114514114514,
        114514114514114
    ],
    "members": { 
     		 // lst 最后一次在群里发言时间(该使用了标准10位时间戳,转换时间需要乘以1000)
		 // jt 入群的时间(该使用了标准10位时间戳,转换时间需要乘以1000)
		 // 剩下其余参数不清楚 后期补全
        "114514": {
            "lst": 1634322548,
            "jt": 1617205505,
            "rm": 1,
            "lad": 30,
            "lp": 522,
            "ll": 3
        },
        "114514114": {
            "lst": 1628307654,
            "jt": 1618410450,
            "rm": 1,
            "lad": 9,
            "lp": 139,
            "ll": 2
        },
        "114514114514": {
            "lst": 1634220941,
            "jt": 1617205505,
            "rm": 1,
            "lad": 17,
            "lp": 269,
            "ll": 2
        },
        "114514114514114": {
            "lst": 1634298294,
            "jt": 1617205505,
            "rm": 0,
            "lad": 30,
            "lp": 505,
            "ll": 2
        }
    },
    "levelname": { // 群等级配置
        "lvln1": "潜水",
        "lvln2": "冒泡",
        "lvln3": "吐槽",
        "lvln4": "活跃",
        "lvln5": "话唠",
        "lvln6": "传说",
        "lvln101": "LV.1",
        "lvln102": "LV.2",
        "lvln103": "LV.3",
        "lvln104": "LV.4",
        "lvln105": "LV.5",
        "lvln106": "LV.6",
        "lvln107": "LV.7",
        "lvln108": "LV.8",
        "lvln109": "LV.9",
        "lvln110": "LV.10",
        "lvln111": "LV.11",
        "lvln112": "LV.12",
        "lvln113": "LV.13",
        "lvln114": "LV.14",
        "lvln115": "LV.15",
        "lvln116": "LV.16",
        "lvln117": "LV.17",
        "lvln118": "LV.18",
        "lvln197": "小酋长",
        "lvln198": "大酋长",
        "lvln199": "首席酋长",
        "lvln10": "一见倾心",
        "lvln11": "超凡脱俗",
        "lvln12": "风华绝代",
        "lvln13": "崭露头角",
        "lvln14": "金玉满堂",
        "lvln15": "富甲一方"
    }
}
			 </pre>
	         </details></td>
	 </tr>
	 <tr></tr>
	 <tr>
		 <td>获取<strong>指定QQ群</strong>加群链接</td>
		 <td><img src="https://pic.stackoverflow.wiki/uploadImages/13/113/104/116/2021/09/05/10/20/3b2fa54f-03b9-4c5a-abcf-845149399700.svg" width="26.6666666vw"/></td>
		 <td>https://qm.qq.com/cgi-bin/qm/qr?k=(获取get_join_k的值)&jump_from=webapi</td>
		 <td><details><summary>例</summary>
			 GET<pre>https://qm.qq.com/cgi-bin/qm/qr?k=TemikiPyqA7GFiyMlGv4pC6gAfYIrIs&jump_from=webapi //这里的k值是不存在的所以自然跳转不了加群</pre>	 
			 </details></td>
	 </tr>
 </table>
</details>
