# Javascript_Chat_Sample 

## 시작하기
JavaScript(WEB) PartnerPush SDK 설정하는 방법에 대해 설명을 시작합니다.

## PartnerPush JavaScript SDK 설명
PartnerMQTTFramework를 다운받으세요.
해당 html,project에서 다운받은 JS파일을 불러오세요

## init 설명 및 구현방법
init이란 PartnerPush에 푸시서비스를 연결하는 함수입니다. (javascript에서는 Client 객체 생성시 자동으로 init()해주고 있습니다)
사용자의 project가 Client가 되고 저희 Partner가 server가 되어 Push service를 제공합니다.

## MQTT 연결 요청
 
push service를 사용하기 위해 사용자는 클라이언트 객체를 생성해주어야 합니다. 
여기에 필요한 정보로는 

1. appId -> Project별 구분 Key로 PartnerBiz에서 발급받을 수 있습니다. ex) chatProject, webProject
2. apiKey -> platform별 구분 Key로 PartnerBiz에서 발급받을 수 있습니다. ex)Android, ios, web(javascript)
가 필요합니다.

아래는 예시입니다.

    pushClient = new PartnerPush.Client({
        appId: "appId",  //필수 항목
        apiKey : "apikey", //필수 항목
        onPPReceived : function, // 선택사항  메세지를 받았을때 실행되는 interface
        onPPConnected : function, // 선택사항 연결이 성공했을때 실행되는 interface
        onPPFail : function // 선택사항 연결이 실패했을때 실행되는 interface
	});
	
선택 사항은 overriding해서 사용하는 interface들로. function 자리에 사용자가 지정해서 함수를 넣으면 됩니다.


## 구독

클라이언트명.appTopic("구독할 토픽명");
ex)  pushClient.addTopic("Test Topic");
  
## 구독해제

클라이언트명.appTopic("구독 해제할 토픽명");
ex)  pushClient.removeTopic("Test Topic");

## 발행(json 타입 보내기)

##### [QOS를 생략할 경우. 1로 defualt 설정 되어서 보내짐.]

 -  `pushClient.sendMessage('Test Topic', JSON.stringify(payload))` : 클라이언트명.sendMessage('토픽명', JSON.stringify(payload))

##### [QOS를 지정할 경우. 지정한 QOS를 파라미터로 삽입해야함.]
 - `pushClient.sendMessage('Test Topic', JSON.stringify(payload), 0)` : 클라이언트명.sendMessage('토픽명', JSON.stringify(payload),QOS);
 
 [QOS는 0,1,2의 매개변수로 전달해주면 됩니다.]

- - -


``` javascript
var payload = {
    nickname : 'hello',
    text : msg
};

pushClient.sendMessage('Test Topic', JSON.stringify(payload));
pushClient.sendMessage('Test Topic', JSON.stringify(payload), 0);

```

## 연결
##### 클라이언트명.connect(); 
```
pushClient.connect();
```

## 연결해지
##### 클라이언트명.disconnect();

```
pushClient.disconnect();

```
## 오류코드

### 버전 히스토리

2015.06.25 - pp3 설명.
