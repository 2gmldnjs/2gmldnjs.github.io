---
title:  "[Android][Java] 고급 위젯과 프래그먼트"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-10-16 19:37:20

---

# 어댑터 뷰

어댑터 뷰(AdapterView)는 배열이나 파일, 데이터 베이스에 저장된 데이터를 화면에 표시할 때 유용한 뷰

## 어댑터 뷰의 종류

- 리스트 뷰(ListView)
- 갤러리(Gallery)
- 스피너(Spinner)
- 그리드 뷰(GridView)

### 리스트 뷰

항목들을 수직으로 보여주는 어뎁터 뷰로 상하로 스크롤 가능

### 리스트 뷰 예제

레이아웃 파일 activity_main.xml 은 수정하지 않는다



MainActivity.java

```java
public class MainActivity extends ListActivity {//ListActivity 상속

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        String[] values = { "Apple", "Apricot", "Avocado", "Banana", "Blackberry",
                "Blueberry", "Cherry", "Coconut", "Cranberry",
                "Grape Raisin", "Honeydew", "Jackfruit", "Lemon", "Lime",
                "Mango", "Watermelon" };//1차원 배열 생성후 저장
        //문자열 ArrayAdapter 생성 
        ArrayAdapter<String> adapter = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1,values);
        setListAdapter(adapter);

    }
    protected void onListItemClick(ListView l, View v,int position, long id){
        //선택한 항목 읽어옴
        String item = (String) getListAdapter().getItem(position);
        Toast.makeText(this,item+" selected",Toast.LENGTH_LONG).show();
    }
}
```

리스트뷰의 표준 레이아웃

|            레이아웃 ID            |          설명           |
| :-------------------------------: | :---------------------: |
|        simple_list _item_1        |  하나의 텍스트 뷰 사용  |
|        simple_list _item_2        |  두개의 텍스트 뷰 사용  |
|     simple_list _item_checked     |    항목당 체크 표시     |
|  simple_list _item_single_choice  |   한 개의 항목만 선택   |
| simple_list _item_multiple_choice | 여러개의 항목 선택 가능 |

실행화면

<img src="https://user-images.githubusercontent.com/69203345/137577133-65414245-356f-416c-bcbe-1e5033a53ec1.png" alt="Screenshot_1634367095" style="zoom: 33%;" />

# 그리드 뷰

2차원의 그리드에 항목들을 표시하는 뷰그룹

## 그리드 뷰 예제

이미지 4장 넣어 놓기

activity_main.xml

```xml
    <GridView
        android:id="@+id/GridView01"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:columnWidth="90dp"
        android:gravity="center"
        android:horizontalSpacing="10dp"
        android:numColumns="auto_fit"
        android:stretchMode="columnWidth"
        android:verticalSpacing="10dp" />
```

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //GridView 아이디로 찾은후 gridView 객체에 저장
        GridView gridView = (GridView) findViewById(R.id.GridView01);
        //ListView 처럼 Adapter에 세팅
        gridView.setAdapter(new ImageAdapter(this));//ImageAdapter 호출
        gridView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> adapterView, View view, int i, long l) {
                Toast.makeText(MainActivity.this,""+i,Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```

ImageAdapter.java

직접 만들자

```java
package com.example.gridviewtest;

public class ImageAdapter extends BaseAdapter {
    private  Context mContext;
    public ImageAdapter(Context c){
        mContext = c;
    }
    @Override
    public int getCount() {
        return mThumbIds.length;
    }

    @Override
    public Object getItem(int i) {
        return null;
    }

    @Override
    public long getItemId(int i) {
        return 0;
    }

    @Override
    public View getView(int i, View view, ViewGroup viewGroup) {
        ImageView imageView;
        if(view == null){
            imageView = new ImageView(mContext);
            imageView.setLayoutParams(new ViewGroup.LayoutParams(300,300));
            imageView.setScaleType(ImageView.ScaleType.CENTER_CROP);
            imageView.setPadding(8,8,8,8);
        }else{
            imageView = (ImageView) view;
        }
        imageView.setImageResource(mThumbIds[i]);//어떤 이미지를 보여줄지
        return imageView;
    }
    // references to our images
    private Integer[] mThumbIds = { //정수형 배열에 저장
            R.drawable.sample_1, R.drawable.sample_2,
            R.drawable.sample_3, R.drawable.sample_4,
            R.drawable.sample_1, R.drawable.sample_2,
            R.drawable.sample_3, R.drawable.sample_4,
            R.drawable.sample_1, R.drawable.sample_2,
            R.drawable.sample_3, R.drawable.sample_4,
            R.drawable.sample_1, R.drawable.sample_2,
            R.drawable.sample_3, R.drawable.sample_4,
            R.drawable.sample_1, R.drawable.sample_2,
            R.drawable.sample_3, R.drawable.sample_4,
            R.drawable.sample_1, R.drawable.sample_2,
    };
}
```

실행

<img src="https://user-images.githubusercontent.com/69203345/137579301-dd5e0538-3490-42a6-8c51-7ddc0a0c25a8.png" alt="Screenshot_1634370857" style="zoom:33%;" />

이미지를 클릭시 번호가 토스트 메세지로 뜬다

# 스피너

스피너(Spinner)는 항목을 선택하기 위한 드롭다운 리스트

## 스피너 예제

activity_main.xml 디자인

```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        android:padding="10dp">

        <TextView
            android:id="@+id/textView"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="10dp"
            android:text="@string/planet_prompt" />

        <Spinner
            android:id="@+id/spinner"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:prompt="@string/planet_prompt" />
    </LinearLayout>
```

strings.xml

```xml
    <string name="planet_prompt">행성을 선택하시오</string>

    <string-array name="planets_array">
        <item>수성</item>
        <item>금성</item>
        <item>지구</item>
        <item>화성</item>
        <item>목성</item>
        <item>토성</item>
        <item>천왕성</item>
        <item>해왕성</item>
    </string-array>
```

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Spinner spinner = (Spinner) findViewById(R.id.spinner);
        ArrayAdapter<CharSequence> adapter = ArrayAdapter.createFromResource(this, R.array.planets_array, android.R.layout.simple_spinner_item);
        adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
        spinner.setAdapter(adapter);
        spinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener(){

            @Override
            public void onItemSelected(AdapterView<?> adapterView, View view, int i, long l) {
                Toast.makeText(adapterView.getContext(), "선택된 행성은 "+adapterView.getItemAtPosition(i).toString(), Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onNothingSelected(AdapterView<?> adapterView) {

            }
        });
    }
}
```

실행화면

<img src="https://user-images.githubusercontent.com/69203345/137580503-9752f2e9-24b3-4085-9d94-51cd759e2918.png" alt="Screenshot_1634372913" style="zoom: 33%;" />

# 프로그레스 바

작업의 진행 정도를 표시하는 위젯

## 프로그레스 바 예제

activity_main.xml

```xml
    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <Button
            android:id="@+id/button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentTop="true"
            android:layout_centerHorizontal="true"
            android:layout_marginTop="150dp"
            android:onClick="start"
            android:text="start" />

        <TextView
            android:id="@+id/textView"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentTop="true"
            android:layout_alignParentRight="true"
            android:layout_marginTop="19dp"
            android:text="다운로드를 시작하려면 아래 버튼을 누르시요"
            android:textAppearance="?android:attr/textAppearanceLarge" />
    </RelativeLayout>
```

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {
    private ProgressDialog progress;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        progress = new ProgressDialog(this);

    }
    public void start(View view){ //버튼클릭시 호출되는 함수
        progress.setCancelable(true);
        progress.setMessage("네트워크에서 다운로드 중입니다. ");
        progress.setProgressStyle(ProgressDialog.STYLE_HORIZONTAL);
        progress.setProgress(0);//0부터 시작
        progress.setMax(100);//최대 100
        progress.show();
		
        final Thread t = new Thread(){//Thread클래스의 객체 생성
            @Override
            public void run(){

                int time = 0;
                while(time < 100){
                    try {
                        sleep(200);
                        time += 5;
                        progress.setProgress(time);
                    } catch (InterruptedException e) {
                        // TODO Auto-generated catch block
                        e.printStackTrace();
                    }

                }

            }
        };
        t.start(); //실행
    }
}
```

실행

<img src="https://user-images.githubusercontent.com/69203345/137583007-07824b9e-54a4-4b0a-901c-5c0e755035ff.png" alt="Screenshot_1634377720" style="zoom: 33%;" />

# 시크 바

프로그레스 바의 확장판

사용자가 드래그할 수 있는 썸(thumb)이 추가

# 레이팅 바

별을 사용해여 점수를 표시하는 위젯

## 레이팅 바 예제

activity_main.xml

```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <TextView
            android:id="@+id/textView"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="평가해주세요"
            android:textAppearance="?android:attr/textAppearanceLarge"/>

        <RatingBar
            android:id="@+id/ratingBar"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:numStars="5"
            android:rating="2.0"
            android:stepSize="1.0" />

        <Button
            android:id="@+id/button"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="제출" />

        <LinearLayout
            android:id="@+id/linearlayout1"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="horizontal">

            <TextView
                android:id="@+id/lblResult"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="결과는 "
                android:textAppearance="?android:attr/textAppearanceLarge"/>

            <TextView
                android:id="@+id/value"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:textAppearance="?android:attr/textAppearanceLarge"/>
        </LinearLayout>
    </LinearLayout>
```

<img src="https://user-images.githubusercontent.com/69203345/137583454-3ae37010-eb67-4e3c-a0cb-481d13620651.png" alt="image" style="zoom: 80%;" />



MainActivity.java

```java
public class MainActivity extends AppCompatActivity {
    private RatingBar ratingBar;
    private TextView value;
    private Button button;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
        SetupRatingBar(); //함수 호출
        SetupButton();
    }
    private void SetupRatingBar() {
        ratingBar = (RatingBar) findViewById(R.id.ratingBar);
        value = (TextView) findViewById(R.id.value);
        
        ratingBar.setOnRatingBarChangeListener(new RatingBar.OnRatingBarChangeListener() {
            @Override
            public void onRatingChanged(RatingBar ratingBar, float v, boolean b) {
                value.setText(String.valueOf(v));
            }
        });
    }
    private void SetupButton() {
        ratingBar = (RatingBar) findViewById(R.id.ratingBar);
        button = (Button) findViewById(R.id.button);
        
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(getBaseContext(), String.valueOf(ratingBar.getRating()), Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```

실행화면

<img src="https://user-images.githubusercontent.com/69203345/137583597-f57cfee1-a839-4040-a5e2-27df8c5cbe53.png" alt="Screenshot_1634379269" style="zoom: 33%;" />

