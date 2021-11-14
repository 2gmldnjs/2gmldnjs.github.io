---
title:  "[Android][Java] 연습문제"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-11-14 22:41:43

---

# 연습문제1

구성

체크박스 3개 

작동

체크박스를 선택할 때마다 버튼의 속성이 설정되도록 작성

activity_main.xml

```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <CheckBox
            android:id="@+id/checkBox1"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Enabled속성" />

        <CheckBox
            android:id="@+id/checkBox2"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Clickable속성" />

        <CheckBox
            android:id="@+id/checkBox3"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="45도회전" />

        <Button
            android:id="@+id/button"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Button" />
    </LinearLayout>

```

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {
    CheckBox box1, box2, box3;
    Button btn;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);


        box1 = (CheckBox) findViewById(R.id.checkBox1);
        box2 = (CheckBox) findViewById(R.id.checkBox2);
        box3 = (CheckBox) findViewById(R.id.checkBox3);
        btn = (Button) findViewById(R.id.button);

        box1.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(CompoundButton compoundButton, boolean b) {
                if (b) btn.setEnabled(true);
                else btn.setEnabled(false);
            }
        });
        box2.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(CompoundButton compoundButton, boolean b) {
                if (b) btn.setClickable(true);
                else btn.setClickable(false);
            }
        });
        box3.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(CompoundButton compoundButton, boolean b) {
                if (b) btn.setRotation(45);
                else btn.setRotation(0);
            }
        });
    }


}
```

실행

<img src="https://user-images.githubusercontent.com/69203345/141682332-ddf25030-9d92-4a30-af04-ccbefa0b9ba9.png" alt="Screenshot_1636895150" style="zoom: 33%;" />

# 연습문제2

구성

EditText 

작동

EditText의 키가 눌릴때마다 바뀐 글자가 토스트 메시지로 나오도록 작성

setOnKeyListener() 를 사용

activity_main.xml

```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <EditText
            android:id="@+id/editTextTextPersonName"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:inputType="textPersonName" />
    </LinearLayout>
```

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {
    EditText editText;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        EditText editText = (EditText) findViewById(R.id.editText);
        editText.setOnKeyListener(new View.OnKeyListener() {
            @Override
            public boolean onKey(View view, int i, KeyEvent keyEvent) {
                if (keyEvent.getAction()==KeyEvent.ACTION_UP){//키가 눌렸으면
                    Toast.makeText(getApplicationContext(), editText.getText().toString(),Toast.LENGTH_SHORT).show();
                }
                return false;
            }
        });
    }
}
```

실행

<img src="https://user-images.githubusercontent.com/69203345/141682694-0c20e299-82da-4fdd-82e6-f3df4eaceb63.png" alt="Screenshot_1636895867" style="zoom:33%;" />

# 연습문제3

구성

x

작동

xml 파일을 작성하지 않고 java 코드만으로 버튼을 만든후 클릭시 토스트 메시지로 "코드로 생성한 버튼입니다" 라고 출력하도록 작성

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        LinearLayout.LayoutParams params = new LinearLayout.LayoutParams(
                LinearLayout.LayoutParams.MATCH_PARENT, //width,height
                LinearLayout.LayoutParams.MATCH_PARENT);
        LinearLayout linearLayout = new LinearLayout(this);
        linearLayout.setOrientation(LinearLayout.VERTICAL);
        linearLayout.setBackgroundColor(Color.rgb(170,240,209));

        setContentView(linearLayout,params);

        Button btn = new Button(this);
        btn.setText("버튼입니다");
        btn.setBackgroundColor(Color.rgb(228,187,254));
        linearLayout.addView(btn);

        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(MainActivity.this,"코드로 생성한 버튼입니다",Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```

실행

<img src="https://user-images.githubusercontent.com/69203345/141683617-f222fd5c-a851-4b42-8ceb-272e65a832cf.png" alt="Screenshot_1636897198" style="zoom:33%;" />

