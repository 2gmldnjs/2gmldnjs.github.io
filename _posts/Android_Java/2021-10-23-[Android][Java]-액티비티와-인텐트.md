---
title:  "[Android][Java] 액티비티와 인텐트"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-10-23 23:45:56
---

# 액티비티와 인텐트

4가지 중요한 개념

- 액플리케이션
- 액티비티
- 액티비티 스택
- 태스크

## 애플리케이션

- 한개 이상의 액티비티들로 구성
- 액티비티들은 애플리케이션 안에서 느슨하게 묶여있다

## 액티비티

- 애플리메이션을 구성하는 빌딩 블록

## 태스크

- 스택에 있는 액티비티
- 하나의 태스크는 스택에 있는 액티비티들로 구성된다

## 액티비티 스택

- back키를 누르면 현재 액티비티를 제거하고 이전 액티비티로 되돌아 간다
- 사용자가 방문한 액티비티들은 어딘가에 기억

## 인텐트

- 각각의 화면은 별도의 액티비티로 구현된다
- 하나의 액티비티(화면)에서 다른 액티비티(화면)로 전환 하려면 어떻게 하여야 하는가?
- 다른 액티비티를 시작 하려면 액티비티의 실행에 필요한 여러가지 정보들을 보내주어야 한다
- 정보를 인텐트에 실어서 보낸다

### 명시적 인텐트

- 애플리케이션A의 컴포넌트 B를 구동시켜라 와 같이 명확하게 지정
- 실행하고자 하는 액티비티의 이름을 적어 준다

### 암시적 인텐트

- 예) 지도를 보여줄 수 있는 컴포넌트이면 어떤 것이라도 좋다

## 명시적인 인텐트 예제

두개의 액티비티로 이루어진 애플리케이션을 작성

첫번째 액티비티는 Activity1, 두번째 액티비티는 Activity2 

xml도 2개를 만들어줌

![image](https://user-images.githubusercontent.com/69203345/138444322-80384a91-b629-4aad-ba29-d6079928a521.png)

layout1.xml 디자인

```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <TextView
            android:id="@+id/textView"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="여기는 액티비티1 입니다" />
<!--무명클래스 사용-->
        <Button 
            android:id="@+id/button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="이미지 표시 액티비티 열기" />
    </LinearLayout>
```

layout2.xml

```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <TextView
            android:id="@+id/textView2"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="여기는 액티비티2 입니다" />

        <ImageView
            android:id="@+id/imageView"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            app:srcCompat="@drawable/ic_launcher_foreground" />

        <Button
            android:id="@+id/button2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="닫기" />
    </LinearLayout>
```

Activity1 클래스는 Activity 클래스에서 상속을 받아 작성

Activity1.java

```java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.layout1);
        Button b = (Button) findViewById(R.id.button);
        b.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {//버튼을 클릭하면 Activity2를 시작
                //인텐트 객체 생성후 두번째 액티비트의 클래스 이름을 인수로 전달해서 생성
                Intent intent = new Intent(Activity1.this,Activity2.class);
                startActivity(intent);
                
            }
        });
    }
```

Activity2.java

```java
public class Activity2 extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.layout2);
        Button b = (Button) findViewById(R.id.button2);
        b.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                finish();//현재 액티비티 종료
            }
        });

    }
}
```

매니페스트 파일에 추가

```xml
<activity android:name="Activity2" android:label="Activity2"></activity>
```

실행화면

<img src="https://user-images.githubusercontent.com/69203345/138446848-726a60e0-ccea-43e8-b793-07037b057515.png" alt="Screenshot_1634902353" style="zoom:33%;" />

<img src="https://user-images.githubusercontent.com/69203345/138446853-6edb345f-b139-4b08-b00c-5bc31260616a.png" alt="Screenshot_1634902355" style="zoom:33%;" />

## 여러 페이지로 된 애플리케이션 작성

layout 4개 사용

activity_main.xml

```xml
    <FrameLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@color/black">

        <AbsoluteLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orienation="vertical">

            <Button
                android:id="@+id/button1"
                android:layout_width="192dp"
                android:layout_height="wrap_content"
                android:layout_x="100dp"
                android:layout_y="100dp"
                android:background="#ff0000"
                android:gravity="center"
                android:onClick="myListener"
                android:text="Introduction">
            </Button>
            <Button
                android:id="@+id/button2"
                android:layout_width="192dp"
                android:layout_height="wrap_content"
                android:layout_x="100dp"
                android:layout_y="150dp"
                android:background="#ff0000"
                android:gravity="center"
                android:onClick="myListener1"
                android:text="Settings" />

            <Button
                android:layout_width="192dp"
                android:layout_height="wrap_content"
                android:layout_x="100dp"
                android:layout_y="200dp"
                android:background="#ff0000"
                android:gravity="center"
                android:onClick="myListener2"
                android:text="Start" />

        </AbsoluteLayout>
    </FrameLayout>
```

IntroPage 에서 사용할 intro.xml을 작성

```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@color/purple_200"
        android:orientation="vertical">

        <TextView
            android:id="@+id/textView"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="텍스트/메세지
                          ...(중략)
                          텍스트/메세지/텍스트/메세지텍스트/메세지/텍스트/메세지"
            android:textAppearance="?android:attr/textAppearanceLarge"
            android:textColor="#FFFFFF"
            />
    </LinearLayout>
```

SetupPage에서 사용할 setup.xml

```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <TextView
            android:id="@+id/textView2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Difficulties" 
            android:textAppearance="?android:attr/textAppearanceLarge"/>

        <SeekBar
            android:id="@+id/seekBar"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />

        <TextView
            android:id="@+id/textView3"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Players"
            android:textAppearance="?android:attr/textAppearanceLarge"/>

        <SeekBar
            android:id="@+id/seekBar2"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />
    </LinearLayout>
```

StartPage에서 사용할 start.xml

```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@color/purple_500"
        android:orientation="vertical">

        <AnalogClock
            android:id="@+id/analogClock"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content" />

        <Chronometer
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Chronometer"
            android:textSize="100sp"
            android:textStyle="bold|italic"
            android:typeface="serif" />
    </LinearLayout>
```

각각의 화면을 액티비티로 작성

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
    public void myListener1(View target){ //버튼 onClick 속성
        Intent intent = new Intent(getApplicationContext(),IntroActivity.class);
        startActivity(intent);
    }
    public void myListener2(View target){
        Intent intent = new Intent(getApplicationContext(),SetupActivity.class);
        startActivity(intent);
    }
    public void myListener3(View target){
        Intent intent = new Intent(getApplicationContext(),StartActivity.class);
        startActivity(intent);
    }
    
}
```

IntroActivity.java

```java
public class IntroActivity extends AppCompatActivity {
    @Override
    protected void onCreate( Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.intro); //액티비티 화면 설정
    }
}
```

SetupActivity.java

```java
public class SetupActivity extends AppCompatActivity {
    @Override
    protected void onCreate( Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.setup);
    }
}
```

StartActivity.java

```java
public class StartActivity extends AppCompatActivity {
    @Override
    protected void onCreate( Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.start);       
    }
}
```

AndroidManifest.xml 을 설정

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest 
          ...중략
    <application
		...(중략)
        </activity>
        <!--새로 작성된 액티비티들은 여기에 들록해야 사용가능하다-->
        <activity
            android:name="IntroActivity"
            android:label="IntroActivity"/>
        <activity android:name="SetupActivity"
            android:label="SetupActivity"/>
        <activity android:name=".StartActivity"
            android:label="StartActivity"/>
    </application>
</manifest>
```

실행화면

<img src="https://user-images.githubusercontent.com/69203345/138460024-aee0659b-8aff-43af-933f-f13f02bb2b64.png" alt="Screenshot_1634908589" style="zoom:33%;" />

Intro

<img src="https://user-images.githubusercontent.com/69203345/138460096-6441fd59-9e5d-47f0-a1dc-e00d7cceaaa1.png" alt="Screenshot_1634908632" style="zoom:33%;" />

Settings

<img src="https://user-images.githubusercontent.com/69203345/138460160-f12fb49f-d26f-4372-9739-7d9af08444c4.png" alt="Screenshot_1634908654" style="zoom:33%;" />

Start

<img src="https://user-images.githubusercontent.com/69203345/138460233-33ec739f-c496-4c11-b34e-3a58ceab1967.png" alt="Screenshot_1634908690" style="zoom:33%;" />

## 액티비티로부터 결과 받기

<img src="https://user-images.githubusercontent.com/69203345/138465348-a6c6dc90-a755-4ce0-abdd-2243fc032634.png" alt="image" style="zoom:50%;" />

<img src="https://user-images.githubusercontent.com/69203345/138465177-ed8e976a-5429-48af-b337-9894afcda5ed.png" alt="image" style="zoom: 50%;" />

예제

activity_main.xml

```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <Button
            android:id="@+id/button"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="서브 액티비티로부터 문자열 반환받기" />

        <TextView
            android:id="@+id/textView"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="반환된 문자열" />

        <TextView
            android:id="@+id/textView2"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="_____________________" />
    </LinearLayout>
```

sub.xml도 만들기

```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <EditText
            android:id="@+id/edit"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" >
            <requestFocus></requestFocus>
        </EditText>
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center"
            android:orientation="horizontal">

            <Button
                android:id="@+id/button_ok"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="입력완료" />

            <Button
                android:id="@+id/button_cancel"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="취소" />
        </LinearLayout>
    </LinearLayout>
```

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {
    TextView text;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ActivityResultLauncher<Intent> onActivityResult = registerForActivityResult(
                new ActivityResultContracts.StartActivityForResult(),
                new ActivityResultCallback<ActivityResult>() {
                    @Override
                    public void onActivityResult(ActivityResult result) {
                        if (result.getResultCode() == Activity.RESULT_OK) {
                            // There are no request codes
                            Intent in = result.getData();
                            text.setText(in.getStringExtra("INPUT_TEXT"));
                        }
                    }
                });
        
        Button button = (Button) findViewById(R.id.button);
        text = (TextView) findViewById(R.id.text);
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent in = new Intent(MainActivity.this, SubActivity.class);
                onActivityResult.launch(in);
            }
        });

    }
}
```

SubActivity.java

```java
public class SubActivity extends AppCompatActivity {
    EditText edit;

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.sub);
        
        edit = (EditText) findViewById(R.id.edit);
        Button button_ok = (Button) findViewById(R.id.button_ok);
        button_ok.setOnClickListener(new View.OnClickListener() {
            @Override //메인 액티비티로 결과를 보냄
            public void onClick(View view) {
                Intent intent = new Intent();
                intent.putExtra("INPUT_TEXT",edit.getText().toString());
                setResult(RESULT_OK,intent);
                finish();
            }
        });
        
        Button button_cancel = (Button) findViewById(R.id.button_cancel);
        button_cancel.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                setResult(RESULT_CANCELED);
                finish();
            }
        });
    }
}
```

## 암시적인 인텐트

- 어떤 작업을 하기를 원하지만 그 작업을 담당하는 컴포넌트의 이름을 명확하게 모르는 경우에 사용

### 암시적인 인텐트의 형식

<img src="https://user-images.githubusercontent.com/69203345/138546315-c7de786d-e35a-49ca-8af0-40bce3385a22.png" alt="image" style="zoom: 80%;" />

액션의 종류

|    상수     | 타겟 컴포넌트 |                        액션                        |
| :---------: | :-----------: | :------------------------------------------------: |
| ACTION_VIEW |   액티비티    |              데이터를 사용자에게 표시              |
| ACTION_EDIT |   액티비티    |        사용자가 편집할 수 있는 데이터 표시         |
| ACTION_MAIN |   액티비티    |           태스크의 초기 액티비티로 설정            |
| ACTION_CALL |   액티비티    |                  전화통화를 시작                   |
| ACTION_SYNC |   액티비티    | 모바일 장치의 데이터를 서버상의 데이터와 일치 시킴 |
| ACTION_DIAL |   액티비티    |           전화번호를 누르는 화면을 표시            |

### 암시적 인텐트 예제

activity_main.xml

```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <Button
            android:id="@+id/call"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:onClick="onClick"
            android:text="전화걸기" />

        <Button
            android:id="@+id/map"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:onClick="onClick"
            android:text="지도보기" />

        <Button
            android:id="@+id/web"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:onClick="onClick"
            android:text="웹브라우저" />

        <Button
            android:id="@+id/contact"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:onClick="onClick"
            android:text="연락처보기" />
    </LinearLayout>
```

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
    
    public void onClick(View v){
        Intent intent = null;
        switch (v.getId()){
            case R.id.call:
                intent = new Intent(Intent.ACTION_DIAL, Uri.parse("tel:(+82)123456789"));
                break;
            case R.id.map:
                intent = new Intent(Intent.ACTION_VIEW,Uri.parse("geo:37.30.127.2?z=10"));
                break;
            case R.id.web:
                intent = new Intent(Intent.ACTION_VIEW,Uri.parse("http://www.google.com"));
                break;
            case R.id.contact:
                intent = new Intent(Intent.ACTION_VIEW,Uri.parse("content://contacts/people/"));
                break;
        }
        if(intent!=null){
            startActivity(intent); //인탠트를 실행
        }
    }
}
```

매니패스트 파일에 추가

```xml
    <uses-permission android:name="android.permission.CALL_PHONE"/>
    <uses-permission android:name="android.permission.CAMERA"/>
    <uses-permission android:name="android.permission.READ_CONTACTS"/>
    <uses-permission android:name="android.permission.INTERNET"/>
```

실행화면

<img src="https://user-images.githubusercontent.com/69203345/138549732-286231d2-c622-4f5a-ab31-485f63fcc0d6.png" alt="Screenshot_1634978754" style="zoom: 33%;" />

<img src="https://user-images.githubusercontent.com/69203345/138549734-2206a92c-9a9a-4ab6-a68b-00ac1547b270.png" alt="Screenshot_1634978758" style="zoom:33%;" />

# 멀티태스킹

- 동시에 여러 태스크를 실행
- 현재의 태스크를 배경(background)로 보내고 다른 태스크를 전경(foreground)에서 시작할  수 있다

## 오버뷰 화면

최근에 사용된 액티비티들과 태스크들을 보여주는 화면

# 액티비티 생애주기

실행상태(resumed,running): 액티비티가 전경에 위치하고 있으며 사용자의 포커스를 가지고 있다

일시멈춤 상태(paused): 다른 액티비티가 전경에 있으며 포커스를 가지고 있지만 현재 액티비티의 일부가 아직도 화면에서 보이고 있는 상태이다

정지 상태(stopped): 액티비티는 배경에 위치한다

## 콜백 메소드

onCreate()

- 액티비티가 생성되면서 호출
- 중요한 구성요소들을 초기화

onPause()

- 사용자가 액티비티를 떠나고 있을때, 이 메소드가 호출
- 그동안 이루어졌던 변경사항을 저장

# 인텐트 필터

액션이 ACTION_MAIN인 인텐트만 처리함

# 연습문제

구성

EditText

Button 2개

RadioGroup

RadioButton 2개

ImageView 이미지 3개

작동

글자 나타내기 버튼을 클릭하면 EditText에 입력한 글자가 잠깐 Toast메시지로 출력

홈페이지 열기 버튼을 클릭하면 EditText에 입력한 url이 열림

처음에는 기본 이미지가 나타나고, 라디오 버튼을 클릭시 다른 이미지로 변경

activity_main.xml

```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <EditText
            android:id="@+id/edittext"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />

        <Button
            android:id="@+id/btn_text"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="글자 나타내기" />

        <Button
            android:id="@+id/btn_url"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="홈페이지열기" />

        <RadioGroup
            android:id="@+id/radiogroup"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center">

            <RadioButton
                android:id="@+id/radioButton1"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="누가" />

            <RadioButton
                android:id="@+id/radioButton2"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="오레오" />
        </RadioGroup>

        <ImageView
            android:id="@+id/image"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            app:srcCompat="@mipmap/ic_launcher" />
    </LinearLayout>
```

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {
    EditText editText;
    Button btntext, btnurl;
    RadioGroup radioGroup;
    RadioButton radioButton1, radioButton2;
    ImageView imageView;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editText = (EditText) findViewById(R.id.edittext);

        btntext = (Button) findViewById(R.id.btn_text);
        //글자 나타내기 버튼 클릭시
        btntext.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(MainActivity.this, editText.getText().toString(), Toast.LENGTH_LONG).show();
            }
        });

        btnurl = (Button) findViewById(R.id.btn_url);
        //홈페이지 열기 버튼 클릭시
        btnurl.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String url = editText.getText().toString();
                Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(url));
                startActivity(intent); //인텐트 실행
            }
        });
        imageView = (ImageView) findViewById(R.id.image);

        radioGroup = (RadioGroup) findViewById(R.id.radiogroup);
        radioButton1 = (RadioButton) findViewById(R.id.radioButton1);
        radioButton2 = (RadioButton) findViewById(R.id.radioButton2);
		//버튼 체크상태 변경 캐치 리스너
        radioGroup.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(RadioGroup radioGroup, int i) {
                if(radioButton1.isChecked()){//이미지 변경
                    imageView.setImageResource(R.drawable.android);
                }
                else if(radioButton2.isChecked()){
                    imageView.setImageResource(R.drawable.android_oreo);
                }
            }
        });
    }
}
```

실행

<img src="https://user-images.githubusercontent.com/69203345/138561109-c927b12c-18dc-490e-81d2-4da7321cc162.png" alt="Screenshot_1635000248" style="zoom:33%;" />

<img src="https://user-images.githubusercontent.com/69203345/138561111-fdc776a2-91d9-4125-9250-b2b6332e9cd9.png" alt="Screenshot_1635000257" style="zoom:33%;" />
