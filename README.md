<h1>✨ 맡은 업무 설명</h1>
<h2> 1. SKT 프로젝트 </h2>
      
      - 유지보수성 개발을 주로 맡음
      - 그 중 
      
<h3> 💻 개발 환경 </h3>

      1. javascript
      2. Aungular.js ~1.5.5
      3. jquery ~2.1.3

```javascript
// webWorker 일부 수정 발췌
var worker = (function () {

    let workData; // global

    onmessage = function (e) {
        console.log("#### In Worker ##### " + e.data);
        workData = e.data;

        if (workData.command == "start"){
            startProgressData();
        }
    }

    function startProgressData () {
    console.log("#### In startProgressData #####");
        var rowData = workData.data;
        var interval = workData.interval;
        var path = workData.path;

        postData(path , { 데이터 정보 })
            .then(responseData => checkProcessStatus(responseData, interval))
    }

    function checkProcessStatus(responseData, interval) {
        if (isFail(responseData))
            return;

        try {
            var dataJson = JSON.parse(responseData);
        } catch (e) {
            console.error("error", e, responseData);
            setTimeout(startProgressData, interval);
            return;
        }
        if (dataJson.uploadState == "SUCCESS") {
            postMessage({
                "command": "success",
                "data": dataJson
            })
            self.close();
        } else {
            console.log("#### In startProgressStatus - Checking #####");
            postMessage({
                "command": "checking",
                "data": dataJson
            })

            setTimeout(startProgressData, interval);
        }

    }

    function isFail(data) {
        if (data == "") {
            postMessage({
                "command":"failed",
                "data":data
            })
            self.close();
            return true;
        }
        return false;
    }

    function postData(url = '', data = {}) {
        // Default options are marked with *
        return autoRefreshFetch(url, {
            method: 'POST',
            credentials: 'include',
            cache: 'no-cache',
            credentials: 'same-origin',
            headers: {
                 'Content-Type': 'application/x-www-form-urlencoded',
            },
            referrer: 'no-referrer',
            body: new URLSearchParams(data), // body data type must match "Content-Type" header
        })
            .then(response => response.text()).catch(response => console.log(response)); // parses JSON response into native JavaScript objects
    }

    var autoRefreshFetch = function() {
        let originFetch = this;
        let args = arguments;
        return fetch.apply(originFetch, args).then(async function(data) {
            if (data.status === 401 || data.status === 403) {
                var token = workData.session;
                await fetch("URI"}", {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/x-www-form-urlencoded',
                    },
                    body: new URLSearchParams({
                        사용자 정보
                    })
                }).then(async response => {
                    if (response.status != 200)
                        return;

                    var refreshTokenData = await response.json();
                    var token = {
                        토큰 데이터
                    };

                    self.postMessage({
                        "command": "refreshToken",
                        "data": refreshTokenData
                    })
                })

                console.log('failed');
                return fetch(args[0], args[1]);
                
                console.log(response);
                if (response.status === 401) {
                    return {};
                }
            }

            return data;

        });
    };
})();
```


--------------
<h2> 2. 삼성전자 프로젝트</h2>

     - 사용자관리, 로그인, 메뉴관리, 권한관리, Tenant관리, IP 권한관리, 세션관리, 세션 히스토리관리, 3rd party 관리, NE Group 관리 등 RestAPI 개발하였음.
      - Exception 처리 나 log 등 다국어처리가 될 수 있도록 개발하였음.
      - 로그인 사용자의 권한과 세션체크 경험이 있음.
      
<h3> 💻 개발 환경 </h3>

      1. java 
      2. Springboot


