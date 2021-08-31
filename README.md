# QQhttp(s)API接口整合
1.检查指定QQ是否在线(无视隐身状态)<br/>
`POST`
`https://find.qq.com/proxy/domain/cgi.find.qq.com/qqfind/buddy/search_v3`<br/><br/>
`Headers`<br/>
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



`Data`这里采用的是将对应的` key:value `的数据转换为` key1=value1&key2=value2 `<br/>
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

`Response` 如果没在线或者Cookie失效的话返回`{'retcode': 0, 'result': None}`<br/>
在线的时候返回`{'retcode': 0, 'result': {'sret': 0, 'exact': 0, 'buddy': {'info_list': [{'uin': '10001', 'nick': 'Pony', 'country': '在深圳', 'province': '', 'city': '', 'gender': 1, 'age': 120, 'url': 'http://thirdqq.qlogo.cn/g?b=oidb&k=ue9m0Xcttd9Yfu065rGBIw&s=100&t1612053871'}], 'exact': '', 'sessionid': 0}, 'qidian': None, 'qiye': None}}`
