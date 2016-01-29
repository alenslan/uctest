# **苹果商店API文档**  
---

* [<strong>苹果商店API文档</strong>](#苹果商店api文档)
  * [<strong>规格说明</strong>](#规格说明)
  * [<strong>http请求头部参数</strong>](#http请求头部参数)
  * [<strong>请求/返回body实体</strong>](#请求返回body实体)
  * [<strong>http返回header头部参数</strong>](#http返回header头部参数)
  * [<strong>返回状态码</strong>](#返回状态码)
  * [<strong>错误信息error</strong>](#错误信息error)
  * [<strong>修订历史</strong>](#修订历史)
  * [<strong>host配置文件地址</strong>](#host配置文件地址)
  * [<strong>app_base_info</strong>](#app_base_info)
* [<strong>接口</strong>](#接口)
  * [1.启动app时预加载主页及其他信息](#1启动app时预加载主页及其他信息)
  * [2.首页精选](#2首页精选)
  * [3.首页专题列表](#3首页专题列表)
  * [4.专题详情页](#4专题详情页)
  * [5.应用列表](#5应用列表)
  * [6.游戏列表](#6游戏列表)
  * [7.软件/游戏分类](#7软件游戏分类)
  * [8.分类详情页](#8分类列表页)
  * [9.应用详情页](#9应用详情页)
  * [10.搜索框自动匹配](#10搜索框自动匹配)
  * [11.应用搜索结果页](#11应用搜索结果页)
  * [12.免费榜单接口](#12免费榜单接口)
  * [13.收费榜单接口](#13收费榜单接口)
  * [14.畅销榜单接口](#14畅销榜单接口)
  * [15.榜单详情接口](#15榜单详情接口)
  * [16.壁纸列表接口](#16壁纸列表接口)
  * [17.表情包系列列表接口](#17表情包系列列表接口)
  * [18.单表情包列表接口](#18单表情包列表接口)
  * [19.表情包分享计数接口](#19表情包分享计数接口)
  * [20.检测设备是否领取APPST账号接口](#20检测设备是否领取APPST账号接口) 

#### **规格说明**
|/|说明|
|-----|-------|
|版本|v1.0|
|协议版本|v3.0|
|调用方式|HTTP RESTFUL [GET POST PUT DELETE]|
|返回格式|二进制加密数据|
|返回数据|{ data:{}, message:{}, error:{}}只有data时，则直接返回data里面的数据|

<br>
#### **http请求头部参数**
|参数|说明|
|----|---------------|
|X-Client-Info|公共参数，包括如下：<br>uuid：设备唯一标识<br>imei：机器码<br>version：客户端版本<br>version_code：客户端版本代号<br>os_version：操作系统版本<br>device：设备型号<br>metrics：设备分辨率480X800<br>channel：渠道别名<br>access_token：用户登录后服务器返回的用户token，作每次请求的验证串|
|X-Update-Time|api最后更新时间|

<br>
#### **请求/返回body实体**
值为MCrypt(base64_encode(msgpack(data)))
> key为本地秘钥，data为post提交数据或返回数据（json格式）

<br>
#### **http返回header头部参数**
|参数|类型|说明|
|---|---|---|
|X-Links|{<br>"next_page":"http://api.example.com/x?x=x",<br>"last_page":"http://api.example.com/x?x=x"<br>}|上一页，下一页链接（列表页数据接口会有该参数返回）|
|X-Update-Time|2015-09-09 10:10:00|api最后更新时间|
|X-Retry-After|3600(s)|服务器恢复时间（503错误时会返回该参数）|

#### **返回状态码**
|status值|说明|
|---|---|
|200|get请求成功|
|201|post请求成功，并创建服务器资源|
|301|原url已废弃，跳转至资源所在处url（永久）|
|302|重定向url，并发起get请求（暂时）|
|303|允许post请求|
|304|请求成功，但不更新内容|
|400|请求错误，当header参数格式错误或body解析错误|
|401|请求未授权|
|403|请求被拒绝|
|404|找不到资源|
|405|请求方式错误|
|408|请求超时|
|413|请求body实体太大|
|414|请求url太长|
|422|参数错误，返回error信息|
|500|服务器出错|
|502|无法链接服务器|
|503|服务器维护中，header会有服务器恢复时间Retry-After参数|
|504|网关超时|

<br>
#### **错误信息error**
|错误名称|描述|
|---|---|
|missing|资源不存在|
|missing_field|缺少参数|
|invalid|格式错误或参数无效|
|already_exists|字段（唯一索引）存在相同值|
```
{
    "message": "验证错误",
    "errors": [
        {
            "field": "title",
            "code": "missing_field"
        }
        ...
    ]
}
```

<br>
#### **修订历史**
|版本|修改说明|修改人|
|---|---|---|
||||

<br>
#### **host配置文件地址**
http://192.168.5.132/hosts.json
```
{
    "server_host":"http://192.168.5.132/api"
}
```

<br>
#### **app_base_info**
|参数名|类型|说明|
|---|---|---|
|id|int|应用ID|
|appstore_id|int|appstore ID|
|file_size_bytes|int|应用大小单位字节|
|name|string|应用名称|
|alias|string|别名|
|package_name|string|应用包名|
|version|string|应用版本|
|author|string|作者|
|price|float|应用价格|
|icon_urls|string|icon地址|
|view_url|string|appstore应用地址|
|reviews|string|一句话点评|
|average_user_rating|int|应用评分|
|user_rating_count|int|评分数量|
|type|string|apps=>应用，games=>游戏|
|release_date|date|应用发布日期|

<br>
## **接口**
# 1.启动app时预加载主页及其他信息

请求地址：{server_host}/start

|Request|Method : GET||
|---|---|---|
|参数名|类型|说明|
|/|/|/|
|**Respone**|**DataType : json**||
|参数名|类型|说明|
返回数据格式

```json
{
    "index":[$data],
    "apps":[$data],
    "games":[$data]
}
```

$data数据格式

```
[
    {
        "type":"tabs",
        "data":[
            {"title":"精选","active":"true","url":"/index"},
            {"title":"专题","active":"false","url":"/topics"},
            {"title":"大作","active":"false","url":"/games?type=epic"},
            {"title":"必备","active":"false","url":"/apps?type=necessary"},
        ]
    },
    {
        "type":"carousel",
        "data":[
            {
                "type":"app",
                "image_url":"",
                "id":1
            },
            {
                "type":"topic",
                "image_url":"",
                "id":2
            }
            ...
        ]
    },
    {
        "type":"app",
        "data":"{app_base_info}"
    },
    {
        "type":"app",
        "data":"{app_base_info}"
    },
    {
        "type":"app",
        "data":"{app_base_info}"
    },
    {
        "type":"banner",
        "data":{
            "image_url":"",
            "topic_id":12
        }
    }
    ...
]
```
> 注：接口2返回数据跟data结构相同 

<br>
# 2.首页精选

请求地址：{server_host}/index

|Request|Method : GET||
|---|---|---|
|参数名|类型|说明|
|page|int|页数|
|**Respone**|**DataType : json**||
|接口2返回数据跟data结构相同|

<br>
# 3.首页专题列表

请求地址：{server_host}/topics

|Request|Method : GET||
|---|---|---|
|参数名|类型|说明|
|page|int|页数|
|**Respone**|**DataType : json**||
|返回数据格式|||
```
[
    {
        "type":"topic",
        "data":{
            "title":"周年盛典版震撼开启",
            "image_url":"",
            "topic_id":12
        }
    },
    {
        "type":"topic",
        "data":{
            "title":"周年盛典版震撼开启xxx",
            "image_url":"",
            "topic_id":13
        }
    },
    ...
]
```

<br>
# 4.专题详情页

请求地址：{server_host}/topics/{id}

|Request|Method : GET||
|---|---|---|
|参数名|类型|说明|
|page|int|页数|
|**Respone**|**DataType : json**||
|返回数据格式|||
|待定|||

<br>
# 5.应用列表

请求地址：{server_host}/apps

|Request|Method : GET||
|---|---|---|
|参数名|类型|说明|
|page|int|页数|
|type|string|类型 软件最新/软件排行（new/rank）|
|**Respone**|**DataType : json**||
|返回数据格式|||
```
[
    {
        "type":"app",
        "data":"{app_base_info}"
    },
    {
        "type":"app",
        "data":"{app_base_info}"
    },
    ...
]
```

<br>
# 6.游戏列表

请求地址：{server_host}/games

|Request|Method : GET||
|---|---|---|
|参数名|类型|说明|
|page|int|页数|
|type|string|类型 游戏最新/游戏排行（new/rank）|
|**Respone**|**DataType : json**||
|返回数据格式|||
```
[
    {
        "type":"app",
        "data":"{app_base_info}"
    },
    {
        "type":"app",
        "data":"{app_base_info}"
    },
    ...
]
```


<br>
# 7.软件/游戏分类

请求地址：{server_host}/cats

|Request|Method : GET||
|---|---|---|
|参数名|类型|说明|
|type|string|分类类型，应用/游戏(apps/games)|
|**Respone**|**DataType : json**||
|返回数据格式|||
```
[
    {
        "type":"cat",
        "data":{
            "id" : 1,
            "title":"音乐",
            "image_url":"/xxx/xxx/xx.png",
            "resource_count":2000
        }
    },
    {
        "type":"cat",
        "data":{
            "id" : 2,
            "title":"社交",
            "image_url":"/xxx/xxx/xx.png",
            "resource_count":2001
        }
    },
    ...
]
```

<br>
# 8.分类详情页

请求地址：{server_host}/cats/{id}

|Request|Method : GET||
|---|---|---|
|参数名|类型|说明|
|page|int|页数|
|**Respone**|**DataType : json**||
|返回数据格式|||
```
[
    {
        "type":"app",
        "data":"{app_base_info}"
    },
    {
        "type":"app",
        "data":"{app_base_info}"
    },
    ...
]
```

<br>
# 9.应用详情页

请求地址：{server_host}/apps/{id}

|Request|Method : GET||
|---|---|---|
|参数名|类型|说明|
|/|/|/|
|**Respone**|**DataType : json**||
|返回数据格式|||
```
{
    "type":"app_detail",
    "data":{
        {app_base_info},
        "screenshots":[
            "/xxxx/xxx.png",
            "/xxxx/xxx.png"
            ...
        ],
        "guess_you_favor":[
            {
                "id":"22",
                "icon_url":"",
                "name":"我叫MT"
            },
            {
                "id":"23",
                "icon_url":"",
                "name":"我叫MT2"
            }
            ...
        ],
        "same_author":[
            {
                "id":"22",
                "icon_url":"",
                "name":"我叫MT"
            },
            {
                "id":"23",
                "icon_url":"",
                "name":"我叫MT2"
            }
            ...
        ]
    }
}
```

<br>
# 10.搜索框自动匹配

请求地址：{server_host}/automatch

|Request|Method : GET||
|---|---|---|
|参数名|类型|说明|
|keyword|string|匹配关键字|
|**Respone**|**DataType : json**||
|返回数据格式（keyword为"饿"时）|||
```
[
    "饿了么",
    "饿狼传说",
    "饿的倚天",
    ...
]
```

<br>
# 11.应用搜索结果页

请求地址：{server_host}/search

|Request|Method : GET||
|---|---|---|
|参数名|类型|说明|
|q|string|搜索关键字|
|**Respone**|**DataType : json**||
|返回数据格式|||
```
[
    {
        "type":"app",
        "data":"{app_base_info}"
    },
    {
        "type":"app",
        "data":"{app_base_info}"
    },
    ...
]
```

<br>

# 12.免费榜单接口

## 接口参数  
    Method : GET
    访问例子 {server_host}/tops/free?page=1
    page为翻页可选参数

# 13.收费榜单接口

## 接口参数  
    Method : GET
    访问例子 {server_host}/tops/pay?page=1
    page为翻页可选参数

# 14.畅销榜单接口

## 接口参数  
    Method : GET
    访问例子 {server_host}/tops/hot?page=1
    page为翻页可选参数
    


    
# 15.榜单详情接口

## 接口参数  
    Method : GET
    访问例子 {server_host}/tops/{\d+}
             {server_host}/tops/981791837
             

# 16.壁纸列表接口

请求地址：{server_host}/wallpaper

|Request|Method : GET||
|---|---|---|
|参数名|类型|说明|
|page|int|页码|
|size|int|每页条数(默认20条)|
|**Respone**|**DataType : json**||
|返回数据格式(列表格式)|||
|caption|string|图片名|
|thumbURL|string|缩略图|
|originalURL|string|大图|
```
[
   {
      "caption":"暖兔",
      "thumbURL":"http:\/\/yumi2014.b0.upaiyun.com\/bz\/2016\/1\/145344563469400c99e16649e4a6533f27e248ee7b.jpg",
      "originalURL":"http:\/\/yumi2014.b0.upaiyun.com\/bz\/2016\/1\/145344564927472081d1d5491a96475e24b60862fa.jpg"
   },
   {
      "caption":"黄豆",
      "thumbURL":"http:\/\/yumi2014.b0.upaiyun.com\/bz\/2016\/1\/145344582788885a5c0c6e4eeeafc4c2756ea31d0e.jpg",
      "originalURL":"http:\/\/yumi2014.b0.upaiyun.com\/bz\/2016\/1\/145344584001858af848db467b93e041e4a7e6a8d2.jpg"
   },
   ...
]
```

# 17.表情包系列列表接口

请求地址：{server_host}/expression

|Request|Method : GET||
|---|---|---|
|参数名|类型|说明|
|page|int|页码|
|size|int|每页条数(默认18条)|
|**Respone**|**DataType : json**||
|返回数据格式(列表格式)|||
|name|string|表情名|
|imgURL|string|表情地址|
|preImgURL|string|顶图|
|eId|int|表情ID|
```
[
    {
        "name":"玉米仔",
        "imgURL":"http:\/\/7xismb.com2.z0.glb.qiniucdn.com\/android\/icon\/91\/rr\/3964c7be1fab4cfba0a115239615844e.png",
        "preImgURL":"http:\/\/7xismb.com2.z0.glb.qiniucdn.com\/android\/icon\/8h\/q7\/3964c7be1fab4cfba0a115239615844e.jpg",
        "eId":"9"
    },
    {
        "name":"张小盒",
        "imgURL":"http:\/\/7xismb.com2.z0.glb.qiniucdn.com\/android\/icon\/hv\/Z5\/2121d2a096004d5d9357002f5e82bc7f.gif",
        "preImgURL":"http:\/\/7xismb.com2.z0.glb.qiniucdn.com\/android\/icon\/if\/0p\/2121d2a096004d5d9357002f5e82bc7f.jpg",
        "eId":"8"
    },
 ]
```

# 18.单表情包列表接口

请求地址：{server_host}/expression/{id}

|Request|Method : GET||
|---|---|---|
|参数名|类型|说明|
|page|int|页码|
|size|int|每页条数(默认18条)|
|**Respone**|**DataType : json**||
|返回数据格式|||
|imgURL|string|表情图|
|shareNum|string|分享数目|
|name|string|表情名称|
|preImgURL|string|缩略图|
|list|list|子系列表情列表|
|-eName|string|表情名称|
|-imgURL|string|表情图|
|-preImgURL|string|缩略图|

# 19.表情包分享计数接口

请求地址：{server_host}/expression/{id}/share

|Request|Method : POST||
|---|---|---|
|返回数据格式|||
|message|string|返回信息|

# 20.检测设备是否领取APPST账号接口
请求地址：{server_host}/account/appst/used

|Request|Method : POST||
|---|---|---|
||---|设备号|
||||
|返回数据格式|||
|message|string|返回信息|

<br>
<br>
<br>
<br>
<br>
<br>
<br>
