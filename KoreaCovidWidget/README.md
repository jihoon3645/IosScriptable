위젯 : 전국 및 특정 지역 코로나19 실시간 현황과 날짜, 배터리 정보, 단축어 바로가기 버튼을 담은 위젯
===================================================================================================
## 목차
- [소개](https://github.com/sunung007/IosScriptable/blob/main/KoreaCovidWidget/README.md#소개)
- [기본 구성](https://github.com/sunung007/IosScriptable/blob/main/KoreaCovidWidget/README.md#기본-구성)
- [위젯 설치 및 적용 방법](https://github.com/sunung007/IosScriptable/blob/main/KoreaCovidWidget/README.md#위젯-설치-및-적용-방법)
- [지역, 배경, 텍스트/아이콘 색상 변경](https://github.com/sunung007/IosScriptable/blob/main/KoreaCovidWidget/README.md#설정값-변경-방법)
- [오류 대처](https://github.com/sunung007/IosScriptable/blob/main/KoreaCovidWidget/README.md#FAQ)
- [자주묻는 질문](https://github.com/sunung007/IosScriptable/blob/main/KoreaCovidWidget/README.md#FAQ)

## 소개

<img src="./image/widget_intro.jpeg" width="400"></img>

iOS의 **Scriptable** 어플의 midium size 위젯에서 작동하는 코드입니다.

## 기본 구성

위젯의 좌측부에는 다음과 같이 구성되어 있습니다.

- 날짜
  - 누르면 캘린더로 연결됩니다.
- 현재 날씨
  - 누르면 네이버 날씨로 연결됩니다.
- 배터리 용량
- 기능을 수행하는 버튼들
  - 각 버튼들은 단축어 어플과 연동되어 있습니다.
  - 단, 개인별로 단축어 이름이 다르기 때문에, 이 기능을 수행하기 전에 **코드를 직접 수정**해야 합니다.

위젯의 우측은 다음과 같이 구성되어 있습니다.
- 코로나 실시간 현황
- 전국단위 실시간 발생 현황
  - 금일 확진자 현황
  - 전일 대비 증감 수
- 특정 지역 실시간 발생 현황
  - 금일 확진자 현황
  - 전일 대비 증감
- 코로나 누적 확진자 수(정부 발표 기준)
  - 전국 누적 확진자 수
  - 전일 증가 수

을 볼 수 있습니다. 전국과 특정 1개 지역의 실시간 현황과 누적 현황을 나타냅니다. 현재 이 코드는 중간 사이즈의 위젯만 지원합니다.

----------------
## 위젯 설치 및 적용 방법

기기에 **scriptable** 어플이 설치되어 있어야 합니다. [여기](https://apps.apple.com/kr/app/scriptable/id1405459188)를 누르면 앱스토어로 이동합니다.

1. [코드 페이지](https://github.com/sunung007/IosScriptable/blob/main/KoreaCovidWidget)에 들어갑니다.   
<img src="./image/guide_1.jpeg" width="200"></img>
2. **RAW** 버튼을 눌러 전체 코드를 복사합니다.
3. scriptable 어플을 실행합니다.   
<img src="./image/guide_2.jpeg" width="200"></img>
4. `+`버튼을 눌러서 코드를 붙여넣습니다.
5. 단축어 바로가기를 위해 코드 맨 위의 부분을 수정해야합니다.   
<img src="./image/guide_3.jpeg" width="200"></img>
```
	// 위젯에 띄울 단축어 버튼들
	// itmes 안에는 ['SF symbol name', '단축어 이름']을 넣으세요.
	const buttons = {
	  number : 4,  // 버튼의 개수
	  items : [ // 버튼 내용
	    ['headphones', '음악'],
	    ['qrcode', 'QR 체크인'],
	    ['house', '집'],
	    ['dollarsign.circle', '계좌'],
	    /*...*/
	  ]} 
```

  - 넣고 싶은 버튼의 개수를 `number`에 입력합니다.   
     `number = {버튼 개수}`   
  - items의 내용에 SF symbol 이름과 기기에 저장된 단축어 이름을 입력합니다.   
     `['{SF Symbold 이름}', '{단축어 이름}'],`
  - URL scheme을 이용하기 때문에 단축어 이름은 띄어쓰기, 대/소문자 까지 정확해야 합니다.
  - SF symbol은 [여기](https://github.com/cyanzhong/sf-symbols-online)서 확인할 수 있습니다.
6. 우측 하단의 재생 버튼을 눌러서 코드를 실행시킨 후 왼쪽 상단의 `Done`을 눌러 적용합니다.   
<img src="./image/guide_4.jpeg" width="200"></img> <img src="./image/guide_5.jpeg" width="200"></img>
7. 바탕화면에 scriptable의 중간크기 위젯을 생성합니다.
8. 편집상태의 위젯을 눌러 방금 추가시킨 스크립트(코드)를 선택합니다.   
<img src="./image/guide_6.png" width="200"></img>

------------------
## 설정값 변경 방법
### 지역, 위젯 배경, 텍스트/아이콘 색 변경
코드를 편집해야 합니다.
1. 코드 16번째 줄의 `let changeSetting = false`의 값을 `true`로 변경합니다.
2. 재생버튼을 눌러 script를 실행시킵니다.
3. 실행이 끝나면 `changeSetting`을 `false`로 변경합니다.
4. Done을 눌러 저장합니다.

### 새로고침 시간 변경
코드를 편집해야 합니다.
1. 19번째 줄의 `const refreshTime = 60 * 10`의 값을 변경합니다.
2. 단위는 초입니다.
3. 기본 상태의 새로고침 시간은 10분 입니다.
4. Done을 눌러 저장합니다.

---------------
## FAQ
### 투명한 배경 만들기
mzeryck님의 배경화면 자르는 스크립트를 이용했습니다!   
필요하신 분들은 [여기](https://github.com/mzeryck/Transparent-Scriptable-Widget/blob/master/mz_transparent_widget.js)를 누르세요.

### Select script in widget configurator
위젯 편집에 들어가셔서 **script-저장한 스크립트 선택** 하면 됩니다.

### SyntaxError : ~~~
끝까지 복사 안하신 경우가 거의입니다. 코드가 너무 길어서 그래요ㅠㅠ   
코드를 **끝까지 복사** 하시고 처음부터 다시 진행해주세요.

### Alerts are not supported in a widget.
코드 16번째 줄의 `changeSetting`을 `false`로 변경하시고 스크립트 실행-적용 해주세요.

----------------------

업데이트 내용
-------------

> 20.12.29 10:07 주석

> 20.12.30 19:57
  >> - 코드 구조 변경
  >> - 위젯 설정 변경 시 `changeSetting` 값만 바꾸도록 변경
  >> - 위젯 설정 시 alert 띄워서 진행
  >> - 날씨 위젯 추가

참조
----

> 본 위젯의 현황 데이터는 [corona-live.com](http://corona-live.com)를 이용하였습니다.   
> 본 위젯의 기상 데이터는 기상청 오픈 API를 이용하였습니다.
