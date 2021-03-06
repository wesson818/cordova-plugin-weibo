#Weibo

Plugin for weibo, the popular twitter-like service in China. Help user get oauth2/access_token to further access weibo content.

Please refer to [weibo oauth2](ttp://open.weibo.com/wiki/OAuth2/access_token)

##Methods

  ```Weibo.login(clientId, redirectUrl, success, fail);```

* login
   * clientId, the AppKey assigned by weibo service when you apply a new application
   * redirectUrl, the callback url same as in your app registration
   * success, success callback
   * fail, error callback

##Supported Platforms

- Android
- iOS

##Quick Example

    var clientId = "12312312313";
    var redirectUrl = "http://www.server.com";

    // ... later on ...

    Weibo.login(clientId, redirectUrl, success, fail);

##Full Example

    <!DOCTYPE html>
    <!--
        Licensed to the Apache Software Foundation (ASF) under one
        or more contributor license agreements.  See the NOTICE file
        distributed with this work for additional information
        regarding copyright ownership.  The ASF licenses this file
        to you under the Apache License, Version 2.0 (the
        "License"); you may not use this file except in compliance
        with the License.  You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

        Unless required by applicable law or agreed to in writing,
        software distributed under the License is distributed on an
        "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
         KIND, either express or implied.  See the License for the
        specific language governing permissions and limitations
        under the License.
    -->
    <html>
        <head>
            <meta charset="utf-8" />
            <meta name="viewport" content="width=device-width,height=device-height,user-scalable=no,initial-scale=1.0" />
            <meta http-equiv="Content-type" content="text/html; charset=utf-8">
            <link rel="stylesheet" href="master.css" type="text/css" media="screen" title="no title" charset="utf-8">
            <title>Hello Weibo</title>
            <script type="text/javascript" src="cordova.js"></script>
            <script type="text/javascript" src="Weibo.js"></script>
            <script type="text/javascript" charset="utf-8">

                var Weibo = cordova.require("cordova/plugin/Weibo");

                /**
                 * Function called when page has finished loading.
                 */
                function init() {
                    document.addEventListener("deviceready", function() {
                        document.getElementById('status').innerText = "ondeviceready!";},
                        false);
                };

                var clientId = "3968026932";
                var redirectUrl = "http://www.igo.cn";
                function WeiboLogin() {
                    Weibo.login(clientId, redirectUrl, success, fail);
                };

                function WeiboLoginWithRedirectUrlNull() {
                    Weibo.login(clientId, null, success, fail);
                };

                function WeiboLoginWithRedirectUrlEmpty() {
                    Weibo.login(clientId, "", success, fail);
                };

                function success(result) {
                    var loginResult = "";
                    loginResult = loginResult + "access_token:" + result.access_token + "\n";
                    document.getElementById('status').innerText = "success";
                    document.getElementById('result').innerText = loginResult;
                };

                function fail(result) {
                    document.getElementById('status').innerText = "fail";
                    document.getElementById('result').innerText = "fail:" + result;
                };
            </script>
        </head>
        <body id="stage" class="theme">
           <h1>Weibo</h1>
            <div id="info">
                status: <span id="status"></span><br/>
                result: <span id="result"></span><br/>
            </div>
            <div class="btn large" onclick="WeiboLogin();">WeiboLogin</div>
            <div class="btn large" onclick="WeiboLoginWithRedirectUrlNull();">RedirectUrlNull</div>
            <div class="btn large" onclick="WeiboLoginWithRedirectUrlEmpty();">RedirectUrlEmpty</div>
            <script type="text/javascript">
                init();
            </script>
        </body>
    </html>
