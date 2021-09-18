---
title:  "[Android][Java] 사용자 인터페이스"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-09-17 23:14:12 

---

# 사용자 인터페이스

자바의 swing은 사용하지 않는다

- 너무 리소스를 많이 잡아먹기 때문

독자적인 사용자 인터페이스 컨트롤 사용

- 버튼, 리스트, 스크롤 바, 체크 박스, 메뉴, 대화 상자

## 뷰 그룹

다른 뷰들을 담는 컨테이너 기능.

뷰 그룹은 ViewGroup 클래스에서 상속받아 작성된다

흔히 레이이웃(layout)이라고 불리며 

- 선형 레이아웃
- 테이블 레이아웃
- 상대적 레이아웃

등이 속한다

각 레이아웃들은 정해진 정책에 따라서 뷰들을 배치한다

## 뷰

컨트롤, 위젯 이라고도 불린다

사용자 인터페이스를 구성한느 기초적인 빌딩 블록이다

버튼, 텍스트 필드, 체크박스 등이 속한다

뷰들은 View클래스를 상속받아 작성된다

# UI를 작성하는 절차

1. 뷰 그룹을 생성한다
2. 필요한 뷰를 추가한다
3. 액티비티 화면으로 설정한다

**UI는 작성법**

- xml로 사용자 인터페이스 기술
- 코드로 사용자 인터페이스 작성

# 뷰

- View  클래스는 모든 뷰들의 부모 클래스이다.
- View 클래스가 가지고 있는 필드나 메소드는 모든 뷰에서 공통적으로 사용 가능하다

## 뷰의 필드와 메소드

id

- 뷰의 식별자

뷰의 위치와 크기

|     상수     |                       설명                       |
| :----------: | :----------------------------------------------: |
| match_parent | 부모의 크기를 꽉 채운다(fill_parent도 같은 의미) |
| wrap_content |       뷰가 나타내는 내용물의 크기에 맞춘다       |
|     숫자     |              크기를 정확히 지정한다              |

![b0143083_4d00e05b37369](https://user-images.githubusercontent.com/69203345/133784415-9b6ba559-e1ed-423e-856d-59bf6b03db2f.jpg)

[출처](http://egloos.zum.com/beatin/v/1186597)

**화면에 보이기 속성**

|   상수    |  값  |                       설명                       |
| :-------: | :--: | :----------------------------------------------: |
|  visible  |  0   |          화면에 보이게 한다. 디폴트 값           |
| invisible |  1   | 표시되지 않는다. 그러나 배치에서 공간은 차지한다 |
|   gone    |  2   |                 완전히 숨겨진다                  |

**마진과 패딩**

패딩이란 뷰의 경계와 뷰 내용물 사이의 간격

마진이란 뷰 주위의 여백

### 텍스트뷰

텍스트뷰(TextView)는 화면에 간단한 텍스트를 출력하는 뷰이다. 레이블(lable)이라고도 함

```xml
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="#0000ff"
        android:text="This is a test."
        android:textColor="#ff0000"
        android:textSize="20sp"
        android:textStyle="italic"
        android:typeface="serif"
    />
```

이렇게 수정시

<img src="https://user-images.githubusercontent.com/69203345/133788580-e8143d35-b6bd-4c38-8cf9-104ceeee40e0.png" alt="image" style="zoom:67%;" />

이렇게 나온다

### 에디트 텍스트

에디트 텍스트(EditText)는 입력이 가능한 텍스트 필드이다. 텍스트 필드라고도 함

EditText는 TextView의 자식 클래스이다

TextView클래스에서 상속 받은 속성들

|          속성           |                     설명                     |
| :---------------------: | :------------------------------------------: |
|    android: autoText    |       자동으로 타이핑 오류를 교정한다        |
| android: drawableBottom |  텍스트의 아래에 표시되는 이미지 리소스이다  |
| android: drawableRight  | 텍스트의 오른쪽에 표시되는 이미지 리소스이다 |
|    android: editable    |                   편집가능                   |
|      android: text      |             표시되는 텍스트이다              |
|   android: singleLine   |             ture이면 한줄만 받음             |
|   android: inputType    |                 입력의 종류                  |
|      android: hint      |       입력 필드에 표시되는 힌트 메세지       |

inputType속성

|      inputType      |          설명          |
| :-----------------: | :--------------------: |
|        none         |    편집불가 문자열     |
|        Text         |    일반적인 문자열     |
|    textMultiLine    |   여러줄로 입력 가능   |
|  textPostalAddress  |        우편주소        |
|  textEmailAddress   |      이메일 주소       |
|    textPassword     |        패스워드        |
| textVisiblePassword | 패스워드 화면에 보인다 |
|       number        |          숫자          |
|    numberSigned     |    부호가 붙은 숫자    |
|    numberDecimal    |   소숫점이 있는 숫자   |
|        phone        |        전화번호        |
|      datetime       |          시간          |

코드 추가

```xml
    <EditText
        android:id="@+id/editTextTextPersonName"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:ems="10"
        android:hint="아이디"
        android:inputType="text" />

    <EditText
        android:id="@+id/editTextTextPassword2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:ems="10"
        android:hint="패스워드"
        android:inputType="textPassword" />

    <EditText
        android:id="@+id/editTextPhone2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:ems="10"
        android:hint="010-xxxx-xxxx"
        android:inputType="phone" />
```

결과

<img src="https://user-images.githubusercontent.com/69203345/133792746-d8e71189-fe38-4c7d-9127-8ce1710920cb.png" alt="image" style="zoom:80%;" />

### 이미지 뷰

아이콘과 같은 이미지들을 간단히 표시하는데 사용

이미지를 표시할수 있는 TextView라고 생각하면 된다

|           속성           |             설정 메소드              |                             설명                             |
| :----------------------: | :----------------------------------: | :----------------------------------------------------------: |
| android:adjustViewBounds |     setAdjustViewBounds(boolean)     | drawable의 종횡비를 유지하기 위하여 이미지의 가로, 세로를 조정 |
|  android:cropToPadding   |                                      |           true이면 패딩안에 맞추어서 이미지를 자름           |
|    android:maxHeight     |          setMaxHeight(int)           |                    이미지 뷰의 최대 높이                     |
|     android:maxWidth     |           setMaxWidth(int)           |                    이미지 뷰의 최대 넓이                     |
|    android:scaleType     |  setScaleType(ImageView.ScaleType)   | 이미지 뷰의 크기에 맞추어 어떻게 확대나 축소할 것인지 방법 선택 |
|       android:src        |        setImageResource(int)         |                         이미지 소스                          |
|       android:int        | setColorFilter(int, PorterDuff.Mode) |                       이미지 배경 색상                       |

### 버튼 

푸시버튼 위젯을 나타냄

사용자가 클릭 할 수 있는 가장 기본적인 위젯중 하나

TextView클래스를 상속받아 작성됐으므로 TextView의 모든 속성을 사용가능

코드

```xml
    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="버튼1" />

    <Button
        android:id="@+id/button2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="버튼2" />

    <ToggleButton
        android:id="@+id/toggleButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="버튼1" />
```

작성시 결과

![image](https://user-images.githubusercontent.com/69203345/133795807-4d02c8da-a1f7-46d5-8316-b4010188d89b.png)

### 레이아웃

뷰들을 화면에 배치하는 방법

종류

- LinerLayout : 자식들을 수직이나 수평으로 배치
- TableLayout : 자식들을 테이블 형태로 배치
- GridLayout : 자식들을 바둑판 모양으로 배치
- RelativeLayout : 자식들을 부모나 다른 자식에 상대적으로 배치
- ConstraintLayout : 자식들을 부모나 다른 자식 중에서 하나를 선택
- TabLayout : 탭을 이용하여 겹쳐진 자식 중에서 하나를 선택
- AbsoluteLayout : 절대 위치로 배치
- FrameLayout : 모든 자식들을 겹치게 배치

#### 선형 레이아웃

가장 기본적인 배치관리자

자식 뷰들을 수직 또는 수평으로 배치한다

|      속성       |         관련 메소드         |                       설명                        |
| :-------------: | :-------------------------: | :-----------------------------------------------: |
|   orientation   |     setOrientation(int)     |      "horizontal": 수평,"vertical": 수직배치      |
|     gravity     |       setGravity(int)       |        x축과 y축에 자식을 어떻게 배치할지         |
| baselineAligned | setBaselineAligned(boolean) | false로 설정시 자식뷰들의 기준선을 정렬 하지 않음 |

#### 가중치

선형 레이아웃의 자식 뷰들의 가중치가 각각 1,2,3 이면, 남아있는 공간의 1/6,2/6,3/6을 할당받는다

가중치를 1로 선언한 2개의 뷰들은 남아있는공간을 동일하게 차지함

 ```xml
     <EditText
         android:id="@+id/editTextTextPersonName"
         android:layout_width="match_parent"
         android:layout_height="wrap_content"
         android:ems="10"
         android:hint="To"
         android:inputType="textPersonName" />
 
     <EditText
         android:id="@+id/editTextTextPersonName2"
         android:layout_width="match_parent"
         android:layout_height="wrap_content"
         android:ems="10"
         android:hint="Subject"
         android:inputType="textPersonName" />
 
     <EditText
         android:id="@+id/editTextTextPersonName3"
         android:layout_width="match_parent"
         android:layout_height="0dp"
         android:layout_weight="1"
         android:ems="10"
         android:gravity="top"
         android:hint="Message"
         android:inputType="textPersonName" />
 
     <Button
         android:id="@+id/button"
         android:layout_width="100dp"
         android:layout_height="wrap_content"
         android:layout_gravity="right"
         android:text="Send" />
 ```

1,2번 에디트 텍스트의 가중치를 0(디폴트)

3번 에티트 텍스트의 가중치를 1

버튼의 layout_gravity 속성 right사용

결과

<img src="https://user-images.githubusercontent.com/69203345/133877760-a1df63a4-6d17-4745-bd03-2f8a26fdb36b.png" alt="image" style="zoom:80%;" />

#### 테이블 레이아웃

자식뷰 들을 테이블 형태로 배치

html에서 테이블을 표시하는 방법과 비슷

#### 상대적 레이아웃

특정한 뷰를 중심으로 상대적으로 지정하는 방법

```xml
    <TextView
        android:id="@+id/address"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:text="주소를 입력하세요" />

    <EditText
        android:id="@+id/input"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@+id/address"
        android:background="@android:drawable/editbox_background"
        android:inputType="textPersonName" />

    <Button
        android:id="@+id/cancel"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/input"
        android:layout_alignParentRight="true"
        android:layout_marginLeft="10dp"
        android:text="취소" />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_toLeftOf="@+id/cancel"
        android:layout_alignTop="@id/cancel"
        android:text="확인" />
```

결과

<img src="https://user-images.githubusercontent.com/69203345/133878909-b7510cab-2a1a-4b04-ba9d-014d93b7672b.png" alt="image" style="zoom: 80%;" />

# 코드로 UI작성

## 코드를사용

코드를 이용해서 레이아웃, 뷰들을 생성 할 수 있다.

MainActivity.java를 수정한다

```java
package com.example.ui2;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.Button;
import android.widget.LinearLayout;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
// ============ 추가 ============
        LinearLayout container = new LinearLayout(this);
        container.setOrientation(LinearLayout.VERTICAL); //선형 레이아웃 생성

        Button b1 = new Button(this);//버튼 생성
        b1.setText("첫번째 버튼");
        container.addView(b1);//생성한 버튼 화면에 추가

        Button b2 = new Button(this);
        b2.setText("두번째 버튼");
        container.addView(b2);

        setContentView(container);//만들어진 뷰 트리를 액티비티 화면으로 설정

    }
}
```

실행 화면

![image](https://user-images.githubusercontent.com/69203345/133880352-f44316ff-88c0-4f1c-9ae8-84fa34837016.png)

## XML과 코드를 둘다 사용

activity_main.xml 사용

```xml
    <Button
        android:id="@+id/button"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="첫번째 버튼" />

    <Button
        android:id="@+id/button2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="두번째 버튼" />
```

버튼2개 생성후 속성 바꿔즘

MainActivity.java 파일 수정

```java
package com.example.ui3;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.Button;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
//============= 추가 ============
        Button b1 = (Button) findViewById(R.id.button);
        b1.setText("코드로 변경도 가능");
        
        Button b2 = (Button) findViewById(R.id.button2);
        b2.setEnabled(false);
    }
}
```

실행 결과

![image](https://user-images.githubusercontent.com/69203345/133880674-c47d09d5-4085-4941-8e3f-46c022b0024c.png)

"첫번째 버튼" 이 아닌 "코드로 변경도 가능"으로 바뀌고,

두번째 버튼은 화면은 보이지만 사용은 할 수 없는 상태로 변경 된것이 보인다

## 코드로 레이아웃 속성 변경

activity_main.xml

```xml
<Button
    android:id="@+id/button"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Button" />

<Button
    android:id="@+id/button2"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Button" />
```

버튼 2개 추가 + 레이아웃에도 id 지정 해주기

MainActivity.java

```java
package com.example.layoutbycodeactivity;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.LinearLayout;

import java.util.logging.Level;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
//=================== 추가 ==================
        LinearLayout manager = (LinearLayout) findViewById(R.id.LayoutManager);
        manager.setOrientation(LinearLayout.HORIZONTAL);      
        
    }
}
```

