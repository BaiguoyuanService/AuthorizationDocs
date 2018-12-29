# AuthorizationDocs
授权登录方案

 #### 1. BPTX为每个二级应用提供appid,secret;

 #### 2. 二级应用自己准备一个回调的地址,进行access_token的信息接收；

 #### 3. 二级应用使用BPTX登录；

 >a. 通过webview打开一个BPTX的授权登录页面；

         https://****/login?appid=1&secret=2&redirect_uri=3

         {
            appid         // appid
            secret        // secret
            redirect_uri  // 回调地址
         }

 >b. 用户通过网页进行登录，登录成功后回调二级应用回调地址
 
         请求方式： post
         返回参数：
         {
              "access_token":"ACCESS_TOKEN",    // access_token
              "expire":604800000,               // 过期时间（秒）
         }

#### 4. 二级应用可通过access_token进行以下操作：
    >a. 获取用户资料
    
    请求方式： get
    请求地址： https://****/api/v1/user/tp/info?access_token=ACCESS_TOKEN
    返回参数：
    {
        "data": {
            "userId": "1068060421518286850"
        },
        "errcode": 0,
        "errmsg": "成功"
    }


    >b. 获取银行卡信息
    
    请求方式： get
    请求地址： https://****/api/v1/user/tp/bank/list?access_token=ACCESS_TOKEN
    返回参数：
    {
        "data": [
            {
                "name": "中国银行",
                "account": "14545454545454545",
                "openingName": "姓名"
            }
        ],
        "errcode": 0,
        "errmsg": "成功"
    }

#### 5. 刷新access_token

    请求方式： get
    请求地址： https://****/api/v1/user/tp/refreshToken?access_token=ACCESS_TOKEN
    返回参数：
    {
        "data": {
            "access_token": "ACCESS_TOKEN",    // access_token
            "expire": 604800000                // 过期时间（秒）
        },
        "errcode": 0,
        "errmsg": "成功"
    }



