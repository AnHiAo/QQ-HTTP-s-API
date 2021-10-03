# QQhttp(s)API接口整合

## 检查指定QQ是否在线(无视隐身状态)

### URL
`https://find.qq.com/proxy/domain/cgi.find.qq.com/qqfind/buddy/search_v3`

### 请求方式
`POST`

### Header
```
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
```

### 请求参数/Data
这里采用的是将对应的 `key:value` 的数据转换为 `key1=value1&key2=value2`
```
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
```

### 返回示例/Response
如果没在线或者Cookie失效的话返回
```json
{
    "retcode": 0, 
    "result": ""
}
```

在线的时候返回
```json
{
	"retcode": 0,
	"result": {
		"sret": 0,
		"exact": 0,
		"buddy": {
			"info_list": [{
				"uin": "10001",
				"nick": "Pony",
				"country": "在深圳",
				"province": "",
				"city": "",
				"gender": 1,
				"age": 120,
				"url": "http://thirdqq.qlogo.cn/g?b=oidb&k=ue9m0Xcttd9Yfu065rGBIw&s=100&t1612053871"
			}],
			"exact": "",
			"sessionid": 0
		},
		"qidian": "",
		"qiye": ""
	}
}
```

## 个人信息

### URL
`https://qun.qq.com/cgi-bin/qunwelcome/myinfo`

### 请求方式
`GET`

### 请求参数/Data
| 参数名   | 是否必须 | 说明 |
| -------- | -------- | ---- |
| callback | 是       |      |
| bkn      | 是       |      |

## 个人头像


### URL
`https://ssl.ptlogin2.qq.com/getface`

### 请求参数
| 参数名  | 是否必须 | 说明                          |
| ------- | -------- | ----------------------------- |
| imgtype | 是       | 参数值为1到4，最大140px*140px |
| uin     | 是       | QQ号                          |

## 好友列表

### URL
`https://qun.qq.com/cgi-bin/qun_mgr/get_friend_list`

### 请求方式
`GET`

### 请求参数
| 参数名 | 是否必须 | 说明 |
| ------ | -------- | ---- |
| bkn    | 是       |      |

## 群列表

### URL
`https://qun.qq.com/cgi-bin/qun_mgr/get_group_list`

### 请求方式
`GET`

### 请求参数
| 参数名 | 是否必须 | 说明 |
| ------ | -------- | ---- |
| bkn    | 是       |      |

## 群成员获取

### URL
`https://qun.qq.com/cgi-bin/qun_mgr/search_group_members`

### 请求方式
`GET`

### 请求参数
| 参数名 | 是否必须 | 说明                   |
| ------ | -------- | ---------------------- |
| gc     | 是       | 由群列表返回json中获取 |
| st     |          | 起始位置，由0开始      |
| end    |          | 终止位置，由0开始      |
| sort   |          | 0                      |
| bkn    | 是       |                        |
