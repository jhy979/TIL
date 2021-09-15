# CSS
>  **Juice 라는 프로젝트**를 진행한 적이 있습니다. AWS를 활용하여 주식 데이터들을 DB에 저장하고 react를 통해 웹페이지를 구현하는 프로젝트였습니다. 그 당시 **js와 html로만 웹 페이지를 제작**하고  CSS의 지식은 거의 밑바닥인 상태로 진행했었습니다. .css파일을 안쓰고 .html파일의 html태그 안에서 그냥 주먹구구식으로 스타일을 작성했었네요. bootstrap만을 이용하여 페이지를 꾸며 제가 원하는 모습대로 안나온 기억이 있습니다.<br><br> 그 때의 아쉬움 때문에 이렇게 CSS를 다시 공부하게 되었습니다. <br><br>**저만의 언어로 CSS를 정리해보았습니다.**
## 1. CSS의 개념
- 기본적인 HTML 구조를 스타일을 추가할 수 있어요. 
```CSS
div {
  font-size : 50px;
  color : blue;
  text-decoration : underline;
  margin : 20px;
}
```
- div라는 태그를 { } 안에서 스타일링 해주는 거예요.
- 이 div는 특정 요소를 선택하는 ___선택자___ 라고합니다.
> 선택자 { 속성 : 값 } ;
## 2. 선언 방식
### 2-1) 내장 방식
- 별도의 css 파일 없이 html 안에서 <style> 태그 안에서 사용합니다.
- 하지만.. css html js 서로 파일을 분리하는 것이 유지 보수 측면에서 좋겠죠? 권장하지 않아요.
### 2-2) 인라인 방식
```html
<div style = "color" : red;> </div>
```
- 편리해보이지만 CSS 우선순위 개념에서 인라인 방식이 너무 우선적입니다.
- 너무 지나치게 우선해서 덮어써가며 수정하고 싶어도 수정이 안되는 경우도 있어요. (유지보수가 힘들 수 있어요.)
### 2-3) 링크 방식 (병렬 방식)
```html
<link rel="stylesheet" href="./css/main.css">
```
- 링크를 통해 외부 css파일을 링크하는 방식입니다.
### 2-4) import 방식 (직렬 방식)
- html 내부에서는 👇👇👇
```html
<link rel="stylesheet" href="./css/main.css">
```
- css 내부에서는 👇👇👇 아래처럼 직렬로 연결합니다.
```css
@import url("./box.css"); // 또 다른 css 파일의 경로
```
- css가 또 다른 css파일을 부르는 구조입니다.
- main.css가 html에 연결이 되어 main.css가 box.css를 import 하기 전까지는 box.css는 html에 적용이 안 됩니다. (연결이 지연될 수 있어요.)
  
## 3. CSS 선택자
### 3-1) 기본 선택자
> 전체 선택자
```css
* {
  color : red;  
}
  ```
  - 모든 요소를 선택합니다.
  > 태그 선택자
  ```css
   li {
      color : red;
  }
  ```
  - 특정 태그 이름을 기준으로 선택합니다. 가장 기본적이죠?
  > 클래스 선택자 . 
  ```css
  .orange {
    color : red;
  }
  ```
  ```html
  <li class="orange"> 오렌지 </li>
  <div class="orange"> 오렌지 </div>
  ```
  - .이 꼭 필요합니다. 
  > 아이디 선택자 #
   ```css
  #orange {
    color : red;
  }
  ```
  ```html
  <li id="orange"> 오렌지 </li>
  ```
### 3-2) 복합 선택자
  - 기본 선택자를 조합해서 사용하는 겁니다.
  > 일치 선택자 
  - 선택자 A 와 선택자 B를 동시에 만족하는 요소 선택
  ```css
  span.orange {
    color : red;
  }
  ```
  - 태그는 span, 클래스는 orange 인 경우에 스타일 적용해!
  
  > 자식 선택자 >
  ```css
  ul > .orange {
    color : red;
  }
  ```
  ```html
  <ul>
    <li> 사과 </li>
    <li class = "orange"> 오렌지 </li>
  </ul>  
  ```
  - 부모요소가 ul인 자식 중에서 class가 oragne인 친구들만 스타일 적용해!
  
  > 하위 선택자 (띄어쓰기)
  ```css
  div .orange {
    color : red;
  }
  ```
  - 공백문자로 구분합니다.
  - div라는 태그 선택자 + class가 orange인 친구를 찾자.
  - 하위 선택자를 더 많이 사용합니다.
  
  > 인접 형제 선택자
  ```css
  .orange + li {
    color : red; 
  }
  ```
  ```html
  <ul>
    <li> 사과 </li>
    <li class = "orange"> 오렌지 </li>
    <li> 망고 </li>
    <li> 수박 </li>
  </ul>  
  ```
  - 같은 부모를 공유하는 li 태그 중 바로 **다음 형제 하나만** 골라요.
  - 신기하게도 오렌지가 아니라 망고가 선택되게 됩니다.
  
  > 일반 형제 선택자
  ```css
  .orange ~ li {
    color : red; 
  }
  ```
  ```html
  <ul>
    <li> 사과 </li>
    <li class = "orange"> 오렌지 </li>
    <li> 망고 </li>
    <li> 수박 </li>
  </ul>  
  ```
  - 같은 부모를 공유하는 li 태그 중 바로 **다음 형제 모두**를 골라요.
  - 망고와 수박이 선택됩니다.
### 3-3) 가상 클래스 선택자
  > Hover
  - **마우스 올리면 변화**를 만들 수 있어요.
  ```css
  a:hober {
    color : red;
  }
  ```
  - 마우스 커서를 a 태그 위에 올리면 빨간색으로 변하는 예제입니다.
  
  > Active
  - **마우스를 클릭하고 있는 동안 변화**를 만들 수 있어요.
  ```css
  a:active {
    color : red;
  }
  ```
  
  > Focus
  - 포커스는 가능한 요소가 일반적으로 input 요소입니다.
  - 마우스 눌렀을 때 켜집니다.
  ```css
  input:focus {
    background-color : orange;
  }
  ```
  - input 박스를 누르면 변화가 일어나요.
  - focus가 가능한 요소는 select, text area, input ... 정도가 있어요.
  - div같이 안되는 요소에는 html에서 tabindex="-1" 속성을 주면 되긴하는데 권장하지 않아요.
  
  > First Child 
  - 형제 요소 중 선택자가 첫째라면 선택합니다.
  ```css
  .fruits span:first-child{
    color : red;
  }
  ```
  - first-child 👉 형제 요소 중 첫째만 선택할건데
  - span 👉 span 태그를 가지는 친구여야하고
  - .fruit 띄어쓰기👉 fruit 클래스를 가지는 요소의 후손이여야해.
  
  > Last Child 
  - first-child라 똑같지만 막내를 찾는 겁니다.
  
  > Nth Child 
  - 비슷합니다.
  ```css
  .fruits *:nth-child(2){
    color : red;
  }
  ```
  👆👆 둘째를 찾을 건데 어떤 태그든 상관없이 fruits class의 후손이면 됨.
   ```css
  .fruits *:nth-child(2n){
    color : red;
  }
  ```
  👆👆 2번째, 4번째, ... 친구들을 찾을 겁니다.
  
  > 부정 선택자
  - Not 사용
  ```css
  .fruits *:note(span){
    color :red;
  }
  ```
  👆👆 span 제외하고 fruits class 내 모든 태그들을 선택합니다.
  
  ### 3-4) 가상 요소 선택자
  > Before
  - 콜론이 두 개!
  - before라는 가상의 요소를 만들어서 class 가 덮은 요소 앞에 삽입하는 선택자입니다.
  ```css
  .box::before {
    content:"앞!";
  }
  ```
  ```html
  <div class="box">
    뒤!
  </div>
  ```
  👉 출력이 **뒤!** 가 아니라** 앞! 뒤!** 로나옵니다.
  
  > After
  - 반대 개념이겠죠?
  ```css
  .box::after{
    content: "";
    display: block;
    width :30px;
    height :30px;
    background :royalblue;
  }
  ```
  - content는 필수로 써야합니다.
  - inline 방식이라 width,hegiht,background가 적용이 안됩니다.
  👉 ```css display: block; ```   속성을 추가하면 적용이 됩니다.
  
  ### 3-5) 속성 선택자
  > 속성만으로 찾기
  ```css
  [disabled] {
    color : red;
  }
  ```
  - disabled 라는 속성을 가진 태그들을 선택합니다.
   ```css
  [type] {
    color : red;
  }
  ```
  - type 이라는 속성을 가진 태그들을 선택합니다.
  > 속성= "값" 
   [type="password"] {
    color : red;
  }
  
  
  ❗️ 태그 없이도 속성,값으로 스타일을 적용시킬 태그들을찾을 수 있어요.
  
  
  ## 4. 스타일 상속
  - class에 스타일을 적용하면 class 하위 요소까지 상속되어 적용됩니다.
  ❗️ **글자/문자 관련 속성들이 대부분 상속됩니다.**<br>
  ### 4-1) 강제 상속 
  - css에서 attribute의 값을 inherit로 주면 됩니다.
  - inherit을 주면 원래 안되는 width, height, .... 같은 속성들도 부모의 것을 그대로 가져 옵니다.
  👇👇 부모 값이 바뀌면 따라서 바뀌어요.
  
  ```css
  .parent {
  width: 300px;
  height :400px;
  background-color:orange;
  }
  .child {
    width:100px;
    height: inherit;
    background-color : orange;
  }
  ```
  
  ## 5. 선택자 우선순위
  - 어떤 CSS 속성을 먼저 적용을 해줘야할까요?
  1. 점수 높은 선언부터!
  2. 점수 같으면 마지막에 해석된 선언이 우선!<br>

❗️❗️❗️ 우선순위 파악이 생각보다 어렵습니다!
|속성|점수|코드|
|:---:|:---:|:---|
|!important|99999999점| ```css color : red !important ``` 이거도 적당히 씁시다. 초보들만 많이 써요.
|직접 명시 (inline 선언 방식)|1000점|html 내부 선언 (피하는 게 좋아요 우선순위 너무 높아요 ㅠㅠ)|
|ID 선택자|100점|```css #color_yellow { ... }  ```|
|class 선택자|10점|```css .div { ... } ```|
|태그 선택자|1점|```css div { ...} ```|
|전체 선택자|0점|*|
|상속|0점|```css body {...} ```|
<br>
  
![image](https://user-images.githubusercontent.com/32920566/119309432-43ec8100-bca9-11eb-9d66-96ad48355c65.png)
  
  
  ## 6. 속성
  |제어 가능한 속성|구현|
  |:--:|:--|
  |박스|가로세로 너비, 내부여백 가진 박스|
  |글꼴, 문자|크기,두께|
  |배경|배경 색상,이미지|
  |배치|요소의 위치 조정|
  |플렉스(정렬)|hmtl은 기본적으로 수직이지만, 수평 정렬 시 사용|
  |전환|요소의 전과 후 상태를 애니메이션 처리|
  |변환|요소를 회전, 이동, 크기 조절|
  |띄움|요소를 공중으로 띄움(요소 주변으로 문자가 흐르도록 - 마치 신문기사에서 이미지 옆 글씨)|
  |애니메이션|전환보다 더 복잡한 애니메이션|
  |그리드|엑셀처럼 행과 열의 레이아웃을 만들 수 있음|
  |다단|한컴에서의 단 나누기|
  |필터|이미지 필터|
  
  ### 6-1) width, height
  
 👉 기본값 : auto <br>
 👉 단위 : px, em, vw 등
  
  * 인라인 요소 (eg. span) : 가로 요소가 최대한 줄어들도록 하고 width, height 같은 레이아웃 작업은 불가능합니다. (이건 글자를 처리하기 위한 거예요!)<br>
  * 블록 요소 (eg. div) : 가로 길이가 최대가 되도록
  * max-width, max-height<br>
  👉 최대 너비 제한<br>
  👉 기본값 : none <br>
  👉 단위 : p, em, vw 등<br>
  * min-width, min-height<br>
  👉 최대 너비 제한<br>
  👉 기본값 : 0 <br>
  👉 단위 : p, em, vw 등<br>
  
  |단위|내용|
  |:---:|:---|
  |em|해당 클래스에서의 글자 크기 == 1em|
  |rem|root 기준의 글자 크기 == 1rem|
  |vw|viewport의 가로|
  |vh|viewport의 세로|
  
  
  ❓ 0 px  0vw 뭐가 더 클까요? <br>
  ❗️0은 다 같으므로 단위를 붙이지 마세요!<br>
  
  ### 6-2) margin
  - 외부 여백 <br>
 👉 기본값 : 0 <br>
 👉 지정가능값 : auto (가운데 정렬입니다)<br>
 👉 단위 : px, em, vw 등
  ```css
    margin-bottom: 20px; /* 아래만 */
    margin : 10px 20px; /* 위아래 10px 좌우 20px */
    margin : 10px 20px 30px; /* 위 10px 좌우 20px 아래 40px */
    margin : 10px 20px 30px 40px; /* 시계방향으로 */
    margin : -20px 10px /* 음수로 두면 요소들이 겹쳐짐 */
  ```
  
   ### 6-3) padding
  
  - 내부 여백<br>
 👉 기본값 : 0 <br>
 👉 단위 : px, em, vw 등
  - margin 과 같은 순서로 값을 여러개 줄 수 있어요.
  
   ### 6-4) border 
  - 순서대로 선-두께, 선-종류, 선-색상 <br>
 👉 기본값 : black <br>
  
  ``` css
    border : 10px solid orange;
  ```
  1. border-width : medium thin thick 존재하지만 숫자로 씁시다. 위의 10px 처럼 숫자로! <br>
  2. border-style : solid (실선) , dashed (파선), dotted (점선), ... <br>
  3. border-color : 기본 black <br>
  👉 색상은 색상이름(Black), Hex 색상코드 (#FFFFFF) RGB - rgb(255,255,255), RGBA - rgba(0,0,0,0.5)로 표현할 수 있어요. <br>
  👉 border-top ,buttom, right, left 도 존재합니다. <br>
  
   ### 6-5) border-radius 
  - border를 둥굴게
 👉 기본값 : 0 <br>
  ```css
    border-radius : 10px; /* 전체를 둥글게 */ 
    border-radius : 0 10px 0 0; /* 오른쪽 상단만 둥글게 */
  ```
   ### 6-5) box-sizing
  - 요소의 크기 계산 기준을 지정 <br>
 👉 기본값 : content-box / 요소의 내용만으로 크기를 계산 <br> 
 👉 입력 가능값 : border-box / 요소 내용 + padding + border 를 다 합쳐서 크기를 계산<br>
  
  ```css 
      tem:first-child {
        border: 4px solid red; /* 경계선 추가하면 원래 요소가 더 커짐 */
        padding : 20px; /* 내부 패딩하면 요소가 더 커짐 */
        box-sizing : border-box; /* 하지만 이때 border-box하면 원래 크기를 유지하면서 경계선과 padding을 진행함! */
    }
  ```
  
   ### 6-6) overflow
  - 요소의 크기 이상으로 내용이 넘치면 넘친걸 어떻게 보여줄지 설정해요.
 👉 기본값 : visible / 넘쳐도 보여주세요 <br> 
 👉 입력 가능값 : hidden, scroll, auto / 이름만 봐도 느낌 오시죠?<br>
  ![image](https://user-images.githubusercontent.com/32920566/120620141-a27ae180-c497-11eb-86ac-a55fff2e816f.png)<br>
  ※ scroll은 가로 세로 축 무조건 만들어요 ㅠㅠ 그래서 그냥 auto로 자동적으로 스크롤바를 만들어주는게 일반적이예요<br>
  - overflow-x : x축 넘치는 부분만 체크해요
  - overflow-y : y축 넘치는 부분만 체크해요
  
  
 ### 6-7) display
  - 화면 출력을 어떻게 보여줄지 결정해요.
  
  
  |요소|설명|
  |---|---|
  |block|상자 요소|
  |inline|글자 요소|
  |inline-block|기본적으로 글자 + 상자 요소(가로 세로 지정이 가능해요)|
  |flex|플렉스 박스 (1차원 레이아웃, 축 1개)|
  |grid|그리드 (2차원 레이아웃, 축 2개)|
  |none|보여짐 특성 없어요, 화면에서 사라져|
  |기타|table, table-row, table-cell|
  ```css
  span{
      width : 120px;
      height : 30px;
      background-color: royalblue;
      color : white;
      display : block;
  }
  ```
  - 위처럼 inline값인 글씨를 block으로 만들어 가로, 세로 길이를 줄 수 있어요.
  
  ### 6-8) opacity
  - 요소의 투명도를 결정합니다.
 👉 기본값 :1 / 완전 불투명 <br> 
 👉 입력 가능값: 0~1 / 조절하세용<br>
  
  
  ### 6-9) 글꼴
  
  
  |속성|기능|구체적 내용|
  |:---:|:---:|:---|
  |font-size|글꼴 크기|기본적으로 16px|
  |font-weight|두께|700(bold), normal(400) 100~900으로 조절 가능합니다.|
  |font-style|글꼴 기울임|italic|
  |font-family|글꼴|글꼴1,글꼴2..... 글꼴계열 : 여러 후보 작성 가능, 앞의 후보부터 시도해보고 안되면 글꼴계열을 사용합니다. (글꼴 이름에 띄어쓰기 있으면 ""로 묶어주세요 아니면 다 ""로 묶는 습관 들여도 괜찮아요)<br> sans-serif : 고딕체 계열로 웹에서 대부분 씁니다. 따라서 글꼴계열로 작성하세요. |
  |line-weight|상하 장평|기본적으로 normal(1) eg) 1.4는 글꼴 크기의 1.4배가 높이가 됩니다. 뭔가 상하좌우 여백을 맞춰 정렬하려는 느낌이 있어요.|
  |text-decoration|문자 장식(선 긋기)|none, underline, overline, line-through|
  |text-align|정렬|left,right,center,justify(양쪽 정렬)|
  |color|글 생삭|rgb(0,0,0)이 기본값
  |text-indent|들여쓰기,내어쓰기|50px, -50px|
  
  
  ### 6-10) 배경
  ```css
    div {
      width : 200px;
  
      height : 100px;
  
      background-color : orange; /*이미지 색상 👉기본 transparent*/ 
  
      background-image : url("경로"); /*배경 이미지, 안전하게 따옴표를 써줍시다.*/
  
      background-size : 200px; /*이미지 가로 세로 크기 , 가로 세로 둘 다 작성할 수 있지만 가로만 쓰면 비율 조절 알아서 해줘요.
                                👉기본 : auto  가능값: cover(더 넓은범위에 맞춰서 짤림)contain(더 작은거에 맞춰서 안짤림), 단위 */
  
      background-repeat : no-repeat; /*기본적으로 이미지가 요소 크기에 맞추어 반복되어 나오므로 그걸 방지
                                       👉repeat, no-repeat, repeat-x, repeat-y사용 가능*/
  
      background-position : top right; /*이미지를 요소에 맞추어 정렬
                                        👉기본 : 0% 0%   방향 : top,bottom,center,right,left   단위 : px,em,rem*/
  
      background-position : 100px 30px; /*단위로도 사용가능*/
  
      background=attachment : /*배경 이미지 스크롤 특성 지정
                               👉기본 :scroll 가능값 : fixed(스크롤은 움직이는데 이미지는 가만히 있어요. 뷰포트에 고정) */
    }
  ```

   ### 6-11) 배치
  - 요소의 위치는 반드시 반드시 **어떠한 기준을 잡고 설정해야 해요!**  
  
  
  |속성|기능|구체적 내용|
  |:---:|:---:|:---|
  |position|요소의 위치를 지정|기본 : static / 가능값 : relative(요소 자신 기준), absolute(부모 요소 기준), fixed(뷰포트 기준), sticky(스크롤 영역 기준)|
  |top bottom left right|위치 지정 |기본 : auto, 가능값 : 양수 음수|
  
  ❗️❗️  position : relavtive를 이용하는 배치는 거의 사용하지 않아요. 대부분 absolute 써요. 다른 요소들의 위치가 혼동이 올 수 있기 때문이예요.<br>
  - position을 쓰면 동급 친구들과의 상호작용이 유지됩니다. absolute를 쓰면 동급 친구들과의 상호작용이 무너집니다.
  - position : absolute를 쓰려면 위치상 부모 요소를 지정해줘야 해요. 따라서 구조 상에서 부모한테 position: relative를 써줘야해요. ( position : relavtive 는 대부분 이 때만 사용됩니다.)
  - 개념이 헷갈릴 수 있어요. 부모를 계속 찾아간다고 생각하세요. 부모를 찾아갔는데 그 부모가 position : 값으로 지정이 되어있다면 사용가능하겠죠?<br>
  ※ absolute(부모 요소 기준), fixed(뷰포트 기준)를 사용하면 display :block이 기본적으로 적용됩니다.<br><br>
  ❗️❗️ 요소 쌓임 순서
  - 어떤 요소가 더 위에 보일지 결정하는 방식입니다.
  1. 요소에 position 속성이 있으면 더 위에 쌓여요. 
  2. z-index 속성의 숫자가 높을수록 위에 쌓여요.
  3. HTML의 구조로 볼 때 나중에 써질수록 위에 쌓여요.
  👇👇👇 아래 예시로 확인해봅시당.
  ```css
  .container .item:nth-child(1){
  width : 100px;
  height : 100px;
  position : relative;
  z-index : 1;         /*기본 0 이고 -1까지도 사용합니다. 귀찮다고 999 입력하면 관리가 어려워요! 코딩할때부터 잘 관리해서 써주세요.*/
}
.container .item:nth-child(2){
  width : 100px;
  height : 100px;
  position : absolute;
  top : 50px;
  left: 50px;
  z-index : 2; 
  
}
.container .item:nth-child(3){
  width : 100px;
  height : 100px;
  z-index : 3;
}
```
  ![image](https://user-images.githubusercontent.com/32920566/120648810-03fe7880-c4b7-11eb-8642-e91860a89b20.png)
<br><br>
### 6-12) 정렬 (flex)
  - 수평, 수직 정렬을 위해 사용합니다.
  - 부모 요소에 ``` dispaly : flex; ``` 주면 child들이 수평정렬 됩니다. 그러면, 부모를 flex container라고 부르고 child들을  flex items라고 부릅니다.
  ```css
    body {
      display : flex; /* inline-flex, inline, block을 넣을 수 있어요. */
    }
  ```
  -
  
  |부모요소 속성|기능|자세히|
  |:---:|:---:|:---|
  |flex-direction|주축 설정|``` 기본:row(수평), row-reverse, column(수직), column-reverse ```|
  |justify-content|주축의 정렬 방법(수평정렬, 가로정렬)|```기본:flex-start 가능값:flex-end,center```|
  |align-content|교차 축의 **여러 줄** 정렬 방법(수직정렬 느낌)|```기본:stretch 가능값:flex-start,flex-end,center```<br>stretch는 부모 container를 꽉 채우면서 정렬 그니깐 쭉 늘인다는거죠, flex-start는 child들이 다닥다닥 붙게 모두 start를 기준으로 정렬합니다.|
  |align-items|**한 줄**의 수직 정렬|```기본:stretch  가능값:flex-start,flex-end,center,baseline(문자 기준선) ``` |

  
  |자식요소 속성|기능|자세히|
  |:---:|:---:|:---|
  |flex-wrap|자식요소 줄바꿀까 말까|``` 기본:no-wrap, wrap``` no-wrap은 한줄에서 다하려고해서 찌그러지고 wrap은 넘치면 줄바꿈해줘요|
  |flex-grow|각 child가 가로로 늘어나는 비율|```기본:0  가능값:1, ...```|
  |flex-shrink|가로로 줄어드는 비율|```기본:1  가능값: 감소비율```  0으로 두면 parent 너비가 child 너비보다 작아도 child는 줄어들지 않아요.|
  |flex-basis|flex-grow를 위한 기준,기본 너비|```기본:auto(content(글자) 너비)  가능값: 0 ``` 0으로 설정하면 눈으로 봤을 때 레이아웃이 정말 제가 원하는 기준만큼 나뉩니다.|
  |order|flex item의 순서|```기본:0 (순서없음) 가능값 : 숫자``` 숫자가 작을수록 먼저 나와요. html구조 안바꿔도 원하는대로 출력할 수 있어요.|
  
  
  ![image](https://user-images.githubusercontent.com/32920566/120892266-66d34980-c648-11eb-80af-ce9fa05f8378.png)<br><br>
  ![image](https://user-images.githubusercontent.com/32920566/120892270-6dfa5780-c648-11eb-833d-516c6809bc9f.png)<br><br>
  👉 flex를 가로라고 생각하세요 align을 세로라고 생각하세요. 여러 줄이면 align-content 한 줄이면 align-items 사용하면 됩니다.오키??<br>
  
   ### 6-13) 전환
  - 요소의 전 후 변환 상태를 자연스럽게 시간에 걸쳐 바뀌도록 하는 것을 전환 효과라고 합니다.
  
  |속성|기능|자세히|
  |---|---|---|
  |transition|전환이 지속되는 시간|필수로 써야해요.|
  |transition-property|전환 효과를 사용할 이름을 명시|```기본:all  가능값: 속성이름``` 가로너비만 영향을 받게하고 싶으면 ```transition : width 1s; ``` 이런식으로 작성| 
  |transition-duration|지속 시간을 설정||
  |transition-timing-function|타이밍 조절, 전환의 완급조절이랄까?|```기본:ease(느빠느) 가능:linear(일정),ease-in(느빠),ease-out(빠느),ease-in-out(느빠느),cubic-bezier(n,n,n,n)- 사용자 직접 정의```  easying 함수에 대한 이해가 중요하기 때문에 easying functions mdn 검색해보세요.|
  |transition-delay|대기시간|```기본:0 ```|
  
  ```css
  div {
    width:100px;
    height:100px;
    background-color:royalblue; 
    transition : 
      background-color 3s 1s, /* 따로따로 속성에 따른 전환효과 줄 수 있구요*/
      width .5s 1s            /*앞의 초는 duration이고 뒤의 초는 대기시간이예요*/
    ;
}
  ```
  
  ### 6-14) 변환
  - 뭔가 그래픽스 시간에 배웠던 느낌이네요 (눈좌표계, 세상좌표계... 이런거 배우면서 transform 행렬 수식도 많이 봤었는데.. 여튼)
  > transform : 변환함수1 변환함수2 변환함수3 ...;<br>
  👉 원근법, 이동, 크기, 회전, 기울임...
  
  #### 2D 변홤함수
  
  |변환함수|기능|
  |---|---|
  |translate(x,y)|이동|
  |translateX(x)|x축이동|
  |translateY(y)|y축이동|
  |scale(x,y)|크기|
  |rotate(45deg)|회전|
  |skewX(x)|x축 기울임|
  |skewY(y)|y축 기울임|
  
   👉 matrix(n,n,n,n,n) : 2차원 변환효과를 모두 나타낼 수 있는데, 편하게 위의 함수들로 작성합시다. <br>
  
  #### 3D 변홤함수
  
  |변환함수|기능|
  |---|---|
  |perspective(n)|원근법|
  |rotateX(x)|x축 기준 회전|
  |rotateY(y)|y축 기준 회전|
  
   👉 matrix3d(n,n,n,n,n,......,n) : 3차원 변환효과를 모두 나타낼 수 있는데, 편하게 위의 함수들로 작성합시다.(총 16개 작성해야하는데 좀;; 아니죠?) <br>
  
  ```css
  .container .item{
        width:100px;
        height: 100px;
        background-color: orange;
        transform : rotate(45deg) translate(40px,40px) scale(1.5) perspective(200px) rotateX(45deg) ; 
  }
  ```
  
   #### 속성
  1. ```perspective : 500px;```  👉 아래 설명 / 부모 기준 원근법
  2. ```backface-visibility : hidden ```  👉 기본:visible / 화면에서 뒷면은 안 보이게 할 수 있어요.
  3. 
  ❗️❗️❗️ perspective 주의점 있어요<br>
  - ```perspective :600px``` 속성 👉 관찰 대상의 **부모**에게 적용되므로 부모 요소 안에서 선언해야해요. / 기준점 : perspective-origin
  - ``` transform : perspective(600px) ``` 변환함수 👉 관찰 대상에게 적용 / 기준점 : transform-origin 
  
