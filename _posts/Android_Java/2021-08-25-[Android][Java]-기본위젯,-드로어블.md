---

title:  "[Android][Java] 기본위젯, 드로어블"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-08-25 23:55:55 //
---

시작하기 전에 

뷰 - 화면에 보이는 모든것들 (레이아웃 포함)

# TextView 속성

새 프로젝트 empty activity 로 시작

linearlayout(vertical)로 변경

팔레트에서 textview 끌어 넣고 textview의 text속성 변경

<img src="https://user-images.githubusercontent.com/69203345/130739455-de8cbc56-9e2c-453d-a81f-ffb072fd5fb8.png" alt="image" style="zoom:67%;" />

res 폴더 밑의 strings.xml을 이용해 변경

strings.xml에 코드 추가

```xml
    <string name="myname">마이크</string>
```

이후 textview의 text속성을 @string/myname 로 변경

여기서 myname은 변수명 이라고 생각하면 편함, 둘이 맞춰 주기만 하자

![image](https://user-images.githubusercontent.com/69203345/130740050-5961dd76-2e52-45f1-8680-0f8d010d029e.png)

<img src="https://user-images.githubusercontent.com/69203345/130739946-6841e871-69e4-4174-9fab-4dd8ec6035bd.png" alt="image" style="zoom:67%;" />

strings.xml 에 글자를 더 늘린후 maxLines 속성값을 1로 지정

maxLine 속성 = 택스트가 보이는 최대 줄수

lineSpacingExtra 속성 = 줄간격 

# 체크박스, 라디오 버튼

아래에 버튼,체크박스버튼 추가

<img src="https://user-images.githubusercontent.com/69203345/130742597-b466f907-e881-4f86-bbcd-48eb589d2035.png" alt="image" style="zoom:67%;" />

버튼에도 onClick을 제외하면 텍스트뷰와 같은 속성이다

라디오 버튼도 추가해보자

우선 라디오 그룹을 넣고

안에 라디오 버튼 추가

![image](https://user-images.githubusercontent.com/69203345/130743221-c528fc08-9134-4694-8eb7-1ae9fbb33a5e.png)

라디오 그룹의 속성을 아래와 같아 바꿔주면

|     속성      |      값      |
| :-----------: | :----------: |
| layout_height | wrap_content |
|  orientation  |  horizontal  |

아마 라디오 버튼이 하나만 보일텐데

|     속성     |      값      |
| :----------: | :----------: |
| layout_width | wrap_content |

변경 하자(다 해주자 그룹도)

![image](https://user-images.githubusercontent.com/69203345/130744488-d823431c-6ad4-4e92-9bd3-af61af39f5b5.png)

이렇게 변한다

# 입력상자

Plain Text

input type속성의 설정에 따라 보이는 키패드 유형이 달라짐

![image](https://user-images.githubusercontent.com/69203345/130746170-4cc3cce0-2fa5-468c-8724-580769ea1c4c.png)

위에부터 inputType을

text

number 로 변경 한 후 실행 결과이고

마지막은 팔레트에서 password를 가져와서 사용할 결과임

# 이미지뷰

srcCompat으로 이미지 변경 가능

layout_width,height 의 값에 자동으로 사이즈 조절이 됨

scaleType의 속성에 따라서 어떻게 보이는지 달라짐

![image](https://user-images.githubusercontent.com/69203345/130750554-8afa1082-f9e7-46b1-9431-31b7446142f4.png)

scaleType속성이 center 일때

# 드로어블

## 상태 드로어블

버튼의 상태에 따라 변화

버튼의 background 속성을 변경

![image](https://user-images.githubusercontent.com/69203345/130754613-2a8d9233-f410-49b5-bc95-8eb2e3359e5d.png)

res폴더안 drawble 폴더에서 new resource file 을 눌러서 xml파일 만들기

```xml
    <item android:state_pressed="true" android:drawable="@drawable/finger_pressed"></item>
    <item android:drawable="@drawable/finger"></item>
```

추가후 

다시 버튼에서 만들어놓은 xml 파일명과같은 이미지로 바꿔주면 에뮬레이터에서 클릭되는것을 볼 수 있다

## 쉐이프 드로어블

res폴더안 drawble 폴더에서 new resource file 을 눌러서 xml파일 만들기

select → shape 로 변경 

rectangle = 사각형

stroke = 테두리선 

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" android:shape="rectangle">
    <size android:width="200dp" android:height="120dp"/>
    <stroke android:width="1dp" android:color="#0000FF"/>
    <solid android:color="#aaddff"/>
    <padding android:bottom="1dp"/>
</shape>
```

<img src="https://user-images.githubusercontent.com/69203345/130766994-fcdefd86-7a63-4149-8e06-39456711cebc.png" alt="image" style="zoom:80%;" />

혹시 배경이 안바뀐다면 아래대로 해보자

- theme.xml 파일의 style태그의 parent 속성을 MaterialComponent에서 AppCompat으로 변경

### 그라데이션 넣기

xml 파일 생성

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" >
    <gradient
        android:startColor="#7288D8"
        android:centerColor="#3250B4"
        android:endColor="#254095"
        android:angle="90"
        android:centerY="0.5"/>
    <corners android:radius="2dp"/>
</shape>
```

gradient = 그라데이션

background 속성변경

![image](https://user-images.githubusercontent.com/69203345/130767823-b3008b62-88be-4f7d-b2e3-e57fd33b2acb.png)

### border 만들기

xml파일 생성

```xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item>
        <shape android:shape="rectangle">
            <stroke android:width="1dp" android:color="#BE55DA"/>
            <solid android:color="#00000000"/>
            <size android:width="200dp" android:height="100dp"/>
        </shape>
    </item>
    <item android:top="1dp" android:bottom="1dp"
        android:right="1dp" android:left="1dp">
        <shape android:shape="rectangle">
            <stroke android:width="1dp" android:color="#ff55da"/>
            <solid android:color="#00000000"/>
        </shape>
    </item>
</layer-list>
```

#00000000 = 투명

<img src="https://user-images.githubusercontent.com/69203345/130769538-959dc64e-99e8-4ca4-a975-ca40e9ab405c.png" alt="image" style="zoom:67%;" />

투명한 상태에서 border가 잘 들어가있는 버튼을 볼 수있음

# 이벤트

## 터치

새 프로젝트, 리니어 레이아웃 vertical

팔레트에서 View 집어넣기

![image](https://user-images.githubusercontent.com/69203345/130784580-b50a9daf-93ca-46f8-b7bc-a1392ec5090d.png)

textView를 제외한 view, view2, scrollview는 모두

layout_height 0dp 로 바꿔주고, layout_weight 1 로 설정

<img src="https://user-images.githubusercontent.com/69203345/130784852-f4f942cd-348c-4d73-aba8-505facf33cb4.png" alt="image" style="zoom:67%;" />

3분할 됨

java 소스코드 입력으로 기능 추가

```java
package com.example.myevent;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.MotionEvent;
import android.view.View;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    TextView textView;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);//textView라는 아이디른 가진 뷰 찾기

        View view = findViewById(R.id.view);//첫번째 뷰
        view.setOnTouchListener(new View.OnTouchListener() {
            @Override
            public boolean onTouch(View view, MotionEvent motionEvent) {//터치 이벤트
                //손으로 누르거나 움직이거나 떼면 이 함수 호출됨
                int action= motionEvent.getAction();//호출 됐을때 상태 저장(눌림, 움직임 같은)

                float curX = motionEvent.getX();
                float curY = motionEvent.getY();

                if(action == MotionEvent.ACTION_DOWN){ //손가락이 눌린 상태
                    println("손가락 눌림 : "+curX+" , "+curY);
                }else if (action == MotionEvent.ACTION_MOVE){
                    println("손가락 움직임 : "+curX+" , "+curY);
                }else if (action == MotionEvent.ACTION_UP){
                    println("손가락 뗌 : "+curX+" , "+curY);
                }
                return true;
            }
        });

    }
    public void println(String data){
        textView.append(data+ "\n");
    }

}
```

실행해서 첫번재 뷰를 터치하면 값이 뜨는것을 볼 수 있다

## 제스쳐

위에와 이어서 계속 ㄱㄱㄱ

```java
package com.example.myevent;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.GestureDetector;
import android.view.MotionEvent;
import android.view.View;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    TextView textView;

    GestureDetector detector;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);//textView라는 아이디른 가진 뷰 찾기

        View view = findViewById(R.id.view);//첫번째 뷰
        view.setOnTouchListener(new View.OnTouchListener() {
            @Override
            public boolean onTouch(View view, MotionEvent motionEvent) {//터치 이벤트
                //손으로 누르거나 움직이거나 떼면 이 함수 호출됨
                int action= motionEvent.getAction();//호출 됐을때 상태 저장(눌림, 움직임 같은)

                float curX = motionEvent.getX();
                float curY = motionEvent.getY();

                if(action == MotionEvent.ACTION_DOWN){ //손가락이 눌린 상태
                    println("손가락 눌림 : "+curX+" , "+curY);
                }else if (action == MotionEvent.ACTION_MOVE){
                    println("손가락 움직임 : "+curX+" , "+curY);
                }else if (action == MotionEvent.ACTION_UP){
                    println("손가락 뗌 : "+curX+" , "+curY);
                }
                return true;
            }
        });
        detector = new GestureDetector(this, new GestureDetector.OnGestureListener() {
            @Override
            public boolean onDown(MotionEvent motionEvent) {//눌렸을때
                println("onDown 호출됨");
                return true;
            }

            @Override
            public void onShowPress(MotionEvent motionEvent) {

            }

            @Override
            public boolean onSingleTapUp(MotionEvent motionEvent) {
                return false;
            }

            @Override
            public boolean onScroll(MotionEvent motionEvent, MotionEvent motionEvent1, float v, float v1) {
                return false;
            }

            @Override
            public void onLongPress(MotionEvent motionEvent) {
                println("onLongPress 호출됨");
            }

            @Override
            public boolean onFling(MotionEvent motionEvent, MotionEvent motionEvent1, float v, float v1) {
                println("onFling 호출됨 : " + v + " , " + v1);
                //v -> velocityX , v1 -> velocityY 속도 계산해줌
                return true;
            }
        });

        View view2 = findViewById(R.id.view2);//view2 두번째 뷰
        view2.setOnTouchListener(new View.OnTouchListener() {
            @Override
            public boolean onTouch(View view, MotionEvent motionEvent) {
                detector.onTouchEvent(motionEvent);
                return true;

            }
        });

    }
    public void println(String data){
        textView.append(data+ "\n");
    }

}
```

## 키

위에랑 이어서 계속 ㄱㄱㄱ

```java
package com.example.myevent;

import androidx.appcompat.app.AppCompatActivity;

import android.icu.text.RelativeDateTimeFormatter;
import android.os.Bundle;
import android.view.GestureDetector;
import android.view.KeyEvent;
import android.view.MotionEvent;
import android.view.View;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    TextView textView;

    GestureDetector detector;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);//textView라는 아이디른 가진 뷰 찾기

        View view = findViewById(R.id.view);//첫번째 뷰
        view.setOnTouchListener(new View.OnTouchListener() {
            @Override
            public boolean onTouch(View view, MotionEvent motionEvent) {//터치 이벤트
                //손으로 누르거나 움직이거나 떼면 이 함수 호출됨
                int action= motionEvent.getAction();//호출 됐을때 상태 저장(눌림, 움직임 같은)

                float curX = motionEvent.getX();
                float curY = motionEvent.getY();

                if(action == MotionEvent.ACTION_DOWN){ //손가락이 눌린 상태
                    println("손가락 눌림 : "+curX+" , "+curY);
                }else if (action == MotionEvent.ACTION_MOVE){
                    println("손가락 움직임 : "+curX+" , "+curY);
                }else if (action == MotionEvent.ACTION_UP){
                    println("손가락 뗌 : "+curX+" , "+curY);
                }
                return true;
            }
        });
        detector = new GestureDetector(this, new GestureDetector.OnGestureListener() {
            @Override
            public boolean onDown(MotionEvent motionEvent) {//눌렸을때
                println("onDown 호출됨");
                return true;
            }

            @Override
            public void onShowPress(MotionEvent motionEvent) {

            }

            @Override
            public boolean onSingleTapUp(MotionEvent motionEvent) {
                return false;
            }

            @Override
            public boolean onScroll(MotionEvent motionEvent, MotionEvent motionEvent1, float v, float v1) {
                return false;
            }

            @Override
            public void onLongPress(MotionEvent motionEvent) {
                println("onLongPress 호출됨");
            }

            @Override
            public boolean onFling(MotionEvent motionEvent, MotionEvent motionEvent1, float v, float v1) {
                println("onFling 호출됨 : " + v + " , " + v1);
                //v -> velocityX , v1 -> velocityY 속도 계산해줌
                return true;
            }
        });

        View view2 = findViewById(R.id.view2);
        view2.setOnTouchListener(new View.OnTouchListener() {
            @Override
            public boolean onTouch(View view, MotionEvent motionEvent) {
                detector.onTouchEvent(motionEvent);
                return true;

            }
        });

    }

    @Override//이부분 추가함
    public boolean onKeyDown(int keyCode, KeyEvent event) {
        if(keyCode == KeyEvent.KEYCODE_BACK){//back버튼이 눌렸을때 호출됨
            println("시스템 [BACK] 버튼이 눌렸어요");
            return true;
        }
        return  false;

    }

    public void println(String data){
        textView.append(data+ "\n");
    }

}
```

## 단말기 회전

새 프로젝트 

res 안에 새폴더 layout-land 만들기

만든 폴더가 안보인다면

![image](https://user-images.githubusercontent.com/69203345/130793318-302a779f-79bf-4893-97dc-ad34f6ac6ce1.png)

Android 가 아닌 Project Files 로 바꿔서 찾아보자

layout 밑에있던 main.xml 도 복사해서 넣어주기

![image](https://user-images.githubusercontent.com/69203345/130793629-a461a2d1-6b22-4267-a05b-f5b797f966fe.png)

<img src="https://user-images.githubusercontent.com/69203345/130793803-573cd814-60ca-45fe-bd9b-2092ac5983f6.png" alt="image" style="zoom:67%;" />

그럼 이렇게 가로로 돼있는 화면을 볼 수 있다(가로방향 텍스트는 내가 넣어준거다)

단말기를 켜서 돌려보면 바뀌는것을 볼 수있다

MainActivity.java 파일에

```java
package com.example.myorientation;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        showToast("onCreate 호출됨");//추가

    }

    @Override//추가
    protected void onDestroy() {
        super.onDestroy();
        showToast("onDestroy 호출됨");
    }

    public void showToast(String data){//추가
        Toast.makeText(this,data, Toast.LENGTH_SHORT).show();
    }
}
```

코드를 넣어주면 화면이 돌아갈때 없어졌다가 새로 만들어진다는것을 알수 있다

**화면이 없어졌다 다시 만들어 지는 과정에서 데이터의 저장**

가로화면에 textView 하나 만들기

```java
package com.example.myorientation;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {
    String name;
    EditText editText;
    TextView textView2;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        showToast("onCreate 호출됨");

        editText = findViewById(R.id.editText);
        textView2 = findViewById(R.id.textView2);

        Button button = findViewById(R.id.button);
        if (button !=null){

            button.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View view) {
                    if(editText !=null){
                        name=editText.getText().toString();//editText값을 name에 저장
                        showToast("사용자 입력값을 name 변수에 할당함");
                    }
                }
            });
        }
        if(savedInstanceState != null){
            if(textView2 != null){
                name = savedInstanceState.getString("name"); //값빼옴
                textView2.setText(name);

                showToast("값을 복원 했습니다 : " + name);
           }
        }

    }

    @Override
    protected void onSaveInstanceState(Bundle outState) {//화면이 없어질때 호출됨
        super.onSaveInstanceState(outState);

        outState.putString("name", name);
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        showToast("onDestroy 호출됨");
    }

    public void showToast(String data){
        Toast.makeText(this,data, Toast.LENGTH_SHORT).show();
    }
}
```

<img src="https://user-images.githubusercontent.com/69203345/130804941-1906023f-ffae-4522-8042-ae28657c44f4.png" alt="image" style="zoom:67%;" />

잘 저장되고 불러와지는 결과를 볼수 있다

### 방향 전환이 되더라도 데이터 유지

새 프로젝트

manifest.xml수정

activity 태그 안에 

> android:configChanges="orientation|screenSize|keyboardHidden"

추가 해주기

mainActivity.java 에 추가

```java
package com.example.myorientation2;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

import android.content.res.Configuration;
import android.os.Bundle;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    @Override
    public void onConfigurationChanged(@NonNull Configuration newConfig) { //방향 전환시 호출

        super.onConfigurationChanged(newConfig);
        if(newConfig.orientation == Configuration.ORIENTATION_LANDSCAPE){//가로방향인지 확인
            showToast("가로 방향임");
        }else if (newConfig.orientation == Configuration.ORIENTATION_PORTRAIT ){//세로인지 확인
            showToast("세로방향임");
        }
    }
    public void showToast(String data){
        Toast.makeText(this, data, Toast.LENGTH_SHORT).show();
    }
}
```

방향이 바뀌면 기본은 activity가 종료됐다가 새로 만드는거지만 종료되지 않도록 할수있다

# Toast 다루기

새 프로젝트

## 위치 바꾸기

다만 api 30 이상인 에뮬레이터에선 작동하지 않음..

그래도 해보려고 api 29인걸로 해봄...

![image](https://user-images.githubusercontent.com/69203345/130814451-f2c8b49d-6031-4b36-8fbf-682a769379c7.png)

바꼈다!



