## 2장. 전자 회로의 조합 논리
> 비트를 동작 시키는 모든 물리적 장치를 하드웨어라고 한다.

> 조합논리(논리연산)를 구현하는 하드웨어를 살펴보자

### 1. 디지털 컴퓨터의 사례
```
1. 과거 톱니 바퀴를 사용한 기계 계산 장치에서 기계식 컴퓨터를 만든 윌리엄 오트레드의 계산자로 발전되었다. => 현대의 비행컴퓨터로 사용됨 log(x*y) = log(x)+log(y)
2. 기원전 부터 탤리 막대를 사용하여 계산장치로 사용함
```
- 아날로그와 디지털의 차이
    - 아날로그는 연속적(실수를 표현할수 있다는 말)인것을 뜻하고, 디지털은 이산적인것을 뜻함(이산적 : 연속되지않고 , 정수와 같은정해진값을 뜻함)
    - 손가락은 이산적이고, 계산자는 연속적임
- 하드웨어에서 크기가 중요한 이유
    - 컴퓨터에서 전자의 이동시간을 최소화 하는 방법은 부품을 최대한 가깝게 위치 시키는 것
    - 컴퓨터 클록속도(프로세스 속도)는 4GHz이다.
    - 전자의 이동거리가 줄어들면 전력과 발열손상을 막을수 있다.
- 디지털을 사용하면 더 안정적인 장치를 만들 수 있다.
    - 하드웨어를 작게 만들면 문제점이 서로 간섭하기 쉬워진다.
    - 전자 기력은 중력과 마찬가지로 멀리 떨어진 물체에 영향을 끼칠수 있다.
    - 높은 판정기준(간섭 안하게 하는 기준)을 통해 잡음 내성(신호 간섭을 안하는)을 갖는 디지털 회로를 사용하는 것이 필수
- 아날로그 세계에서 디지털 만들기
    - 증폭기를 예로 들면 증폭기는 전이함수라는 아날로그(연속적인) 그래프를 그려주는데, 증폭기를 가파르게 설정하여 왜곡이 발생하게 되면 연속적인 공간을 이산적인 영역으로 나눠줄수있다.
- 10진 숫자 대신 비트를 사용하는 이유
    - 비용이나 편의성에서 유용하기 때문에 사용
### 2. 간단한 전기 이론 가이드
- 전기는 수도 배관과 유사하다.
    - 게이트 밸브가 닫혀 있으면 0, 열려있으면 1로 가정
    ```
        직렬 연결 : AND 연산자을 구현 , 한 밸브의 출력이 다른 밸브와 이어져 있을 경우
        병렬 연결 : OR 연산자를 구현, 두 밸브의 입력을 한관에 함께 연결하고, 두 밸브의 출력을 한관으로 연결 (P.103 참조)
        전파 지연 : 전기가 컴터 칩 내부에서 전파되는데 시간이 걸리는것
        도체 : 전자가 흐르는 금속선
        부도체 : 금속을 둘러싼 바깥부분
        스위치 : 전기의 흐름을 제어
        전압 : 물이 압력으로 흐르는 것처럼 전기도 압력에 의해 흐름 (전압의 측정단위는 볼트(V))
        전류 : 전기흐름의 양 (측정단위는 암페어(A))
        저항 : 전류가 흐르는데 도체가 가늘수록 제한이 걸리는것(측정단위는 옴)
        옴의 법칙 : 전류 = 전압 /저항 (I = V/R)
    ```
- 전기 스위치
    ```
        회로 : 전기 시스템 , 스키매틱(회로도)를 통해 문서화 한다. (회로도 기호 P.105참조)
        단극단투 : 스위치수가 1개 인 통로
        단극쌍투 : 하나의 스위치에서 2갈래의 통로로 이동가능한 것 (P.106참조)
        쌍극쌍투 : 두개의 스위치에서 각각 스위치의 2갈래 통로로 이동가능한 것
        회로는 전류가 흐른뒤 다시 근원으로 돌아간다.
    ```
### 3. 비트를 처리하기 위한 하드웨어
- 릴레이
    - 선을 둥글게 감아서 코일로 만들고 전기를 흘러보내면 [전자석]이됨
    - 코일 주변에 자석을 움직으면 전기가 발생 (닥터스톤보면 알수 있음 ㅇㅇ)
    - 릴레이 : 코일로 만들어진 전자석을 n극과 s극을 이용해 스위치를 움직이는데 사용하는 장치
    ```
        평상시 열린 릴레이 : 코일에 전력이 들어가지 않아 스위치가 열려있음
        평상시 닫힌 릴레이 :  코일에 전력이 들어가지 않아 스위치가 닫혀있음
    ```
    - 릴레이를 사용하면 NOT함수를 구현한 인버터(직류 를 교류로 바꾸는 전기변환 장치)를 만들수있음
    - 그레이스 호퍼가 릴레이 사이에 낀 나방을 발견하면서 [버그]라는 말이 생김
- 진공관
    - 존 앰브로즈는 물체를 충분히 가열하면 전자가 튀어나오는 [열전자방출]현상을 기반으로 [진공관]을 만들었다.
    - 진공관에는 [캐소드(전자가 흘러나오고들어가는 장소)]와 [히터(캐소드를 가열시키는것)]가 있다.
    - 애노드 : 캐소드에서 발생한 전자가 날아가는곳(더듬이 처럼 생김)
    - 그리드 : 전자가 애노드로 못들어가게함
    - 캐소드, 애노드, 그리드가 들어가 있는 진공관을 삼극관이라고 함 
- 트랜지스터
    - 진공관과 비슷하지만 반도체의 특별한 물질을 사용한다. 
    - 반도체 물질로 이루어진 [기판] 또는 [슬랩]위에 만들어진다.
    - 트랜지스터 그림을 그림을 실리콘 웨이퍼(뉴스에서 나오는 원 반도체형)위에 투영해서 현상하는 [광식각]이라는 과정을 통해 만들어짐.
    ```
        쌍극 접합 트랜지스터 : N형과P형의 결합으로 구성 (NPN,PNP쌍극 , P.114참조)
        필드 효과 트랜지스터 : 게이트 단자를 통해 전류를 제어 (P.114참조)
        - 게이트와 베이스는 스위치의 손잡이이며 손잡이가 올라가면 전기 흐름
        - MOSFET는 전력소모가 낮아 컴퓨터 칩으로 가장 널리 사용됨
    ```
- 집적회로
    - 잭 킬비와 로버트 노이스가 [집적회로] 발명.
    - 복잡한 시스템을 트랜지스터 하나 만드는 비용으로 절약가능
    - 칩(chip)이라고 불림

### 4. 논리 게이트
> 잭 킬비가 일하던 인스트루먼츠는 집적회로 패밀리를 발표했다.
> 이 칩들에는 논리연산을 수행하는 회로가 들어가 있는데  이 회로를 [논리게이트]라고 부른다. (간략히 [게이트]라고 부르기도함)

- 게이트 스키매틱(회로도) 기호 (p.116 참조)
- 논리 게이트에서 가장 단순한 회로는 NAND,NOR이다. (디지털 회로 설계시 가장 기본적으로 사용)
- 드모르간 법칙으로 NAND게이트를 OR게이트로 다시 그릴수 있음(P.117참조)

- 이력 현상을 활용한 잡음 내성 향상
    - 작은 하드웨어를 만들면서 잡음내성을 생각해야 한다.
    - 입력신호에 잡음이 있으면 출력신호에 [글리치(오류)]가 생기는데 이 글리치를 [이력현상]을 통해 방지할수 있다. (P.118참조)
    - 잡음 내성이 강해진다.
    - 슈미트 트리거 : 이력을 추가한 게이트,비쌈
    - 문턱값이 하나가 아니라 클러치가 발생할때마다 문턱값을 설정해 0과1을 계속 출력함으로써 클러치를 없애주는 역할을 함
- 차동 신호
    - 두개의 전송선 위에 거울어 비치듯 양방향으로 전류가 흐르는 것을[차동신호]라고한다. 
    - 차동은 서로 [반전관계]를 뜻한다.
    - 잡음이 너무 많으면 제품의 정격(정해진 규격)을 벗어나 문제가 발생할수 있는데, [공통 모드 판별비]라는 부품이 처리가능한 잡음의 양을 표시해준다.
    - 반전되는 전파신호 두개를 결합해서 잡음을 잡아주는 역할함
    - 그레이엄 벨은 [연선 케이블링]을 발명했는데, 잡음을 최대한 줄여 간섭을 피할수 있다.
    - 전차선과 전화선이 한묶음이라 잡음발생하는데, 차동신호로 잡음을 줄일수 있었다.
- 전파 지연
    - 최대 지연값과 최소 지연값을 감안해서 설계를 해야한다.
    - PLH는 0(HIGH)에서 1(LOW)로 가는 경우 걸리는 지연시간
    - PHL은 1(LOW)에서 0(HIGH)로 가는 경우 걸리는 지연시간
- 출력 유형
    - 토템폴 출력
        - 일반적인 게이트 출력을 [토템폴]이라고 부른다.
        - 스위치는 출력과 높은 논리값 1을 연결하기 때문에 [액티브 풀업]이라고 불린다. (P.123참조)
        - 토템폴은 서로 연결 못함 (음극과 양극을 서로 연결하게 되서 타버림)
    - 오픈 컬렉터 출력
        - [오픈드레인]과[오픈 컬렉터]는 여러 디바이스를 하나의 연결선으로 양방향 통신할수 있는 회로 기술을 뜻함 (P.124참조)
        - 오픈드레인과 오픈 컬렉터는 액티브 풀업이 없기 때문에 문제없이 서로 연결 가능
    - 트라이스테이트 출력
        - 오픈 컬텍터의 속도지연 문제를 해결해주는 [트라이스테이트] 출력
        - 베이스를 제어하면 0,1,hi-Z,멜트다운(녹아버림) 이라는 4가지 상태를 얻을수 있음
### 5. 게이트를 조합한 복잡한 회로
- 가산기
    - 반가산기로 는 2개의 비트가 한계이기 때문에 전가산기를 사용한다.(p.127참조)
    - 합은 이진수의 [합]이고, 합에서 올림이 발생할시 다음 비트로 올려주는 [올림]이 있다.
    - 리플 자리올림 가산기 : 아래쪽 비트로 부터 위쪽 비트로 물결처럼 전달기에 붙여진 이름(p.128참조)
    - 올림 예측 가산기 : 출력 지연을 제거할 수 있음
- 디코더
    - 인코딩된 수를 개별 비트의 집합으로 만들어줌
    - 예로 4비트의 2진수를 10가지 각기다른 출력으로 만들수있다.
    - p.130을 참조해 보면 3개의 입력에서 8개의 출력이 나오는 3:8 디코더를 볼수 있다.
- 디멀티플렉서
    - 디코더를 이용해 [디 멀티플렉서]를 만들수 있다. (보통 디먹스라 줄여 부른다.)
    - 한개의 입력을 선택해 1:4의 경우의 출력방식을 할당해줌(p.131참조)
- 실렉터
    - 출력을 먼저 선택하고 입력을 선택하는 방식 4:1
    - 토스터 기와 동일(p.133참조)
