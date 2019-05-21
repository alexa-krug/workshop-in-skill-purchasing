> Alexa KRUG에서 현재 한글화 작업을 진행중 입니다. 작업에 참여하실 분들은 파일 단위로 번역하실 issue를 먼저 작성하신 후에 작업하시고 PR을 보내주시면 됩니다. 번역 작업 전에 꼭 [AWSKRUG 핸즈온랩 번역 가이드](https://github.com/awskrug/awskrug-rule-book/wiki/Hands-on-lab-translation-guide)를 읽어주세요. PR전에는 실제 동작여부까지 테스트 해 주시기 바랍니다. 궁금하신점은 [페이스북 Alexa 한국 사용자 모임](https://www.facebook.com/groups/kalexa)으로 문의 주세요.

## 인스킬 구매(In-Skill Purchasing) 워크샵

이 워크샵에서는 인스킬 구매를 이용하여 소비재를 다루는 샘플 스킬 작성합니다.

[곧바로 워크샵 진행으로 넘어가기](#워크샵)

## 알렉사 스킬(Skill)

### 스킬 개관

이 워크샵에서 구축할 스킬은 플레이어에게 단서(배우 이름)를 말해주는 게임입니다. 플레이어는 추측한 답(배우가 주요 인물을 묘사하는 TV드라마)을 말할 수 있고, 다른 단서(다른 배우)를 원한다면 힌트를 요청할 수 있습니다. 힌트는 5개 묶음으로 판매하고, 가격은 0.99센트입니다.

### 사용자 상호작용(interaction) 예시

다음은 워크샵에서 만들 스킬의 사용자 상호작용 예시입니다. 일부 대화는 쉽게 읽을 수 있도록 축약하였습니다.

:speech_balloon: User: "Alexa, open name the show"
:speech_balloon: 사용자: "알렉사, name the show 열어줘."

:loud_sound: Alexa: "Welcome to Name the Show, the game where you try to guess the show based on the actors in it. Are you ready to begin?"
:loud_sound: 알렉사: "출연 배우로 드라마 이름을 추측하는 게임인 Name the Show 에 오신 것을 환영합니다. 시작할 준비되셨나요?"

:speech_balloon: User: "Yes"
:speech_balloon: 사용자: "네"

:loud_sound: Alexa: "Your clue is Billy Bob Thornton. What show do you guess?"
:loud_sound: 알렉사: "당신의 단서는 빌리 밥 손튼. 당신의 추측은?"

:speech_balloon: User: "Man in the high castle"
:speech_balloon: 사용자: "Man in the high castle"

:loud_sound: Alexa: "That is incorrect. Please guess again. What show do you guess?"
:loud_sound: 알렉사: "틀렸습니다. 다시 추측해 보세요. 당신의 추측은?"

:speech_balloon: User: "Give me a hint"
:speech_balloon: 사용자: "힌트 좀 줘"

:loud_sound: Alexa: "You currently do not have any hints, would you like to learn more about the Five Hint Pack?"
:loud_sound: 알렉사: "힌트를 가지고 있지 않군요, 다섯 힌트 팩에 대해서 알려드릴가요?"

:speech_balloon: User: "Yes"
:speech_balloon: 사용자: "네"

:loud_sound: Alexa: "The Five Hint Pack is available for 99 cents. Would you like to buy it?"
:loud_sound: 알렉사: "다섯 힌트 팩은 99 센트에 구입 가능합니다. 구입하시겠어요?"

:speech_balloon: User: "Yes"
:speech_balloon: 사용자: "네"

:loud_sound: Alexa: "Great, you now own a five hint pack. Here's your clue: Billy Bob Thornton and Nina Arianda. Which show do you guess?"
:loud_sound: 알렉사: "좋아요, 이제 다섯개의 힌트 팩을 가졌네요. 단서를 알려드리죠. 빌리 밥 손튼과 니나 아리안다. 당신의 추측은?"

:speech_balloon: User: "Goliath"
:speech_balloon: 사용자: "골리앗"

:loud_sound: Alexa: "Correct, the show I was thinking of was Goliath. Would you like to play again?"
:loud_sound: 알렉사: "정답, 내가 생각한 드라마는 골리앗이었어요. 더 해보시겠어요?"

:speech_balloon: User: "No"
:speech_balloon: 사용자: "아니요"
(스킬을 종료합니다)

### 아키텍처

스킬 아키텍처는 아마존 다이나모DB(Amazon DynamoDB) 테이블에 각 사용자 세션에 대한 영속적인 특성(힌트 인벤토리를 포함)을 저장하는 AWS 람다(AWS Lambda) 함수로 구성되어 있습니다.
스킬의 상호작용 모델은 알렉사 스킬킷(Alexa Skill Kit)으로 관리되고 인스킬 제품 카다로그(In-Skill Product Catalog)와 지불 흐름(Payment Flow)는 알렉사 수익화 서비스(Alexa Monetization Service)에서 관리합니다.
스킬의 처리 로직은 Node.js로 작성하였고, 알렉사 스킬 SDK(Alexa Skill SDK, ASK SDK)를 활용합니다.

여기 자세한 아키텍처 다이어그램이 있습니다.
![상세 아키텍처 다이어그램](./workshop-architecture.png)

## 워크샵

이 워크샵은 세가지 실습으로 구성되어 있습니다. 각 실습을 완료하는데 약30분 정도 걸립니다.

스킬의 시작 상태에 프리미엄 기능(힌트)은 이미 스킬에 추가되어 있습니다.
이 워크샵에서는 힌트 팩의 인스킬 구매 기능을 추가할 것입니다.

### 첫번째 실습 - 상품의 설정과 구성

첫번째 실습에서는 워크샵의 요구사항(prerequisites)을 갖추고, 기반 스킬을 배포하며 인스킬 상품 카다로그(In-Skill Product Catalog)에 제품을 추가합니다.

[Lab 1](./lab-1-guide.md)

### 두번째 실습 - 음성으로 제품 구매를 가능하게(ISP)

두번째 실습에서는 힌트 구매에 관련된 인텐트(intent)를 포함한 스킬의 음성 상호작용 모델을 갱신합니다.
추가로 스킬 처리 코드를 갱신하여 새 인텐트 뿐만 아니라 알렉사 수익화 서비스를 다룹니다.

[Lab 2](./lab-2-guide.md)

### 세번째 실습 - 재고 유지 관리

세번째 실습에서는 스킬의 상호작용 모델을 갱신하여 힌트 재고 수준(남은 힌트 개수)를 확인하는 인덴트를 추가하고, 재고 수준을 저장할 아마존 다이나모DB를 만들며,
스킬 처리 코드를 갱신하여 새 인텐트를 다루며 데이터 테이블에 재고 수준를 저장합니다.

[Lab 3](./lab-3-guide.md)

## 워크샵 이후

이 워크샵을 마치면 다음 단계의 스킬을 시도해 볼 수 있습니다. 제안하는 다음 단계는 [여기](./next-steps.md)에서 찾아볼 수 있습니다.

### 커뮤니티 리소스

[아마존 개발자 포럼](https://forums.developer.amazon.com/spaces/165/index.html)

[알렉사 스킬 - 사용자 목소리](https://alexa.uservoice.com)

## 라이선스

본 라이브러리는 Amazon Software License 라이선스를 따릅니다.
