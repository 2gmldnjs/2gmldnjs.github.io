---
title:  "[Android][Java] 이벤트 처리"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-09-25 23:57:55
---

# 이벤트 처리

## 입력 위젯

- 버튼, 텍스트 필드, 시크 바, 체크박스, 줌 버튼, 토글 버튼 등

입력위젯의 종류

|     위젯      |                             설명                             |          관련 클래스           |
| :-----------: | :----------------------------------------------------------: | :----------------------------: |
|    Button     |           사용자가 누를수 있고 클릭가능한 푸시버튼           |             Button             |
|  Text field   |                  편집이 가능한 텍스트 필드                   | EditText, AutoCompleteTextView |
|   Checkbox    | 토글될수있는 on/off 버튼, 여러 옵션을 선택하게 하려면 체크박스를 사용 |            CheckBox            |
| Radio button  |    체크박스와 유사하지만 그룹에서 하나의 옵션만 선택 가능    |    RadioGroup, RadioButton     |
| Toggle button |             라이트 인디케이터가 있는 on/off 버튼             |          ToggleButton          |
|    Spinner    |    여러 값중에서 하나를 선택 할 수 있는 드롭 다운 리스트     |            Spinner             |
|    Pickers    | up/down 버튼이나 스와이프 제스처를 통해 값을 선택하는 대화상자 |     DatePicker, TimePicker     |

ex) 버튼의 이벤트 처리

onClick 속성을 이용해서 함수를 기입

해당되는 함수를 자바 코드로 작성

![버튼의+이벤트+처리](https://user-images.githubusercontent.com/69203345/134772440-c4a7a7d9-2344-4320-89fc-ad9934908ea8.jpg)

버튼을 클릭시 sendMessage라는 함수가 호출됨

## 안드로이드에서 이벤트 처리방법

- xml 파일에 이벤트 처리 메소드(함수)를 등록
  - 가장 쉽고 권장 되는 방법
  - 위에서 다룬예시
- 이벤트 처리 객체를 생성하여 컴포넌트(리스너)에 등록
- 뷰 클래스의 이벤트 처리 메소드를 재정의
  - 커스텀 뷰를 작성하는 경우: (예) 게임

### 리스너의 종류

|           리스너           |   콜백 메소드   |                             설명                             |
| :------------------------: | :-------------: | :----------------------------------------------------------: |
|    View.OnClickListener    |    onClick()    | 어떤 항목을 터치 하거나 항목으로 이동한후 엔터키를 눌러서 호출 |
|  View.OnLongClickListener  |  onLongClick()  |       항목을 터치해서 일정시간동안 누르고 있으면 발생        |
| View.OnFocusChangeListener | onFocusChange() |     하나의항목에서 다른 항목으로 포커스를 이동할때 호출      |
|     View.OnKeyListener     |     onKey()     |   포커스를 가지고 있는 항목위에서 눌렀다가 놓았을 때 호출    |
|    View.OnTouchListener    |    onTouch()    |          터치 이벤트로 간주되는 동작을 한 경우 호출          |

- 콜백 메소드 - 내가 호출하지 않아도 자동적으로 호출되는 메소드

### 리스너 객체를 생성하는 방법

이벤트 처리 객체를 생성하여 컴포넌트(리스너)에 등록하는 방법 3가지

- 리스너 클래스를 내부 클래스로 정의
- 리스너 클래스를 무명 클래스로 정의 ← 가장 많이 사용됨
- 리스너 인터페이스를 액티비티 클래스에 구현

ex

```java
...
public class MainActivity extends AppCompatActivity {
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Button button = (Button) findViewById(R.id.button);
        button.setOnClickListener(new OnClickListener(){
            public void onClick(View v) {
                Toast.makeText(getApplicationContext(),
                               "버튼이 눌려졌습니다", Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```

> ​       Button button = (Button) findViewById(R.id.button);

xml 상에 존재하는 버튼의 아이디를 사용해서 버튼클래스의 객체인 button 을 생성

> ​        Button button = (Button) findViewById(R.id.button);
>
> ​        button.setOnClickListener(new OnClickListener(){
>
> ​            public void onClick(View v) {
>
> ​                Toast.makeText(getApplicationContext(),
>
> ​                               "버튼이 눌려졌습니다", Toast.LENGTH_SHORT).show();
>
> ​            }
>
> ​        });

button(객체).setOnClickListener ← 무명 클래스 이벤트 처리

#### 무명 클래스

클래스 몸체는 정의되지만 이름이 없는 클래스

무명클래스는 클래스를 정의 하면서 동시에 객체 생성

### 텍스트필드

텍스트필드를 사용하면 사용자가 앱에 텍스트를 타이핑하여 입력가능

단일 라인 이거나 멀티 라인일수 있음

### 체크박스

중복허용
체크박스의 예시코드만 분석

![체크박스의+이벤트+처리](https://user-images.githubusercontent.com/69203345/134775293-088d6cb0-af13-4d81-a08d-63be2b18270c.jpg)

위 예시에서는 switch case 문을 사용, onClick 값이 동일한 경우

체크박스별로 onClick 을 다르게 설정한후 따로 함수를 설정해도 상관은 없음

>  public void onCheckboxClicked(View view)

체크돼있는 뷰에 대한 모든 정보가 view 에 들어감

> boolean checked  = ((CheckBox) view ).isChecked();

체크여부 확인

체크가 됐으면 checked 가 true

### 라디오박스

중복불가

라디오그룹안에 라디오버튼을 정의



라디오박스의 예시 코드만 분석

![라디오+버튼의+이벤트+처리](https://user-images.githubusercontent.com/69203345/134775476-28a589db-7b09-4953-bd83-41eea5251746.jpg)

토글버튼