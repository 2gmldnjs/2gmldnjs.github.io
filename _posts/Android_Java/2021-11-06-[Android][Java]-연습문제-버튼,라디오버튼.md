---
title:  "[Android][Java] 연습문제-버튼,라디오버튼"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-11-06 23:55:16
---

# 연습문제1

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
        getSupportActionBar().setDisplayShowHomeEnabled(true);
        getSupportActionBar().setIcon(R.mipmap.ic_launcher);
        getSupportActionBar().setTitle("좀 그럴듯한 앱");

        editText = (EditText) findViewById(R.id.edittext);

        btntext = (Button) findViewById(R.id.btn_text);
        btntext.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(MainActivity.this, editText.getText().toString(), Toast.LENGTH_LONG).show();
            }
        });

        btnurl = (Button) findViewById(R.id.btn_url);
        btnurl.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(editText.getText().toString()));
                startActivity(intent);
            }
        });
        imageView = (ImageView) findViewById(R.id.image);

        radioGroup = (RadioGroup) findViewById(R.id.radiogroup);
        radioButton1 = (RadioButton) findViewById(R.id.radioButton1);
        radioButton2 = (RadioButton) findViewById(R.id.radioButton2);

        radioGroup.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(RadioGroup radioGroup, int i) {
                if(radioButton1.isChecked()){
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

<img src="https://user-images.githubusercontent.com/69203345/140612305-cdd7f2b8-73b9-4653-bc44-8ce0b5139c74.png" alt="Screenshot_1636207144" style="zoom:33%;" />

<img src="https://user-images.githubusercontent.com/69203345/140612307-e8cc9aa3-7f09-419f-b01b-cebe79b55bfa.png" alt="Screenshot_1636207151" style="zoom:33%;" />

# 연습문제2

버튼 1개

이미지뷰 1개

버튼에도 이미지 넣기

버튼을 클릭시 이미지뷰 이미지가 10도씩 회전하도록 하기

xml의 속성중 drawableLeft, drawableRight 등이 있다

activity_main.xml

```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:gravity="center"
        android:orientation="vertical">

        <Button
            android:id="@+id/button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:drawableLeft="@android:mipmap/sym_def_app_icon"
            android:drawableRight="@android:mipmap/sym_def_app_icon"
            android:text="회전하기" />

        <ImageView
            android:id="@+id/imageView"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            app:srcCompat="@drawable/cat" />
    </LinearLayout>
```

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {
    Button btn;
    ImageView imageView;
    float angle=0;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);



        btn =(Button) findViewById(R.id.button);
        imageView = (ImageView) findViewById(R.id.imageView);

        getSupportActionBar().setDisplayShowHomeEnabled(true);
        getSupportActionBar().setIcon(R.mipmap.ic_launcher);
        setTitle("에에ㅔㅇ에ㅔ엥");

        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                angle += 10;
                imageView.setRotation(angle);
            }
        });
    }
}
```

실행

<img src="https://user-images.githubusercontent.com/69203345/140613927-ca8d789e-6528-4182-8a86-7cdc521ac0cf.png" alt="Screenshot_1636210463" style="zoom:33%;" />

