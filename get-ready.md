워크숍을 시작하기 전에 다음을 확인해주세요.

# 워크숍 필수 구성 요소

1. Amazon Developer 계정
2. AWS 계정
3. ASK CLI

## Amazon Developer 계정

1. 브라우저에서 [https://developer.amazon.com](https://developer.amazon.com/)을 방문해주세요.
2. 기존 계정 또는 새로운 계정을 생성하여 로그인해주세요.
3. 회사 정보는 모두 입력해주셔야 합니다.

## Amazon Web Services (AWS) 계정

1. 브라우저에서 [https://aws.amazon.com](https://aws.amazon.com/)을 방문해주세요.
2. 기존 계정 또는 새로운 계정을 생성하여 로그인해주세요.
3. 새로운 계정을 생성하기 위해서는 신용카드와 휴대폰이 필요합니다.

> 참고 : 새로운 AWS 계정을 생성하기 위해서는 신용카드가 필요합니다. 워크숍에서 진행되는 실습은 모두 AWS Free Tier로 진행할 수 있습니다. 계정의 Free Tier가 만료된 경우 워크숍에서 진행되는 실습은 소량의 사용 요금이 청구될 수 있습니다.

## Alexa Skills Kit Command Line Interface (ASK CLI)

실습을 진행하려면 ASK CLI가 필요합니다. ASK CLI가 로컬 환경에 아직 설정되지 않았다면 다음 단계에 따라 ASK CLI를 개발 환경(AWS Cloud9)에 설정해주세요. 이 단계는 반드시 AWS 계정을 가지고 있어야 합니다.

ASK CLI가 설정되어 있으신 분들은 다음 세션으로 넘어가 주세요.

Cloud9 대신 로컬 환경에서 ASK CLI를 설정하시려면 [여기](https://alexa.design/cli)를 클릭해주세요. 

1. AWS 계정에 로그인하세요.
2. [Cloud9](https://console.aws.amazon.com/cloud9/home)으로 이동하세요.
3. Create environment를 클릭하고 "ASK Workshop"으로 이름을 설정합니다. 
4. 기본 값을 적용하고 Next를 클릭합니다.
5. Review를 확인 후 Create environment를 클릭합니다.
6. 환경이 생성되는 동안 잠시 기다려주세요.
7. 환경이 준비되면, 기본 생성된 bash 터미널에 다음 명령을 입력해주세요. 이 명령은 ASK CLI를 설치합니다.
	```
	npm install ask-cli -g
	``` 
8. 다음 명령을 입력하여 ASK CLI의 환경을 설정해주세요.
	```
	ask init --no-browser
	```
9. 기본 프로필을 사용하시려면 **ENTER**를 눌러주세요. 이것은 Cloud9에서 관리하는 AWS 임시 보안 자격 증명을 사용합니다. 임시 보안 자격 증명에 대한 자세한 내용을 보시려면 [여기](https://docs.aws.amazon.com/cloud9/latest/user-guide/auth-and-access-control.html#auth-and-access-control-temporary-managed-credentials)를 클릭해주세요.
10. 생성된 링크를 클릭하세요. 팝업 메뉴에서 **Open**을 클릭하면 브라우저에서 새 탭이 열립니다. 해당 탭에서 Amazon Developer 계정을 로그인해주세요.
11. **Allow**를 클릭하면 브라우저에 코드가 나타납니다. 이 코드를 복사해주세요.
12. Cloud9 터미널로 돌아와서 복사한 코드를 붙여 넣어주세요.
13. 만약 연결된 벤더 ID가 2개 이상인 경우 사용할 벤더 ID를 선택해주세요.
    > 벤더 ID를 조회할 수 없는 경우(error message is 'call list-vendors error' / 401 / 'You are not authorized to access this operation')는 일반적으로 개발자 계정이 완전히 생성되지 않았음을 의미합니다. https://developer.amazon.com/alexa-skills-kit으로 돌아가서 요청된 정보를 모두 작성해주세요.
14. 이제 ASK CLI가 설치 및 설정이 완료되었으므로 Cloud9의 임시 보안 자격 증명과 함께 작동하도록 하는 마지막 단계가 남아있습니다. 다음 명령을 입력해주세요.
	```
	echo 'export ASK_DEPLOY_ROLE_PREFIX=Cloud9-' >> ~/.bashrc
	```
	이것은 ASK CLI가 Cloud9의 임시 보안 자격 증명 제한과 호환되는 IAM 역할을 생성할 수 있도록 하는 환경 변수를 설정합니다.
15. **IMPORTANT** 새 환경 변수를 사용하려면 현재 터미널 세션을 닫고(exit 입력 또는 터미널 탭의 x 클릭) 새로운 터미널 세션을 시작하세요.(+를 누른 후 New Terminal 선택)

## ASK-CLI 버전 확인

터미널 / 명령 프롬프트에서 다음 명령을 입력해주세요.
```
ask --version
```
ask의 버전은 최소 1.4.5 이상이어야 합니다. 버전이 1.4.5보다 낮은 경우, 다음 명령을 실행하여 CLI를 업데이트해주세요.
```
npm install ask-cli -g
```

모든 준비가 완료되었습니다. 워크숍이 시작되기 전까지 잠시 기다려주세요.

감사합니다.