# serverless 프레임워크를 aws-serverless 사용하기


<br><br><br>

------------

<br><br><br>


## 본 세션을 진행하기 위해 필요한 것들

- Node.js 6 이상 - [Windows Installer][nodejs-windows-installer] / [macOS Installer][nodejs-macos-installer] / [Linux Installer][nodejs-linux-installer]
- Javascript IDE - [Jetbrains WebStorm][webstorm-download] / [Microsoft VSCode][vscode-download]
- Postman - [Download][postman-download]
- aws 계정
<br><br><br>

## 결과물 git

```bash
$ git clone https://github.com/freechild/aws_serverless.git
```

## 개발환경 준비

## IAM Credential 준비

### IAM Key 발급

> What's IAM?
>
> IAM은 AWS에 대한 접근을 관리하는 서비스입니다. 
> 필요에 따라 여러 종류의 권한을 부여,삭제가 가능하다.

1. [AWS Console][aws-console] 로그인
2. [IAM Console][iam-console] 이동
3. 사용자 추가
4. 추가된 유저에서 권한 부여 ( AdministratorAccess ) 
5. 발급된 Access Key ID,Secret Key ID 저장


<br><br><br>

## 사용
1. serverless 설치
```bash
npm install -g serverless -g
```

2. serverless 프로젝트 생성

ex)
```bash
sls create -t 사용할 템플릿 -p 경로의 폴더명
```

따라하기)

```bash
sls create -t aws-nodejs -p hello-wolrd
```

<br>
3. aws 계정 설정 (프로젝트 폴더로 이동)
<br>
###키 입력란에 발급받은 키를 입력해주세요.

```bash
cd hello-wolrd
echo 'export AWS_ACCESS_KEY_ID=Access Key 입력' >> .aws-credentials
echo 'export AWS_SECRET_ACCESS_KEY=Secret Key 입력' >> .aws-credentials
source .aws-credentials
```
<br>
4. 설정파일 수정
###프로젝트 파일안에 있는 serverless.yml 열어봅시다.
###provider 설정
###ps. 한국지역명 :  ap-northeast-2

ex)
```js
provider:
  name: aws
  runtime: server version
  stage: 스테이지명
  region: 지역명
```

따라하기)
```js
provider:
  name: aws
  runtime: nodejs8.10
  stage: dev
  region: ap-northeast-2
```

라우터 설정 ( 라우터 설정시 api 게이트웨이 설정됨)<br>
ex)
```js
functions:
  hello:
    handler: 파일/함수명
    events:
      - http:
          path: 주소
          method: http method (get,post,put 등등)
    이외 기능들은 문서를 참고      
```

따라하기)
```js
functions:
  hello:
    handler: handler.index
    events:
      - http:
          path: hello
          method: get      
```

<br>
5. 람다 함수 생성
<br>
이제 만들어진 파일을 최초로 푸시를 합시다. (최초의 푸시는 시간이 걸립니다.)

```bash
sls deploy
```



[nodejs-windows-installer]: https://nodejs.org/dist/v8.11.4/node-v8.11.4-x86.msi
[nodejs-macos-installer]: https://nodejs.org/dist/v8.11.4/node-v8.11.4.pkg
[nodejs-linux-installer]: https://github.com/nodesource/distributions
[chrome-download]: https://www.google.com/chrome/
[webstorm-download]: http://www.jetbrains.com/webstorm/download/
[vscode-download]: https://code.visualstudio.com/download
[postman-download]: https://www.getpostman.com/apps
[aws-console]: https://console.aws.amazon.com/console/home?region=ap-northeast-2
[iam-console]: https://console.aws.amazon.com/iam/home?region=ap-northeast-2
