---
title: SNS-SYSTEM
language_tabs:
  - shell: Shell
  - http: HTTP
  - javascript: JavaScript
  - ruby: Ruby
  - python: Python
  - php: PHP
  - java: Java
  - go: Go
toc_footers: []
includes: []
search: true
code_clipboard: true
highlight_theme: darkula
headingLevel: 2
generator: "@tarslib/widdershins v4.0.23"
---

# SNS-SYSTEM

Base URLs:

# Authentication

# v2/userUserController

<a id="opIdupdate"></a>

## PUT 用户自身更新信息

PUT /user/user

> Body 请求参数

```json
{
  "id": 0,
  "username": "string",
  "nickname": "string",
  "password": "string",
  "gender": "男",
  "email": "string",
  "phone": "string",
  "avatar": "string"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[UserDTO](#     schemauserdto)| 否 | 用户自身更新 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|更新成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdupdatePassword"></a>

## PUT 用户自身更新密码

PUT /user/user/password

> Body 请求参数

```json
{
  "id": 0,
  "oldPassword": "string",
  "newPassword": "string"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[PasswordUpdateDTO](#schemapasswo     rdupdatedto)| 否 | 用户自身更新密码 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|更新成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdlogin"></a>

## POST 用户登录

POST /user/user/login

> Body 请求参数

```json
{
  "phone": "12345678901",
  "password": "123456"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[UserLoginDTO](#sch     emauserlogindto)| 否 | 用户登录 DTO|none|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {
    "id": 0,
    "role": "string",
    "username": "string",
    "nickname": "string",
    "password": "string",
    "gender": "男",
    "email": "string",
    "phone": "string",
    "avatar": "string",
    "token": "string"
  }
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|登录成功|[ResultUserLoginVO](#schemaresultuserloginvo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# v2/userReferralController

<a id="opIdupdateReferralDraft"></a>

## PUT 用户修改内推草稿

PUT /user/referral/draft

> Body 请求参数

```json
{
  "id": 115,
  "title": "111内推标题",
  "body": "111内推内容",
  "positionUrl": "http://www.baidu.com",
  "code": "123456",
  "recruitmentType": "校招"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[ReferralDraftUpdateDTO](#schemareferrald     raftupdatedto)| 否 | 更新内推草稿 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|修改成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdcreateReferralDraft"></a>

## POST 用户创建内推草稿

POST /user/referral/draft

> Body 请求参数

```json
{
  "userId": 103,
  "title": "特别特别对",
  "body": "特别特别对是特别特别对的",
  "positionUrl": "https://www.baidu.com",
  "code": "123456",
  "recruitmentType": "校招"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[ReferralDraftDTO](#schemaref     erraldraftdto)| 否 | 新建内推草稿 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|创建成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdlistReferral"></a>

## GET 用户获取所有内推列表

GET /user/referral

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "authorName": "string",
      "tagsContent": [
        "string"
      ],
      "positionUrl": "string",
      "code": "string",
      "recruitmentType": "校招",
      "status": "草稿"
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListReferralListAllUserVO](#schemaresultlistreferrallistalluservo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdlistReferralByUserAndStatus"></a>

## GET 用户获取自己各个状态的内推列表

GET /user/referral/userId/{userId}/status/{status}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|status|path|string| 是 ||none|
|userId|path|integer(int64)| 是 ||none|

#### 枚举值

|属性|值|
|---|---|
|status|草稿|
|status|审核中|
|status|未通过|
|status|已发布|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "tagsContent": [
        "string"
      ],
      "positionUrl": "string",
      "code": "string",
      "recruitmentType": "校招"
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListReferralListMineUserVO](#schemaresultlistreferrallistmineuservo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIddeleteReferral"></a>

## DELETE 用户删除内推

DELETE /user/referral/{id}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|id|p     ath|integer(int64)| 是 ||内推 id|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# v2/userCommentController

<a id="opIdreportComment"></a>

## PUT 用户举报评论

PUT /user/comment/{id}/report

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|id|path     |integer(int64)| 是 ||被举报评论 id|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|举报成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdcreateComment"></a>

## POST 用户发表评论

POST /user/comment

> Body 请求参数

```json
{
  "userId": 0,
  "articleId": 0,
  "parentId": 0,
  "rootId": 0,
  "content": "string"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[CommentDTO](#s     chemacommentdto)| 否 | 用户评论 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|创建成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdlistCommentByArticle"></a>

## GET 用户获取文章评论列表

GET /user/comment/articleId/{articleId}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|articleId|path|integer(int64)| 是 ||none|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "posterName": "string",
      "avatar": "string",
      "content": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "subComment": [
        {
          "id": 0,
          "posterName": "string",
          "repliedPersonName": "string",
          "avatar": "string",
          "content": "string",
          "createTime": "2019-08-24T14:15:22Z"
        }
      ]
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListCommentListUserVO](#schemaresultlistcommentlistuservo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIddeleteComment"></a>

## DELETE 用户删除自己评论

DELETE /user/comment/{id}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|id|pat     h|integer(int64)| 是 ||删除评论 id|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# v2/userBidRequestController

<a id="opIdlistBidRequest"></a>

## GET 用户获取全部招标列表

GET /user/bidRequest

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "authorName": "string",
      "coreRequirement": "string",
      "pay": 0,
      "startTime": "2019-08-24",
      "endTime": "2019-08-24"
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListBidRequestListAllUserVO](#schemaresultlistbidrequestlistalluservo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdconfirmBidWinner"></a>

## PUT 发包人确定中标

PUT /user/bidRequest

> Body 请求参数

```json
{
  "bidRequestId": 0,
  "winnerBidId": 0
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[BidRequestUpdateUserDTO](#schemabidreque     stupdateuserdto)| 否 | 更新招标 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|确认成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdcreateBidRequest"></a>

## POST 发包人创建招标

POST /user/bidRequest

> Body 请求参数

```json
{
  "creatorId": 0,
  "title": "string",
  "body": "string",
  "coreRequirement": "string",
  "pay": 0,
  "startTime": "2019-08-24",
  "endTime": "2019-08-24"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[BidRequestUserDTO](#schemabi     drequestuserdto)| 否 | 新建招标 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|创建成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdconfirmFinished"></a>

## PUT 发包人确定招标完成

PUT /user/bidRequest/{id}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|id|path|integer(int64)| 是 ||none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|确认成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdlistBidRequestByBidder"></a>

## GET 竞标人获取自己发出申请被招标人同意的进行中招标列表

GET /user/bidRequest/bidder/{id}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|id|pa     th|integer(int64)| 是 ||竞标人 id|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "progress": "string",
      "coreRequirement": "string",
      "pay": 0,
      "startTime": "2019-08-24",
      "endTime": "2019-08-24",
      "biddeeName": "string",
      "phone": "string"
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListBidRequestListWinnerUserVO](#schemaresultlistbidrequestlistwinneruservo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdlistBidRequestByBiddee"></a>

## GET 发包人获取自己招标列表

GET /user/bidRequest/biddee/{id}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|id|pa     th|integer(int64)| 是 ||发包人 id|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "status": "草稿",
      "progress": "string",
      "coreRequirement": "string",
      "pay": 0,
      "startTime": "2019-08-24",
      "endTime": "2019-08-24"
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListBidRequestListMineUserVO](#schemaresultlistbidrequestlistmineuservo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# v2/userArticleController

<a id="opIdupdateBlogDraft"></a>

## PUT 用户修改博文草稿

PUT /user/article/draft

> Body 请求参数

```json
{
  "id": 110,
  "title": "特别特别dui",
  "body": "特别特别dui是特别特别dui的"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[BlogDraftUpdateDTO](#schemablogd     raftupdatedto)| 否 | 更新博文草稿 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|修改成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdcreateBlogDraft"></a>

## POST 用户创建博文草稿

POST /user/article/draft

> Body 请求参数

```json
{
  "userId": 103,
  "title": "特别特别对",
  "body": "特别特别对是特别特别对的"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[BlogDraftDTO](#schem     ablogdraftdto)| 否 | 新建博文草稿 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|创建成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdlistBlog"></a>

## GET 用户获取所有博文列表

GET /user/article

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "authorName": "string",
      "tagsContent": [
        "string"
      ],
      "status": "草稿"
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListBlogListAllUserVO](#schemaresultlistbloglistalluservo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdlistBlogByUserAndStatus"></a>

## GET 用户获取自己各个状态的博文列表

GET /user/article/userId/{userId}/status/{status}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|status|path|string| 是 ||博文状态|
|use     rId|path|integer(int64)| 是 ||用户 id|

#### 枚举值

|属性|值|
|---|---|
|status|草稿|
|status|审核中|
|status|未通过|
|status|已发布|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "tagsContent": [
        "string"
      ]
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListBlogListMineUserVO](#schemaresultlistbloglistmineuservo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIddeleteArticle"></a>

## DELETE 用户删除博文

DELETE /user/article/{id}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|id|p     ath|integer(int64)| 是 ||文章 id|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# v2/userActivityController

<a id="opIdupdateActivity"></a>

## PUT 用户更新发起的活动

PUT /user/activity/{id}

> Body 请求参数

```json
{
  "userId": 0,
  "title": "string",
  "body": "string",
  "startTime": "2019-08-24T14:15:22Z",
  "endTime": "2019-08-24T14:15:22Z",
  "registrationDeadline": "2019-08-24T14:15:22Z",
  "place": "string",
  "maxPerson": 0
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|id|p     ath|integer(int64)| 是 ||活动 id|
|body|body|[ActivityUserDTO]     (#schemaactivityuserdto)| 否 | 用户发起活动 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|更新成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIddeleteActivity"></a>

## DELETE 用户删除发起的活动

DELETE /user/activity/{id}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|id|p     ath|integer(int64)| 是 ||活动 id|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdlistAvailableActivity"></a>

## GET 用户获取可以报名的活动列表

GET /user/activity

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "authorName": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "startTime": "2019-08-24T14:15:22Z",
      "endTime": "2019-08-24T14:15:22Z",
      "registrationDeadline": "2019-08-24T14:15:22Z",
      "place": "string",
      "maxPerson": 0
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListActivityListAllUserVO](#schemaresultlistactivitylistalluservo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdcreateActivity"></a>

## POST 用户发起新的活动

POST /user/activity

> Body 请求参数

```json
{
  "userId": 0,
  "title": "string",
  "body": "string",
  "startTime": "2019-08-24T14:15:22Z",
  "endTime": "2019-08-24T14:15:22Z",
  "registrationDeadline": "2019-08-24T14:15:22Z",
  "place": "string",
  "maxPerson": 0
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[ActivityUserDTO](#schemaac     tivityuserdto)| 否 | 用户发起活动 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|创建成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdlistInitiatedActivity"></a>

## GET 用户获取自己发起的活动列表

GET /user/activity/userId/{userId}/status/{status}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|userId|path|integer(int64)| 是 ||none|
|status|path|string| 是 ||none|

#### 枚举值

|属性|值|
|---|---|
|status|草稿|
|status|审核中|
|status|未通过|
|status|已发布|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "startTime": "2019-08-24T14:15:22Z",
      "endTime": "2019-08-24T14:15:22Z",
      "registrationDeadline": "2019-08-24T14:15:22Z",
      "place": "string",
      "maxPerson": 0
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListActivityListMineUserVO](#schemaresultlistactivitylistmineuservo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# v2/adminUserController

<a id="opIdlistUser"></a>

## GET 管理员获取用户列表

GET /admin/user

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "username": "string",
      "nickname": "string",
      "gender": "男",
      "email": "string",
      "phone": "string",
      "avatar": "string"
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListUserListAdminVO](#schemaresultlistuserlistadminvo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdupdateByAdmin"></a>

## PUT 管理员更新用户信息

PUT /admin/user

> Body 请求参数

```json
{
  "adminId": 0,
  "id": 0,
  "username": "string",
  "nickname": "string",
  "password": "string",
  "gender": "男",
  "email": "string",
  "phone": "string"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[UserUpdateByAdminDTO](#schemauserupdat     ebyadmindto)| 否 | 管理员为用户更新 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|更新成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdregister"></a>

## POST 管理员为用户注册

POST /admin/user/register

> Body 请求参数

```json
{
  "adminId": 1,
  "username": "user1",
  "nickname": "111",
  "password": "123456",
  "gender": "0",
  "email": "1234@123",
  "phone": "12345678901",
  "avatar": "string"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[UserRegisterDTO](#schemauser     registerdto)| 否 | 管理员为用户注册 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|注册成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIddelete"></a>

## DELETE 管理员删除用户

DELETE /admin/user/{id}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|id|p     ath|integer(int64)| 是 ||用户 ID|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# v2/adminArticleController

<a id="opIdlistBlog_1"></a>

## GET 管理员获取博客列表

GET /admin/article

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "status": "草稿",
      "authorName": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "updateTime": "2019-08-24T14:15:22Z",
      "tagsContent": [
        "string"
      ]
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListArticleVO](#schemaresultlistarticlevo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdreviewArticle"></a>

## PUT 管理员审核文章

PUT /admin/article

> Body 请求参数

```json
{
  "id": 0,
  "isPassed": true
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[ArticleReviewDTO](#schemaarti     clereviewdto)| 否 | 管理员文章审核 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|审核成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# v2/userBidController

<a id="opIdcreateBid"></a>

## POST 用户进行投标

POST /user/bid

> Body 请求参数

```json
{
  "userId": 0,
  "bidRequestId": 0,
  "resume": "string",
  "quotation": 0
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[BidUserDTO](#s     chemabiduserdto)| 否 | 新建投标 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|创建成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdlistBidderById"></a>

## GET 发包人获取投标人信息

GET /user/bid/{id}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|id|p     ath|integer(int64)| 是 ||招标 id|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "bidderName": "string",
      "phone": "string",
      "resume": "string",
      "quotation": "string"
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListBidListUserVO](#schemaresultlistbidlistuservo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# v2/userArticleReleaseController

<a id="opIdreleaseReferral"></a>

## POST 用户直接发布内推

POST /user/articleRelease/referral

> Body 请求参数

```json
{
  "userId": 103,
  "title": "内推标题",
  "body": "内推内容",
  "tagsContent": [
    "内推标签1",
    "内推标签2"
  ],
  "positionUrl": "https://www.baidu.com",
  "code": "123456",
  "recruitmentType": "校招"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[ReferralUserDTO](#schema     referraluserdto)| 否 | 新建内推 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|发布成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdreleaseDraftToReferral"></a>

## POST 用户把自己的内推草稿发布

POST /user/articleRelease/referral/draft

> Body 请求参数

```json
{
  "id": 115,
  "title": "特别特别dui",
  "body": "特别特别dui是特别特别对dui",
  "tagsContent": [
    "特别特别dui",
    "特别特别对dui"
  ],
  "positionUrl": "https://www.baidu.com",
  "code": "123456",
  "recruitmentType": "校招"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[ReferralDraftReleaseDTO](#schemareferraldr     aftreleasedto)| 否 | 更新内推草稿 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|发布成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdreleaseBlog"></a>

## POST 用户直接发布博文

POST /user/articleRelease/blog

> Body 请求参数

```json
{
  "userId": 103,
  "title": "哈基米",
  "body": "哈基米是哈基米里第一个哈基米的",
  "tagsContent": [
    "哈基米",
    "哈基米里",
    "哈基米的"
  ]
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[BlogUserDTO](#sc     hemabloguserdto)| 否 | 新建博文 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|发布成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdreleaseDraftToBlog"></a>

## POST 用户把自己的博文草稿发布

POST /user/articleRelease/blog/draft

> Body 请求参数

```json
{
  "id": 110,
  "title": "特别特别对",
  "body": "特别特别对是特别特别对的",
  "tagsContent": [
    "特别特别对",
    "特别特别对的"
  ]
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[BlogDraftReleaseDTO](#schemablogdr     aftreleasedto)| 否 | 更新博文草稿 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|发布成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# v2/userActivityRegistrationController

<a id="opIdregisterActivity"></a>

## POST 用户报名活动

POST /user/activityRegistration

> Body 请求参数

```json
{
  "activityId": 0,
  "userId": 0,
  "remark": "string"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|[ActivityRegistrationUserDTO](#schemaactivityregist     rationuserdto)| 否 | 用户注册活动 DTO|none|

> 返回示例

> 201 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|报名成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdlistActivityRegistration"></a>

## GET 用户获取已报名的活动列表

GET /user/activityRegistration/userId/{userId}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|userId|path|integer(int64)| 是 ||none|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "authorName": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "startTime": "2019-08-24T14:15:22Z",
      "endTime": "2019-08-24T14:15:22Z",
      "registrationDeadline": "2019-08-24T14:15:22Z",
      "place": "string",
      "maxPerson": 0
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListActivityListAllUserVO](#schemaresultlistactivitylistalluservo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdunregisterActivity"></a>

## DELETE 用户取消报名活动

DELETE /user/activityRegistration/{id}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|id|pat     h|integer(int64)| 是 ||活动注册 id|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|取消报名成功|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# v2/adminTagController

<a id="opIdlistTag"></a>

## GET 管理员获取所有标签列表

GET /admin/tag

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "content": "string",
      "creatorName": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "useCount": 0
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListTagAdminVO](#schemaresultlisttagadminvo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIdlistTagLikeContent"></a>

## GET 管理员根据标签内容模糊查询标签列表

GET /admin/tag/fuzzyContent

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|content|query|string| 是 ||标签内容|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "content": "string",
      "creatorName": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "useCount": 0
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListTagAdminVO](#schemaresultlisttagadminvo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# v2/adminReferralController

<a id="opIdlistReferralByAdmin"></a>

## GET 管理员获取内推列表

GET /admin/referral

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "status": "草稿",
      "authorName": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "updateTime": "2019-08-24T14:15:22Z",
      "tags": [
        "string"
      ],
      "positionUrl": "string",
      "code": "string",
      "recruitmentType": "校招"
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListReferralVO](#schemaresultlistreferralvo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# v2/adminCommentController

<a id="opIdlistCommentByAdmin"></a>

## GET 管理员获取所有被举报的评论列表

GET /admin/comment

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "posterName": "string",
      "avatar": "string",
      "content": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "subComment": [
        {
          "id": 0,
          "posterName": "string",
          "repliedPersonName": "string",
          "avatar": "string",
          "content": "string",
          "createTime": "2019-08-24T14:15:22Z"
        }
      ]
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListCommentListUserVO](#schemaresultlistcommentlistuservo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

<a id="opIddeleteComment_1"></a>

## DELETE 管理员删除评论

DELETE /admin/comment/{id}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|id|pat     h|integer(int64)| 是 ||删除评论 id|

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultObject](#schemaresultobject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# v2/adminBidRequestController

<a id="opIdlistBidRequest_1"></a>

## GET 管理员获取招标列表

GET /admin/bidRequest

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "status": "草稿",
      "authorName": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "updateTime": "2019-08-24T14:15:22Z",
      "coreRequirement": "string",
      "pay": 0,
      "startTime": "2019-08-24",
      "endTime": "2019-08-24",
      "bidRequestStatus": "待中标"
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListBidRequestVO](#schemaresultlistbidrequestvo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# v2/adminActivityController

<a id="opIdlistActivity"></a>

## GET 管理员获取活动列表

GET /admin/activity

> 返回示例

> 200 Response

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "status": "草稿",
      "authorName": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "updateTime": "2019-08-24T14:15:22Z",
      "startTime": "2019-08-24T14:15:22Z",
      "endTime": "2019-08-24T14:15:22Z",
      "registrationDeadline": "2019-08-24T14:15:22Z",
      "place": "string",
      "maxPerson": 0
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|[ResultListActivityVO](#schemaresultlistactivityvo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[ResultObject](#schemaresultobject)|

# 数据模型

<h2 id="tocS_BidRequestListMineUserVO">BidRequestListMineUserVO</h2>

<a id="schemabidrequestlistmineuservo"></a>

<a id="schema_BidRequestListMineUserVO"></a>

<a id="tocSbidrequestlistmineuservo"></a>

<a id="tocsbidrequestlistmineuservo"></a>

```json
{
  "id": 0,
  "title": "string",
  "body": "string",
  "status": "草稿",
  "progress": "string",
  "coreRequirement": "string",
  "pay": 0,
  "startTime": "2019-08-24",
  "endTime": "2019-08-24"
}

```

详 情 VO

## 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|招标 id|none|
|title|string|false|none|招标标题|none|
|body|string|false|none|招标内容|none|
|status|string|false|none|招标状态|none|
|progress|string|false|none|招标进度|none|
|coreRequirement|string|false|none|招标核心需求|none|
|pay|number(double)|false|none|招标报酬|none|
|startTime|string(date)|false|none|招标开始时间|none|

dTime|string(date)|false|none|招标结束时间|none|

## 枚举值

|属性|值|
|---|---|
|status|草稿|
|status|审核中|
|status|未通过|
|status|已发布|

<h2 id="tocS_ActivityListMineUserVO">ActivityListMineUserVO</h2>

<a id="schemaactivitylistmineuservo"></a>

<a id="schema_ActivityListMineUserVO"></a>

<a id="tocSactivitylistmineuservo"></a>

<a id="tocsactivitylistmineuservo"></a>

```json
{
  "id": 0,
  "title": "string",
  "body": "string",
  "createTime": "2019-08-24T14:15:22Z",
  "startTime": "2019-08-24T14:15:22Z",
  "endTime": "2019-08-24T14:15:22Z",
  "registrationDeadline": "2019-08-24T14:15:22Z",
  "place": "string",
  "maxPerson": 0
}

```

用户自己发起的活动列表

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|活动 id|none|
|title|string|false|none|活动标题|none|
|body|string|false|none|活动内容|none|
|createTime|string(date-time)|false|none|活动发布时间|none|
|startTime|string(date-time)|false|none|活动开始时间|none|
|endTime|string(date-time)|false|none|活动结束时间|none|
|registrationDeadline|string(date-time)|false|none|活动报名截止时间|none|
|place|string|false|none|活动地点|none|
|maxPerson|integer(int32)|false|none|报名人数上限|none|

<h2 id="tocS_BidRequestListWinnerUserVO">BidRequestListWinnerUserVO</h2>

<a id="schemabidrequestlistwinneruservo"></a>

<a id="schema_BidRequestListWinnerUserVO"></a>

<a id="tocSbidrequestlistwinneruservo"></a>

<a id="tocsbidrequestlistwinneruservo"></a>

```json
{
  "id": 0,
  "title": "string",
  "body": "string",
  "progress": "string",
  "coreRequirement": "string",
  "pay": 0,
  "startTime": "2019-08-24",
  "endTime": "2019-08-24",
  "biddeeName": "string",
  "phone": "string"
}

```

用户全部中标的招标列表 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|招标 id|none|
|title|string|false|none|招标标题|none|
|body|string|false|none|招标内容|none|
|progress|string|false|none|招标进度|none|
|coreRequirement|string|false|none|招标核心需求|none|
|pay|number(double)|false|none|招标报酬|none|
|startTime|string(date)|false|none|招标开始时间|none|
|endTime|string(date)|false|none|招标结束时间|none|
|biddeeName|string|false|none|招标者姓名|none|
|phone|string|false|none|招标者电话|none|

<h2 id="tocS_BlogListMineUserVO">BlogListMineUserVO</h2>

<a id="schemabloglistmineuservo"></a>

<a id="schema_BlogListMineUserVO"></a>

<a id="tocSbloglistmineuservo"></a>

<a id="tocsbloglistmineuservo"></a>

```json
{
  "id": 0,
  "title": "string",
  "body": "string",
  "tagsContent": [
    "string"
  ]
}

```

用户自身博文列表 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|博文 id|none|
|title|string|false|none|博文标题|none|
|body|string|false|none|博文内容|none|
|tagsContent|[string]|false|none|博文标签内容列表|none|
|" 博文标签内容列表|string|false|none|博文标签内容列表|none|

<h2 id="tocS_ReferralListMineUserVO">ReferralListMineUserVO</h2>

<a id="schemareferrallistmineuservo"></a>

<a id="schema_ReferralListMineUserVO"></a>

<a id="tocSreferrallistmineuservo"></a>

<a id="tocsreferrallistmineuservo"></a>

```json
{
  "id": 0,
  "title": "string",
  "body": "string",
  "tagsContent": [
    "string"
  ],
  "positionUrl": "string",
  "code": "string",
  "recruitmentType": "校招"
}

```

用户自身内推列表 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|内推 id|none|
|title|string|false|none|内推标题|none|
|body|string|false|none|内推内容|none|
|tagsContent|[string]|false|none|内推标签内容列表|none|
|" 内推标签内容列表|string|false|none|内推标签内容列表|none|
|positionUrl|string|false|none|内推职位 url|none|
|code|string|false|none|内推码|none|
|recruitmentType|string|false|none|招聘类型|none|

## 枚举值

|属性|值|
|---|---|
|recruitmentType|校招|
|recruitmentType|实习|

<h2 id="tocS_ReferralListAllUserVO">ReferralListAllUserVO</h2>

<a id="schemareferrallistalluservo"></a>

<a id="schema_ReferralListAllUserVO"></a>

<a id="tocSreferrallistalluservo"></a>

<a id="tocsreferrallistalluservo"></a>

```json
{
  "id": 0,
  "title": "string",
  "body": "string",
  "authorName": "string",
  "tagsContent": [
    "string"
  ],
  "positionUrl": "string",
  "code": "string",
  "recruitmentType": "校招",
  "status": "草稿"
}

```

用户可以查看的所有内推列表 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|内推 id|none|
|title|string|false|none|内推标题|none|
|body|string|false|none|内推内容|none|
|authorName|string|false|none|内推作者|none|
|tagsContent|[string]|false|none|内推标签内容列表|none|
|" 内推标签内容列表|string|false|none|内推标签内容列表|none|
|positionUrl|string|false|none|内推职位 url|none|
|code|string|false|none|内推码|none|
|recruitmentType|string|false|none|招聘类型|none|
|status|string|false|none|文章状态|none|

## 枚举值

|属性|值|
|---|---|
|recruitmentType|校招|
|recruitmentType|实习|
|status|草稿|
|status|审核中|
|status|未通过|
|status|已发布|

<h2 id="tocS_UserLoginVO">UserLoginVO</h2>

<a id="schemauserloginvo"></a>

<a id="schema_UserLoginVO"></a>

<a id="tocSuserloginvo"></a>

<a id="tocsuserloginvo"></a>

```json
{
  "id": 0,
  "role": "string",
  "username": "string",
  "nickname": "string",
  "password": "string",
  "gender": "男",
  "email": "string",
  "phone": "string",
  "avatar": "string",
  "token": "string"
}

```

用户登录 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|用户 id|none|
|role|string|false|none|角色名称|none|
|username|string|false|none|用户名|none|
|nickname|string|false|none|昵称|none|
|password|string|false|none|密码|none|
|gender|string|false|none|性别 (0- 男 1- 女 2- 其他)|none|
|email|string|false|none|邮箱|none|
|phone|string|false|none|手机号|none|
|avatar|string|false|none|头像|none|
|token|string|false|none|token|none|

## 枚举值

|属性|值|
|---|---|
|gender|男|
|gender|女|
|gender|其他|

<h2 id="tocS_BlogListAllUserVO">BlogListAllUserVO</h2>

<a id="schemabloglistalluservo"></a>

<a id="schema_BlogListAllUserVO"></a>

<a id="tocSbloglistalluservo"></a>

<a id="tocsbloglistalluservo"></a>

```json
{
  "id": 0,
  "title": "string",
  "body": "string",
  "authorName": "string",
  "tagsContent": [
    "string"
  ],
  "status": "草稿"
}

```

用户可以查看的所有博文列表 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|博文 id|none|
|title|string|false|none|博文标题|none|
|body|string|false|none|博文内容|none|
|authorName|string|false|none|博文作者|none|
|tagsContent|[string]|false|none|博文标签内容列表|none|
|" 博文标签内容列表|string|false|none|博文标签内容列表|none|
|status|string|false|none|博文状态|none|

## 枚举值

|属性|值|
|---|---|
|status|草稿|
|status|审核中|
|status|未通过|
|status|已发布|

<h2 id="tocS_ActivityListAllUserVO">ActivityListAllUserVO</h2>

<a id="schemaactivitylistalluservo"></a>

<a id="schema_ActivityListAllUserVO"></a>

<a id="tocSactivitylistalluservo"></a>

<a id="tocsactivitylistalluservo"></a>

```json
{
  "id": 0,
  "title": "string",
  "body": "string",
  "authorName": "string",
  "createTime": "2019-08-24T14:15:22Z",
  "startTime": "2019-08-24T14:15:22Z",
  "endTime": "2019-08-24T14:15:22Z",
  "registrationDeadline": "2019-08-24T14:15:22Z",
  "place": "string",
  "maxPerson": 0
}

```

用户活动列表

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|活动 id|none|
|title|string|false|none|活动标题|none|
|body|string|false|none|活动内容|none|
|authorName|string|false|none|活动作者姓名|none|
|createTime|string(date-time)|false|none|活动发布时间|none|
|startTime|string(date-time)|false|none|活动开始时间|none|
|endTime|string(date-time)|false|none|活动结束时间|none|
|registrationDeadline|string(date-time)|false|none|活动报名截止时间|none|
|place|string|false|none|活动地点|none|
|maxPerson|integer(int32)|false|none|报名人数上限|none|

<h2 id="tocS_BidListUserVO">BidListUserVO</h2>

<a id="schemabidlistuservo"></a>

<a id="schema_BidListUserVO"></a>

<a id="tocSbidlistuservo"></a>

<a id="tocsbidlistuservo"></a>

```json
{
  "id": 0,
  "bidderName": "string",
  "phone": "string",
  "resume": "string",
  "quotation": "string"
}

```

投标人列表 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|投标人 id|none|
|bidderName|string|false|none|投标人姓名|none|
|phone|string|false|none|投标人手机号|none|
|resume|string|false|none|投标人简历|none|
|quotation|string|false|none|投标人报价|none|

<h2 id="tocS_ActivityVO">ActivityVO</h2>

<a id="schemaactivityvo"></a>

<a id="schema_ActivityVO"></a>

<a id="tocSactivityvo"></a>

<a id="tocsactivityvo"></a>

```json
{
  "id": 0,
  "title": "string",
  "body": "string",
  "status": "草稿",
  "authorName": "string",
  "createTime": "2019-08-24T14:15:22Z",
  "updateTime": "2019-08-24T14:15:22Z",
  "startTime": "2019-08-24T14:15:22Z",
  "endTime": "2019-08-24T14:15:22Z",
  "registrationDeadline": "2019-08-24T14:15:22Z",
  "place": "string",
  "maxPerson": 0
}

```

管理员活动 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|活动 id|none|
|title|string|false|none|活动标题|none|
|body|string|false|none|活动内容|none|
|status|string|false|none|文章状态|none|
|authorName|string|false|none|活动作者姓名|none|
|createTime|string(date-time)|false|none|活动发布时间|none|
|updateTime|string(date-time)|false|none|活动更新时间|none|
|startTime|string(date-time)|false|none|活动开始时间|none|
|endTime|string(date-time)|false|none|活动结束时间|none|
|registrationDeadline|string(date-time)|false|none|活动报名截止时间|none|
|place|string|false|none|活动地点|none|
|maxPerson|integer(int32)|false|none|报名人数上限|none|

## 枚举值

|属性|值|
|---|---|
|status|草稿|
|status|审核中|
|status|未通过|
|status|已发布|

<h2 id="tocS_BidRequestVO">BidRequestVO</h2>

<a id="schemabidrequestvo"></a>

<a id="schema_BidRequestVO"></a>

<a id="tocSbidrequestvo"></a>

<a id="tocsbidrequestvo"></a>

```json
{
  "id": 0,
  "title": "string",
  "body": "string",
  "status": "草稿",
  "authorName": "string",
  "createTime": "2019-08-24T14:15:22Z",
  "updateTime": "2019-08-24T14:15:22Z",
  "coreRequirement": "string",
  "pay": 0,
  "startTime": "2019-08-24",
  "endTime": "2019-08-24",
  "bidRequestStatus": "待中标"
}

```

管理员招标 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|招标 id|none|
|title|string|false|none|招标标题|none|
|body|string|false|none|招标内容|none|
|status|string|false|none|文章状态|none|
|authorName|string|false|none|招标作者姓名|none|
|createTime|string(date-time)|false|none|招标发布时间|none|
|updateTime|string(date-time)|false|none|招标更新时间|none|
|coreRequirement|string|false|none|招标核心需求|none|
|pay|number(double)|false|none|招标报酬|none|
|startTime|string(date)|false|none|招标开始时间|none|
|endTime|string(date)|false|none|招标结束时间|none|
|bidRequestStatus|string|false|none|招标状态|none|

## 枚举值

|属性|值|
|---|---|
|status|草稿|
|status|审核中|
|status|未通过|
|status|已发布|
|bidRequestStatus|待中标|
|bidRequestStatus|进行中|
|bidRequestStatus|已结束|

<h2 id="tocS_SubCommentVO">SubCommentVO</h2>

<a id="schemasubcommentvo"></a>

<a id="schema_SubCommentVO"></a>

<a id="tocSsubcommentvo"></a>

<a id="tocssubcommentvo"></a>

```json
{
  "id": 0,
  "posterName": "string",
  "repliedPersonName": "string",
  "avatar": "string",
  "content": "string",
  "createTime": "2019-08-24T14:15:22Z"
}

```

子评论 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|子评论 ID|none|
|posterName|string|false|none|发评论的用户姓名|none|
|repliedPersonName|string|false|none|被回复的用户姓名|none|
|avatar|string|false|none|用户头像|none|
|content|string|false|none|评论内容|none|
|createTime|string(date-time)|false|none|评论时间|none|

<h2 id="tocS_CommentListUserVO">CommentListUserVO</h2>

<a id="schemacommentlistuservo"></a>

<a id="schema_CommentListUserVO"></a>

<a id="tocScommentlistuservo"></a>

<a id="tocscommentlistuservo"></a>

```json
{
  "id": 0,
  "posterName": "string",
  "avatar": "string",
  "content": "string",
  "createTime": "2019-08-24T14:15:22Z",
  "subComment": [
    {
      "id": 0,
      "posterName": "string",
      "repliedPersonName": "string",
      "avatar": "string",
      "content": "string",
      "createTime": "2019-08-24T14:15:22Z"
    }
  ]
}

```

用户查看评论列表 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|评论 ID|none|
|posterName|string|false|none|发评论的用户姓名|none|
|avatar|string|false|none|用户头像|none|
|content|string|false|none|评论内容|none|
|createTime|string(date-time)|false|none|评论时间|none|
|subComment|[[SubCommentVO](#schemasubcommentvo)]|false|none|子评论|none|

<h2 id="tocS_ReferralVO">ReferralVO</h2>

<a id="schemareferralvo"></a>

<a id="schema_ReferralVO"></a>

<a id="tocSreferralvo"></a>

<a id="tocsreferralvo"></a>

```json
{
  "id": 0,
  "title": "string",
  "body": "string",
  "status": "草稿",
  "authorName": "string",
  "createTime": "2019-08-24T14:15:22Z",
  "updateTime": "2019-08-24T14:15:22Z",
  "tags": [
    "string"
  ],
  "positionUrl": "string",
  "code": "string",
  "recruitmentType": "校招"
}

```

管理员内推 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|内推 id|none|
|title|string|false|none|内推标题|none|
|body|string|false|none|内推内容|none|
|status|string|false|none|文章状态|none|
|authorName|string|false|none|内推作者姓名|none|
|createTime|string(date-time)|false|none|内推发布时间|none|
|updateTime|string(date-time)|false|none|内推更新时间|none|
|tags|[string]|false|none|内推标签列表|none|
|" 内推标签列表|string|false|none|内推标签列表|none|
|positionUrl|string|false|none|职位链接|none|
|code|string|false|none|内推码|none|
|recruitmentType|string|false|none|招聘类型|none|

## 枚举值

|属性|值|
|---|---|
|status|草稿|
|status|审核中|
|status|未通过|
|status|已发布|
|recruitmentType|校招|
|recruitmentType|实习|

<h2 id="tocS_TagAdminVO">TagAdminVO</h2>

<a id="schematagadminvo"></a>

<a id="schema_TagAdminVO"></a>

<a id="tocStagadminvo"></a>

<a id="tocstagadminvo"></a>

```json
{
  "id": 0,
  "content": "string",
  "creatorName": "string",
  "createTime": "2019-08-24T14:15:22Z",
  "useCount": 0
}

```

管理员标签 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|标签 id|none|
|content|string|false|none|标签名|none|
|creatorName|string|false|none|创建者 id|none|
|createTime|string(date-time)|false|none|创建时间|none|
|useCount|integer(int64)|false|none|使用次数|none|

<h2 id="tocS_ArticleVO">ArticleVO</h2>

<a id="schemaarticlevo"></a>

<a id="schema_ArticleVO"></a>

<a id="tocSarticlevo"></a>

<a id="tocsarticlevo"></a>

```json
{
  "id": 0,
  "title": "string",
  "body": "string",
  "status": "草稿",
  "authorName": "string",
  "createTime": "2019-08-24T14:15:22Z",
  "updateTime": "2019-08-24T14:15:22Z",
  "tagsContent": [
    "string"
  ]
}

```

管理员文章 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|文章 id|none|
|title|string|false|none|文章标题|none|
|body|string|false|none|文章内容|none|
|status|string|false|none|文章状态|none|
|authorName|string|false|none|文章作者姓名|none|
|createTime|string(date-time)|false|none|文章发布时间|none|
|updateTime|string(date-time)|false|none|文章更新时间|none|
|tagsContent|[string]|false|none|文章标签列表|none|
|" 文章标签列表|string|false|none|文章标签列表|none|

## 枚举值

|属性|值|
|---|---|
|status|草稿|
|status|审核中|
|status|未通过|
|status|已发布|

<h2 id="tocS_UserListAdminVO">UserListAdminVO</h2>

<a id="schemauserlistadminvo"></a>

<a id="schema_UserListAdminVO"></a>

<a id="tocSuserlistadminvo"></a>

<a id="tocsuserlistadminvo"></a>

```json
{
  "id": 0,
  "username": "string",
  "nickname": "string",
  "gender": "男",
  "email": "string",
  "phone": "string",
  "avatar": "string"
}

```

管理员获取用户列表 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|用户 id|none|
|username|string|false|none|用户名|none|
|nickname|string|false|none|昵称|none|
|gender|string|false|none|性别 (0- 男 1- 女 2- 其他)|none|
|email|string|false|none|邮箱|none|
|phone|string|false|none|手机号|none|
|avatar|string|false|none|头像|none|

## 枚举值

|属性|值|
|---|---|
|gender|男|
|gender|女|
|gender|其他|

<h2 id="tocS_BidRequestListAllUserVO">BidRequestListAllUserVO</h2>

<a id="schemabidrequestlistalluservo"></a>

<a id="schema_BidRequestListAllUserVO"></a>

<a id="tocSbidrequestlistalluservo"></a>

<a id="tocsbidrequestlistalluservo"></a>

```json
{
  "id": 0,
  "title": "string",
  "body": "string",
  "authorName": "string",
  "coreRequirement": "string",
  "pay": 0,
  "startTime": "2019-08-24",
  "endTime": "2019-08-24"
}

```

用户全部招标列表 VO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|招标 id|none|
|title|string|false|none|招标标题|none|
|body|string|false|none|招标内容|none|
|authorName|string|false|none|招标作者姓名|none|
|coreRequirement|string|false|none|招标核心需求|none|
|pay|number(double)|false|none|招标报酬|none|
|startTime|string(date)|false|none|招标开始时间|none|
|endTime|string(date)|false|none|招标结束时间|none|

<h2 id="tocS_ResultListBidRequestListMineUserVO">ResultListBidRequestListMineUserVO</h2>

<a id="schemaresultlistbidrequestlistmineuservo"></a>

<a id="schema_ResultListBidRequestListMineUserVO"></a>

<a id="tocSresultlistbidrequestlistmineuservo"></a>

<a id="tocsresultlistbidrequestlistmineuservo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "status": "草稿",
      "progress": "string",
      "coreRequirement": "string",
      "pay": 0,
      "startTime": "2019-08-24",
      "endTime": "2019-08-24"
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[BidRequestListMineUserVO](#schemabidrequestlistmineuservo)]|false|none||none|

<h2 id="tocS_ResultObject">ResultObject</h2>

<a id="schemaresultobject"></a>

<a id="schema_ResultObject"></a>

<a id="tocSresultobject"></a>

<a id="tocsresultobject"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": {}
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|object|false|none||none|

<h2 id="tocS_ResultListActivityListMineUserVO">ResultListActivityListMineUserVO</h2>

<a id="schemaresultlistactivitylistmineuservo"></a>

<a id="schema_ResultListActivityListMineUserVO"></a>

<a id="tocSresultlistactivitylistmineuservo"></a>

<a id="tocsresultlistactivitylistmineuservo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "startTime": "2019-08-24T14:15:22Z",
      "endTime": "2019-08-24T14:15:22Z",
      "registrationDeadline": "2019-08-24T14:15:22Z",
      "place": "string",
      "maxPerson": 0
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[ActivityListMineUserVO](#schemaactivitylistmineuservo)]|false|none||none|

<h2 id="tocS_ResultListBidRequestListWinnerUserVO">ResultListBidRequestListWinnerUserVO</h2>

<a id="schemaresultlistbidrequestlistwinneruservo"></a>

<a id="schema_ResultListBidRequestListWinnerUserVO"></a>

<a id="tocSresultlistbidrequestlistwinneruservo"></a>

<a id="tocsresultlistbidrequestlistwinneruservo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "progress": "string",
      "coreRequirement": "string",
      "pay": 0,
      "startTime": "2019-08-24",
      "endTime": "2019-08-24",
      "biddeeName": "string",
      "phone": "string"
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[BidRequestListWinnerUserVO](#schemabidrequestlistwinneruservo)]|false|none||none|

<h2 id="tocS_ResultListBidRequestListAllUserVO">ResultListBidRequestListAllUserVO</h2>

<a id="schemaresultlistbidrequestlistalluservo"></a>

<a id="schema_ResultListBidRequestListAllUserVO"></a>

<a id="tocSresultlistbidrequestlistalluservo"></a>

<a id="tocsresultlistbidrequestlistalluservo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "authorName": "string",
      "coreRequirement": "string",
      "pay": 0,
      "startTime": "2019-08-24",
      "endTime": "2019-08-24"
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[BidRequestListAllUserVO](#schemabidrequestlistalluservo)]|false|none||none|

<h2 id="tocS_BlogDraftReleaseDTO">BlogDraftReleaseDTO</h2>

<a id="schemablogdraftreleasedto"></a>

<a id="schema_BlogDraftReleaseDTO"></a>

<a id="tocSblogdraftreleasedto"></a>

<a id="tocsblogdraftreleasedto"></a>

```json
{
  "id": 110,
  "title": "特别特别对",
  "body": "特别特别对是特别特别对的",
  "tagsContent": [
    "特别特别对",
    "特别特别对的"
  ]
}

```

更新博文草稿 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|true|none|博文草稿 id|none|
|title|string|true|none|博文标题|none|
|body|string|true|none|博文内容|none|
|tagsContent|[string]|true|none|博文标签内容列表|none|
|" 博文标签内容列表|string|false|none|博文标签内容列表|none|

<h2 id="tocS_ResultListBlogListMineUserVO">ResultListBlogListMineUserVO</h2>

<a id="schemaresultlistbloglistmineuservo"></a>

<a id="schema_ResultListBlogListMineUserVO"></a>

<a id="tocSresultlistbloglistmineuservo"></a>

<a id="tocsresultlistbloglistmineuservo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "tagsContent": [
        "string"
      ]
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[BlogListMineUserVO](#schemabloglistmineuservo)]|false|none||none|

<h2 id="tocS_BlogDraftUpdateDTO">BlogDraftUpdateDTO</h2>

<a id="schemablogdraftupdatedto"></a>

<a id="schema_BlogDraftUpdateDTO"></a>

<a id="tocSblogdraftupdatedto"></a>

<a id="tocsblogdraftupdatedto"></a>

```json
{
  "id": 110,
  "title": "特别特别dui",
  "body": "特别特别dui是特别特别dui的"
}

```

更新博文草稿 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|true|none|博文草稿 id|none|
|title|string|true|none|博文标题|none|
|body|string|true|none|博文内容|none|

<h2 id="tocS_ResultListReferralListMineUserVO">ResultListReferralListMineUserVO</h2>

<a id="schemaresultlistreferrallistmineuservo"></a>

<a id="schema_ResultListReferralListMineUserVO"></a>

<a id="tocSresultlistreferrallistmineuservo"></a>

<a id="tocsresultlistreferrallistmineuservo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "tagsContent": [
        "string"
      ],
      "positionUrl": "string",
      "code": "string",
      "recruitmentType": "校招"
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[ReferralListMineUserVO](#schemareferrallistmineuservo)]|false|none||none|

<h2 id="tocS_ResultListReferralListAllUserVO">ResultListReferralListAllUserVO</h2>

<a id="schemaresultlistreferrallistalluservo"></a>

<a id="schema_ResultListReferralListAllUserVO"></a>

<a id="tocSresultlistreferrallistalluservo"></a>

<a id="tocsresultlistreferrallistalluservo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "authorName": "string",
      "tagsContent": [
        "string"
      ],
      "positionUrl": "string",
      "code": "string",
      "recruitmentType": "校招",
      "status": "草稿"
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[ReferralListAllUserVO](#schemareferrallistalluservo)]|false|none||none|

<h2 id="tocS_ResultUserLoginVO">ResultUserLoginVO</h2>

<a id="schemaresultuserloginvo"></a>

<a id="schema_ResultUserLoginVO"></a>

<a id="tocSresultuserloginvo"></a>

<a id="tocsresultuserloginvo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": {
    "id": 0,
    "role": "string",
    "username": "string",
    "nickname": "string",
    "password": "string",
    "gender": "男",
    "email": "string",
    "phone": "string",
    "avatar": "string",
    "token": "string"
  }
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[UserLoginVO](#schemauserloginvo)|false|none||none|

<h2 id="tocS_UserLoginDTO">UserLoginDTO</h2>

<a id="schemauserlogindto"></a>

<a id="schema_UserLoginDTO"></a>

<a id="tocSuserlogindto"></a>

<a id="tocsuserlogindto"></a>

```json
{
  "phone": "12345678901",
  "password": "123456"
}

```

用户登录 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|phone|string|true|none|手机号|none|
|password|string|true|none|密码|none|

<h2 id="tocS_BlogUserDTO">BlogUserDTO</h2>

<a id="schemabloguserdto"></a>

<a id="schema_BlogUserDTO"></a>

<a id="tocSbloguserdto"></a>

<a id="tocsbloguserdto"></a>

```json
{
  "userId": 103,
  "title": "哈基米",
  "body": "哈基米是哈基米里第一个哈基米的",
  "tagsContent": [
    "哈基米",
    "哈基米里",
    "哈基米的"
  ]
}

```

新建博文 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|userId|integer(int64)|true|none|博文创建者用户 id|none|
|title|string|true|none|博文标题|none|
|body|string|true|none|博文内容|none|
|tagsContent|[string]|true|none|博文标签内容列表|none|
|" 博文标签内容列表|string|false|none|博文标签内容列表|none|

<h2 id="tocS_UserRegisterDTO">UserRegisterDTO</h2>

<a id="schemauserregisterdto"></a>

<a id="schema_UserRegisterDTO"></a>

<a id="tocSuserregisterdto"></a>

<a id="tocsuserregisterdto"></a>

```json
{
  "adminId": 1,
  "username": "user1",
  "nickname": "111",
  "password": "123456",
  "gender": "0",
  "email": "1234@123",
  "phone": "12345678901",
  "avatar": "string"
}

```

管理员为用户注册 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|adminId|integer(int64)|true|none|管理员 id|none|
|username|string|true|none|用户名|none|
|nickname|string|false|none|昵称|none|
|password|string|false|none|密码|none|
|gender|string|false|none|性别 (0- 男 1- 女 2- 其他)|none|
|email|string|false|none|邮箱|none|
|phone|string|true|none|手机号|none|
|avatar|string|false|none|头像|none|

## 枚举值

|属性|值|
|---|---|
|gender|男|
|gender|女|
|gender|其他|

<h2 id="tocS_ResultListBlogListAllUserVO">ResultListBlogListAllUserVO</h2>

<a id="schemaresultlistbloglistalluservo"></a>

<a id="schema_ResultListBlogListAllUserVO"></a>

<a id="tocSresultlistbloglistalluservo"></a>

<a id="tocsresultlistbloglistalluservo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "authorName": "string",
      "tagsContent": [
        "string"
      ],
      "status": "草稿"
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[BlogListAllUserVO](#schemabloglistalluservo)]|false|none||none|

<h2 id="tocS_ActivityUserDTO">ActivityUserDTO</h2>

<a id="schemaactivityuserdto"></a>

<a id="schema_ActivityUserDTO"></a>

<a id="tocSactivityuserdto"></a>

<a id="tocsactivityuserdto"></a>

```json
{
  "userId": 0,
  "title": "string",
  "body": "string",
  "startTime": "2019-08-24T14:15:22Z",
  "endTime": "2019-08-24T14:15:22Z",
  "registrationDeadline": "2019-08-24T14:15:22Z",
  "place": "string",
  "maxPerson": 0
}

```

用户发起活动 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|userId|integer(int64)|true|none|用户 id|none|
|title|string|true|none|活动标题|none|
|body|string|true|none|活动内容|none|
|startTime|string(date-time)|true|none|活动开始时间|none|
|endTime|string(date-time)|true|none|活动结束时间|none|
|registrationDeadline|string(date-time)|true|none|活动报名截止时间|none|
|place|string|true|none|活动地点|none|
|maxPerson|integer(int32)|true|none|报名人数上限|none|

<h2 id="tocS_BidRequestUserDTO">BidRequestUserDTO</h2>

<a id="schemabidrequestuserdto"></a>

<a id="schema_BidRequestUserDTO"></a>

<a id="tocSbidrequestuserdto"></a>

<a id="tocsbidrequestuserdto"></a>

```json
{
  "creatorId": 0,
  "title": "string",
  "body": "string",
  "coreRequirement": "string",
  "pay": 0,
  "startTime": "2019-08-24",
  "endTime": "2019-08-24"
}

```

新建招标 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|creatorId|integer(int64)|true|none|招标发布者用户 id|none|
|title|string|true|none|招标标题|none|
|body|string|true|none|招标内容|none|
|coreRequirement|string|true|none|招标核心需求|none|
|pay|number(double)|true|none|招标报酬|none|
|startTime|string(date)|true|none|招标开始时间|none|
|endTime|string(date)|true|none|招标结束时间|none|

<h2 id="tocS_ReferralDraftDTO">ReferralDraftDTO</h2>

<a id="schemareferraldraftdto"></a>

<a id="schema_ReferralDraftDTO"></a>

<a id="tocSreferraldraftdto"></a>

<a id="tocsreferraldraftdto"></a>

```json
{
  "userId": 103,
  "title": "特别特别对",
  "body": "特别特别对是特别特别对的",
  "positionUrl": "https://www.baidu.com",
  "code": "123456",
  "recruitmentType": "校招"
}

```

新建内推草稿 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|userId|integer(int64)|true|none|内推创建者用户 id|none|
|title|string|true|none|内推标题|none|
|body|string|true|none|内推内容|none|
|positionUrl|string|true|none|内推职位 url|none|
|code|string|true|none|内推码|none|
|recruitmentType|string|true|none|内推类型|none|

## 枚举值

|属性|值|
|---|---|
|recruitmentType|校招|
|recruitmentType|实习|

<h2 id="tocS_PasswordUpdateDTO">PasswordUpdateDTO</h2>

<a id="schemapasswordupdatedto"></a>

<a id="schema_PasswordUpdateDTO"></a>

<a id="tocSpasswordupdatedto"></a>

<a id="tocspasswordupdatedto"></a>

```json
{
  "id": 0,
  "oldPassword": "string",
  "newPassword": "string"
}

```

用户自身更新密码 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|true|none|用户 id|none|
|oldPassword|string|true|none|旧密码|none|
|newPassword|string|true|none|新密码|none|

<h2 id="tocS_ResultListActivityListAllUserVO">ResultListActivityListAllUserVO</h2>

<a id="schemaresultlistactivitylistalluservo"></a>

<a id="schema_ResultListActivityListAllUserVO"></a>

<a id="tocSresultlistactivitylistalluservo"></a>

<a id="tocsresultlistactivitylistalluservo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "authorName": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "startTime": "2019-08-24T14:15:22Z",
      "endTime": "2019-08-24T14:15:22Z",
      "registrationDeadline": "2019-08-24T14:15:22Z",
      "place": "string",
      "maxPerson": 0
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[ActivityListAllUserVO](#schemaactivitylistalluservo)]|false|none||none|

<h2 id="tocS_ReferralDraftReleaseDTO">ReferralDraftReleaseDTO</h2>

<a id="schemareferraldraftreleasedto"></a>

<a id="schema_ReferralDraftReleaseDTO"></a>

<a id="tocSreferraldraftreleasedto"></a>

<a id="tocsreferraldraftreleasedto"></a>

```json
{
  "id": 115,
  "title": "特别特别dui",
  "body": "特别特别dui是特别特别对dui",
  "tagsContent": [
    "特别特别dui",
    "特别特别对dui"
  ],
  "positionUrl": "https://www.baidu.com",
  "code": "123456",
  "recruitmentType": "校招"
}

```

更新内推草稿 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|true|none|内推草稿 id|none|
|title|string|true|none|内推标题|none|
|body|string|true|none|内推内容|none|
|tagsContent|[string]|true|none|内推标签内容列表|none|
|" 内推标签内容列表|string|false|none|内推标签内容列表|none|
|positionUrl|string|true|none|内推职位 url|none|
|code|string|true|none|内推码|none|
|recruitmentType|string|true|none|内推类型|none|

## 枚举值

|属性|值|
|---|---|
|recruitmentType|校招|
|recruitmentType|实习|

<h2 id="tocS_ResultListBidListUserVO">ResultListBidListUserVO</h2>

<a id="schemaresultlistbidlistuservo"></a>

<a id="schema_ResultListBidListUserVO"></a>

<a id="tocSresultlistbidlistuservo"></a>

<a id="tocsresultlistbidlistuservo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "bidderName": "string",
      "phone": "string",
      "resume": "string",
      "quotation": "string"
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[BidListUserVO](#schemabidlistuservo)]|false|none||none|

<h2 id="tocS_ArticleReviewDTO">ArticleReviewDTO</h2>

<a id="schemaarticlereviewdto"></a>

<a id="schema_ArticleReviewDTO"></a>

<a id="tocSarticlereviewdto"></a>

<a id="tocsarticlereviewdto"></a>

```json
{
  "id": 0,
  "isPassed": true
}

```

管理员文章审核 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|false|none|文章 id|none|
|isPassed|boolean|false|none|文章审核是否通过|none|

<h2 id="tocS_UserUpdateByAdminDTO">UserUpdateByAdminDTO</h2>

<a id="schemauserupdatebyadmindto"></a>

<a id="schema_UserUpdateByAdminDTO"></a>

<a id="tocSuserupdatebyadmindto"></a>

<a id="tocsuserupdatebyadmindto"></a>

```json
{
  "adminId": 0,
  "id": 0,
  "username": "string",
  "nickname": "string",
  "password": "string",
  "gender": "男",
  "email": "string",
  "phone": "string"
}

```

管理员为用户更新 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|adminId|integer(int64)|true|none|管理员用户 id|none|
|id|integer(int64)|true|none|用户 id|none|
|username|string|false|none|用户名|none|
|nickname|string|false|none|昵称|none|
|password|string|false|none|密码|none|
|gender|string|false|none|性别 (0- 男 1- 女 2- 其他)|none|
|email|string|false|none|邮箱|none|
|phone|string|false|none|手机号|none|

## 枚举值

|属性|值|
|---|---|
|gender|男|
|gender|女|
|gender|其他|

<h2 id="tocS_BlogDraftDTO">BlogDraftDTO</h2>

<a id="schemablogdraftdto"></a>

<a id="schema_BlogDraftDTO"></a>

<a id="tocSblogdraftdto"></a>

<a id="tocsblogdraftdto"></a>

```json
{
  "userId": 103,
  "title": "特别特别对",
  "body": "特别特别对是特别特别对的"
}

```

新建博文草稿 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|userId|integer(int64)|true|none|博文创建者用户 id|none|
|title|string|true|none|博文标题|none|
|body|string|true|none|博文内容|none|

<h2 id="tocS_BidRequestUpdateUserDTO">BidRequestUpdateUserDTO</h2>

<a id="schemabidrequestupdateuserdto"></a>

<a id="schema_BidRequestUpdateUserDTO"></a>

<a id="tocSbidrequestupdateuserdto"></a>

<a id="tocsbidrequestupdateuserdto"></a>

```json
{
  "bidRequestId": 0,
  "winnerBidId": 0
}

```

更新招标 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|bidRequestId|integer(int64)|true|none|招标 id|none|
|winnerBidId|integer(int64)|true|none|中标 id|none|

<h2 id="tocS_CommentDTO">CommentDTO</h2>

<a id="schemacommentdto"></a>

<a id="schema_CommentDTO"></a>

<a id="tocScommentdto"></a>

<a id="tocscommentdto"></a>

```json
{
  "userId": 0,
  "articleId": 0,
  "parentId": 0,
  "rootId": 0,
  "content": "string"
}

```

用户评论 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|userId|integer(int64)|true|none|发起评论的用户 id|none|
|articleId|integer(int64)|true|none|评论的文章 id|none|
|parentId|integer(int64)|false|none|回复评论 id|none|
|rootId|integer(int64)|false|none|一级评论 id|none|
|content|string|true|none|评论内容|none|

<h2 id="tocS_ReferralDraftUpdateDTO">ReferralDraftUpdateDTO</h2>

<a id="schemareferraldraftupdatedto"></a>

<a id="schema_ReferralDraftUpdateDTO"></a>

<a id="tocSreferraldraftupdatedto"></a>

<a id="tocsreferraldraftupdatedto"></a>

```json
{
  "id": 115,
  "title": "111内推标题",
  "body": "111内推内容",
  "positionUrl": "http://www.baidu.com",
  "code": "123456",
  "recruitmentType": "校招"
}

```

更新内推草稿 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|true|none|内推 id|none|
|title|string|true|none|内推标题|none|
|body|string|true|none|内推内容|none|
|positionUrl|string|true|none|内推职位 url|none|
|code|string|true|none|内推码|none|
|recruitmentType|string|true|none|内推类型|none|

## 枚举值

|属性|值|
|---|---|
|recruitmentType|校招|
|recruitmentType|实习|

<h2 id="tocS_UserDTO">UserDTO</h2>

<a id="schemauserdto"></a>

<a id="schema_UserDTO"></a>

<a id="tocSuserdto"></a>

<a id="tocsuserdto"></a>

```json
{
  "id": 0,
  "username": "string",
  "nickname": "string",
  "password": "string",
  "gender": "男",
  "email": "string",
  "phone": "string",
  "avatar": "string"
}

```

用户自身更新 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|id|integer(int64)|true|none|用户 id|none|
|username|string|false|none|用户名|none|
|nickname|string|false|none|昵称|none|
|password|string|false|none|密码|none|
|gender|string|false|none|性别 (0- 男 1- 女 2- 其他)|none|
|email|string|false|none|邮箱|none|
|phone|string|false|none|手机号|none|
|avatar|string|false|none|头像|none|

## 枚举值

|属性|值|
|---|---|
|gender|男|
|gender|女|
|gender|其他|

<h2 id="tocS_ResultListActivityVO">ResultListActivityVO</h2>

<a id="schemaresultlistactivityvo"></a>

<a id="schema_ResultListActivityVO"></a>

<a id="tocSresultlistactivityvo"></a>

<a id="tocsresultlistactivityvo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "status": "草稿",
      "authorName": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "updateTime": "2019-08-24T14:15:22Z",
      "startTime": "2019-08-24T14:15:22Z",
      "endTime": "2019-08-24T14:15:22Z",
      "registrationDeadline": "2019-08-24T14:15:22Z",
      "place": "string",
      "maxPerson": 0
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[ActivityVO](#schemaactivityvo)]|false|none||none|

<h2 id="tocS_ResultListUserListAdminVO">ResultListUserListAdminVO</h2>

<a id="schemaresultlistuserlistadminvo"></a>

<a id="schema_ResultListUserListAdminVO"></a>

<a id="tocSresultlistuserlistadminvo"></a>

<a id="tocsresultlistuserlistadminvo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "username": "string",
      "nickname": "string",
      "gender": "男",
      "email": "string",
      "phone": "string",
      "avatar": "string"
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[UserListAdminVO](#schemauserlistadminvo)]|false|none||none|

<h2 id="tocS_ResultListBidRequestVO">ResultListBidRequestVO</h2>

<a id="schemaresultlistbidrequestvo"></a>

<a id="schema_ResultListBidRequestVO"></a>

<a id="tocSresultlistbidrequestvo"></a>

<a id="tocsresultlistbidrequestvo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "status": "草稿",
      "authorName": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "updateTime": "2019-08-24T14:15:22Z",
      "coreRequirement": "string",
      "pay": 0,
      "startTime": "2019-08-24",
      "endTime": "2019-08-24",
      "bidRequestStatus": "待中标"
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[BidRequestVO](#schemabidrequestvo)]|false|none||none|

<h2 id="tocS_ResultListArticleVO">ResultListArticleVO</h2>

<a id="schemaresultlistarticlevo"></a>

<a id="schema_ResultListArticleVO"></a>

<a id="tocSresultlistarticlevo"></a>

<a id="tocsresultlistarticlevo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "status": "草稿",
      "authorName": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "updateTime": "2019-08-24T14:15:22Z",
      "tagsContent": [
        "string"
      ]
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[ArticleVO](#schemaarticlevo)]|false|none||none|

<h2 id="tocS_ResultListCommentListUserVO">ResultListCommentListUserVO</h2>

<a id="schemaresultlistcommentlistuservo"></a>

<a id="schema_ResultListCommentListUserVO"></a>

<a id="tocSresultlistcommentlistuservo"></a>

<a id="tocsresultlistcommentlistuservo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "posterName": "string",
      "avatar": "string",
      "content": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "subComment": [
        {
          "id": 0,
          "posterName": "string",
          "repliedPersonName": "string",
          "avatar": "string",
          "content": "string",
          "createTime": "2019-08-24T14:15:22Z"
        }
      ]
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[CommentListUserVO](#schemacommentlistuservo)]|false|none||none|

<h2 id="tocS_BidUserDTO">BidUserDTO</h2>

<a id="schemabiduserdto"></a>

<a id="schema_BidUserDTO"></a>

<a id="tocSbiduserdto"></a>

<a id="tocsbiduserdto"></a>

```json
{
  "userId": 0,
  "bidRequestId": 0,
  "resume": "string",
  "quotation": 0
}

```

新建投标 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|userId|integer(int32)|true|none|投标人用户 id|none|
|bidRequestId|integer(int32)|true|none|招标 id|none|
|resume|string|true|none|投标人简历|none|
|quotation|number(double)|true|none|投标报价|none|

<h2 id="tocS_ResultListReferralVO">ResultListReferralVO</h2>

<a id="schemaresultlistreferralvo"></a>

<a id="schema_ResultListReferralVO"></a>

<a id="tocSresultlistreferralvo"></a>

<a id="tocsresultlistreferralvo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "title": "string",
      "body": "string",
      "status": "草稿",
      "authorName": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "updateTime": "2019-08-24T14:15:22Z",
      "tags": [
        "string"
      ],
      "positionUrl": "string",
      "code": "string",
      "recruitmentType": "校招"
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[ReferralVO](#schemareferralvo)]|false|none||none|

<h2 id="tocS_ResultListTagAdminVO">ResultListTagAdminVO</h2>

<a id="schemaresultlisttagadminvo"></a>

<a id="schema_ResultListTagAdminVO"></a>

<a id="tocSresultlisttagadminvo"></a>

<a id="tocsresultlisttagadminvo"></a>

```json
{
  "code": 0,
  "msg": "string",
  "data": [
    {
      "id": 0,
      "content": "string",
      "creatorName": "string",
      "createTime": "2019-08-24T14:15:22Z",
      "useCount": 0
    }
  ]
}

```

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|code|integer(int32)|false|none||none|
|msg|string|false|none||none|
|data|[[TagAdminVO](#schematagadminvo)]|false|none||none|

<h2 id="tocS_ActivityRegistrationUserDTO">ActivityRegistrationUserDTO</h2>

<a id="schemaactivityregistrationuserdto"></a>

<a id="schema_ActivityRegistrationUserDTO"></a>

<a id="tocSactivityregistrationuserdto"></a>

<a id="tocsactivityregistrationuserdto"></a>

```json
{
  "activityId": 0,
  "userId": 0,
  "remark": "string"
}

```

用户注册活动 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|activityId|integer(int64)|true|none|要报名的活动 id|none|
|userId|integer(int64)|true|none|用户 id|none|
|remark|string|false|none|报名备注|none|

<h2 id="tocS_ReferralUserDTO">ReferralUserDTO</h2>

<a id="schemareferraluserdto"></a>

<a id="schema_ReferralUserDTO"></a>

<a id="tocSreferraluserdto"></a>

<a id="tocsreferraluserdto"></a>

```json
{
  "userId": 103,
  "title": "内推标题",
  "body": "内推内容",
  "tagsContent": [
    "内推标签1",
    "内推标签2"
  ],
  "positionUrl": "https://www.baidu.com",
  "code": "123456",
  "recruitmentType": "校招"
}

```

新建内推 DTO

# 属性

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|userId|integer(int64)|true|none|内推创建者用户 id|none|
|title|string|true|none|内推标题|none|
|body|string|true|none|内推内容|none|
|tagsContent|[string]|true|none|内推标签内容列表|none|
|" 内推标签内容列表|string|false|none|内推标签内容列表|none|
|positionUrl|string|true|none|内推职位 url|none|
|code|string|true|none|内推码|none|
|recruitmentType|string|true|none|内推类型|none|

## 枚举值

|属性|值|
|---|---|
|recruitmentType|校招|
|recruitmentType|实习|
