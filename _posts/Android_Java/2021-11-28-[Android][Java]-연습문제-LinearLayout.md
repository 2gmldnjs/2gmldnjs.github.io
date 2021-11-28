---
title:  "[Android][Java] 연습문제-LinearLayout"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-11-28 20:46:80

---
# 연습문제1

구성  
이미지1개 or 2개  
버튼  
이미지 뷰  

작동  
버튼을 클릭하면 이미지가 10도씩 돌아가도록

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
            android:src="@drawable/cat" />
    </LinearLayout>
```

MainActivity.java
```java
public class MainActivity extends AppCompatActivity {
    Button btn;
    ImageView iv;
    float angle;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        getSupportActionBar().setDisplayShowHomeEnabled(true);
        getSupportActionBar().setIcon(R.mipmap.ic_launcher_round);
        setTitle("연습문제");

        btn = (Button) findViewById(R.id.button);
        iv = (ImageView) findViewById(R.id.imageView);

        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                angle = angle+10;
                iv.setRotation(angle);

            }
        });
    }
}
```

실행

<img src="https://user-images.githubusercontent.com/69203345/143735075-6d29b46b-f657-4569-bb5f-3578f467269c.png" alt="Screenshot_1638087678" style="zoom: 33%; ">

# 연습문제2

구성  
리니어 레이아웃  
xml로만 작성

activity_main.xml
```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:orientation="horizontal">

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:orientation="vertical">

                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:layout_weight="1"
                    android:background="#EAE088"
                    android:orientation="vertical"></LinearLayout>

                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:layout_weight="1"
                    android:background="#000000"
                    android:orientation="vertical"></LinearLayout>
            </LinearLayout>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:orientation="horizontal">

                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:layout_weight="1"
                    android:background="#2196F3"
                    android:orientation="horizontal">

                </LinearLayout>

                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:layout_weight="1"
                    android:background="#673AB7"
                    android:orientation="horizontal"></LinearLayout>

                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:layout_weight="1"
                    android:background="#96E899"
                    android:orientation="horizontal"></LinearLayout>

            </LinearLayout>

        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:background="#324ED6"
            android:orientation="vertical">

        </LinearLayout>
    </LinearLayout>
```

실행

<img src="https://user-images.githubusercontent.com/69203345/143740924-36d39a50-b2a5-47b1-ada9-d74401385b9e.png" alt="Screenshot_1638090122" style="zoom: 33%; ">

# 연습문제3

구성

<img src="https://user-images.githubusercontent.com/69203345/143742661-aa33d66a-b0f0-42c2-910e-88dfffb51e3a.png" alt="image" style="zoom:80%;" />

레이아웃의 폭은 View.getWidth(), View.getHeight() 메소드를 사용

작동  
각 레이아웃을 클릭함녀 레이아의 폭과 높이가 Toast 메시지로 출력되도록
Java 프로그래밍  
안쪽 레이아웃은 모두 정사각형  
안쪽 레이아웃 부터 50dp, 150dp, 250dp  

activity_main.xml
```xml
    <LinearLayout
        android:id="@+id/layout1"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:gravity="center"
        android:orientation="horizontal">

        <LinearLayout
            android:id="@+id/layout2"
            android:layout_width="250dp"
            android:layout_height="250dp"
            android:background="#4462F8"
            android:gravity="center"
            android:orientation="vertical">

            <LinearLayout
                android:id="@+id/layout3"
                android:layout_width="150dp"
                android:layout_height="150dp"
                android:background="#FFEB3B"
                android:gravity="center"
                android:orientation="vertical">

                <LinearLayout
                    android:id="@+id/layout4"
                    android:layout_width="50dp"
                    android:layout_height="50dp"
                    android:background="@color/black"
                    android:gravity="center"
                    android:orientation="vertical"></LinearLayout>
            </LinearLayout>
        </LinearLayout>
    </LinearLayout>
```

MainActivity.java
```java
public class MainActivity extends AppCompatActivity {
    LinearLayout layout1,layout2,layout3,layout4;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        setTitle("연습문제");

        layout1 = (LinearLayout) findViewById(R.id.layout1);
        layout2 = (LinearLayout) findViewById(R.id.layout2);
        layout3 = (LinearLayout) findViewById(R.id.layout3);
        layout4 = (LinearLayout) findViewById(R.id.layout4);

        layout1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String str1 = Integer.toString(layout1.getWidth());
                String str2 = Integer.toString(layout1.getHeight());
                String str = str1 + "X" + str2;
                Toast.makeText(getApplicationContext(),str,Toast.LENGTH_SHORT).show();
            }
        });
        layout2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String str1 = Integer.toString(layout2.getWidth());
                String str2 = Integer.toString(layout2.getHeight());
                String str = str1 + "X" + str2;
                Toast.makeText(getApplicationContext(),str,Toast.LENGTH_SHORT).show();
            }
        });
        layout3.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String str1 = Integer.toString(layout3.getWidth());
                String str2 = Integer.toString(layout3.getHeight());
                String str = str1 + "X" + str2;
                Toast.makeText(getApplicationContext(),str,Toast.LENGTH_SHORT).show();
            }
        });
        layout4.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String str1 = Integer.toString(layout4.getWidth());
                String str2 = Integer.toString(layout4.getHeight());
                String str = str1 + "X" + str2;
                Toast.makeText(getApplicationContext(),str,Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```

실행

<img src="https://user-images.githubusercontent.com/69203345/143765345-edbc32ed-ebb7-4819-a4b7-5fa60d8e72bc.png" alt="Screenshot_1638097736" style="zoom:33%;" />

# 연습문제4

구성

<img src="https://user-images.githubusercontent.com/69203345/143765405-0ea66b36-b7b4-4d5e-a30d-fb4856d160ef.png" alt="image" style="zoom:80%;" />

xml을 사용하지 않고 Java 코드로만 작성

MainActivity.java
```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setTitle("연습문제");

        LinearLayout.LayoutParams params = new LinearLayout.LayoutParams(
                LinearLayout.LayoutParams.MATCH_PARENT,
                LinearLayout.LayoutParams.MATCH_PARENT, 1);

        LinearLayout baseLayout = new LinearLayout(this); //전체 레이아웃
        baseLayout.setOrientation(LinearLayout.VERTICAL);
        baseLayout.setLayoutParams(params); //위에 params 설정으로 세팅

        LinearLayout upLayout = new LinearLayout(this); //상단 큰 레이아웃
        upLayout.setOrientation(LinearLayout.HORIZONTAL);
        upLayout.setLayoutParams(params);

        LinearLayout upLeft = new LinearLayout(this); //상단 왼쪽
        upLeft.setLayoutParams(params);
        upLeft.setBackgroundColor(Color.RED);
        upLayout.addView(upLeft);

        LinearLayout upRight = new LinearLayout(this); //상단 큰 오른쪽
        upRight.setOrientation(LinearLayout.VERTICAL);
        upRight.setLayoutParams(params);
        upLayout.addView(upRight);

        LinearLayout upRight1 = new LinearLayout(this); //상단 오른쪽1
        upRight1.setLayoutParams(params);
        upRight1.setBackgroundColor(Color.YELLOW);
        upRight.addView(upRight1);

        LinearLayout upRight2 = new LinearLayout(this); //상단 오른쪽2
        upRight2.setLayoutParams(params);
        upRight2.setBackgroundColor(Color.BLACK);
        upRight.addView(upRight2);


        LinearLayout downLayout = new LinearLayout(this); //하단 큰 레이아웃
        downLayout.setLayoutParams(params); //vertical horizon 상관 없기 때문에 생략했음
        downLayout.setBackgroundColor(Color.BLUE);
        baseLayout.addView(upLayout); //baseLayout에 추가(붙임)
        baseLayout.addView(downLayout);//추가하는 순서대로

        setContentView(baseLayout);
    }
}
```

실행

<img src="https://user-images.githubusercontent.com/69203345/143766295-3cb6fd41-4971-4dc7-8848-3cc960b84f0b.png" alt="Screenshot_1638099841" style="zoom:30%;" />