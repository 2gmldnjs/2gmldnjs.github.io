---
title:  "[Android][Java] 메뉴예시, 대화상자"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-10-10 21:55:11

---

# 사용자 인터페이스

## 사용자 인터페이스 종류

- 네비게이션 바
- 액션바
- 다중 패널 레이아웃
- 제스처

### 메뉴의 종류

옵션 메뉴: 사용자가 menu 키를 누를때 나타남

컨텍스트 메뉴: 컨텍스트 메뉴는 사용자가 화면을 일정 시간 이상으로 길게 누르면 나타나는 메뉴

팝업 메뉴

### 메뉴의 생성 방법

뷰, 위젯 생성과 마찬가지로 

- 코드로 메뉴 생성
- xml로 메뉴 생성 

가능하다

menu 엘리먼트는 menu를 생성하고 메뉴 항목들을 담는 컨테이너가 된다, 반드시 루트노드 여야하며 item 이나 group 을 하나 이상 포함 한다

item 엘리먼트는 menuitem을 생성한다. 이것은 하나의  메뉴항목을 나타내고, 서브메뉴를 작성하려면 menu를 포함할 수 있다

### 옵션메뉴

- 현재 액티비티와 관련된 동작

ex) 옵션 메뉴 생성

- 메뉴를 나타내는 xml 파일 생성

![image](https://user-images.githubusercontent.com/69203345/136686674-c2d01602-7b6e-49f2-9846-fec8f243fb11.png)

디자인 수정

<img src="https://user-images.githubusercontent.com/69203345/136686698-6671c154-7bfd-4104-aa1a-b7d7b7e0a506.png" alt="image" style="zoom:80%;" />

![image](https://user-images.githubusercontent.com/69203345/136686711-fc111f10-c7d8-4b91-a3e5-a6e9fdfcd788.png)

java 파일 코드 추가

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
//////////////////// 추가 ////////////////////
    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        MenuInflater inflater = getMenuInflater(); //객체 생성, 초기화
        inflater.inflate(R.menu.mymenu,menu); //메뉴 디렉토레의 mymenu를 팽창하여 menu 객체로 만든다
        return super.onCreateOptionsMenu(menu);
    }
}
```

이벤트 처리 코드

```java
    @Override
    public boolean onOptionsItemSelected(@NonNull MenuItem item) {
        switch (item.getItemId()){
            case R.id.apple:
                Toast.makeText(this, "사과", Toast.LENGTH_SHORT).show();
                return true;
            case R.id.grape:
                Toast.makeText(this,"포도", Toast.LENGTH_SHORT).show();
                return true;
            case R.id.banana:
                Toast.makeText(this,"바나나",Toast.LENGTH_SHORT).show();
                return true;
        }
        return super.onOptionsItemSelected(item);
    }
```

실행화면 

바나나 옵션 클릭시

<img src="https://user-images.githubusercontent.com/69203345/136687089-6b4a4095-0942-4385-817f-01a61ad151ed.png" alt="image" style="zoom:80%;" />

<img src="https://user-images.githubusercontent.com/69203345/136686929-e4e6e2a6-bbc7-4d24-af56-0910acb81d04.png" alt="image" style="zoom:80%;" />

### 컨텍스트 메뉴

UI의 어떤 항목과 관련된 동작

사용자가 항목위에서 오래 누르기를 하면 컨텍스트 메뉴가 표시

pc에서 마우스 오른쪽 버튼을 눌렀을 때 나오는 메뉴와 개념적으로 유사



플로팅 컨텍스트 메뉴:

사용자가 항목 위에서 오래 누르기(long click)을 하면 메뉴가 대화상자처럼 떠서 표시됨



컨텍스트 액션 모드:

현재 선택된 항목에 관련된 메뉴가 액션바에 표시된다. 여러 항목을 선택하여 특정한 액션을 한꺼번에 적용가능

ex) 플로팅 컨텍스트

<img src="https://user-images.githubusercontent.com/69203345/136688119-331c9fb3-77f2-46e7-ab99-08a770df17d7.png" alt="image" style="zoom:80%;" />

![image](https://user-images.githubusercontent.com/69203345/136688135-3ff6ce55-8e86-43b9-ad90-69625d75a895.png)

text 내용은 아무거나!

java 코드 

```java
public class MainActivity extends AppCompatActivity {
    TextView text; //
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
///////////////////// 추가 /////////////////
        text = (TextView) findViewById(R.id.textView); //findViewById로 알아낸 textView를 text에 저장
       registerForContextMenu(text); //ContextMenu에 text를 저장
    }

    @Override
    public void onCreateContextMenu(ContextMenu menu, View v, ContextMenu.ContextMenuInfo menuInfo) {
        menu.setHeaderTitle("컨텍스트 메뉴");
        menu.add(0,1,0,"배경색: red");
        menu.add(0,2,0,"배경색: green");
        menu.add(0,3,0,"배경색: blue");

        super.onCreateContextMenu(menu, v, menuInfo);

    }
        @Override
    public boolean onContextItemSelected(@NonNull MenuItem item) {
        switch (item.getItemId()){
            case 1:
                text.setBackgroundColor(Color.RED);
                return true;
            case 2:
                text.setBackgroundColor(Color.GREEN);
                return true;
            case 3:
                text.setBackgroundColor(Color.BLUE);
                return true;
            default:
                return super.onContextItemSelected(item);
                
        }
    }
}
```

실행화면

텍스트를 길게 누르면 컨텍스트 메뉴가 뜬다

<img src="https://user-images.githubusercontent.com/69203345/136688371-4743c956-15e9-44fc-8c49-9ef7a5280282.png" alt="image" style="zoom:80%;" />

<img src="https://user-images.githubusercontent.com/69203345/136688411-80089cfd-13f6-4579-80f7-9412b8848a53.png" alt="image" style="zoom:80%;" />

### 팝업 메뉴

뷰에 부착된 모달 메뉴(modal menu)

API 레벨 11부터 제공

팝업 메뉴의 용도

- 오버플로우 스타일 메뉴 제공
- 서브메뉴의 역할
- 드롭다운 메뉴

디자인

![image](https://user-images.githubusercontent.com/69203345/136692586-aa8fd55b-69c6-49ab-bdf6-869c41fb8946.png)

<img src="https://user-images.githubusercontent.com/69203345/136692609-430a316b-9a0f-45e9-9596-5791551d64de.png" alt="image" style="zoom:80%;" />

![image](https://user-images.githubusercontent.com/69203345/136692617-ba91263b-4c81-4663-9d1e-bd605b2bd1ea.png)

activity_main.xml 디자인

버튼에서 onClick 속성을 지정

![image](https://user-images.githubusercontent.com/69203345/136692702-941b1124-ce53-4ffb-95bf-75b132c37000.png)

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
    /////////// onClick 속성에 적은 값으로 작성 //////////
    public void onClick(View button) {
        PopupMenu popup = new PopupMenu(this, button);
        popup.getMenuInflater().inflate(R.menu.popup, popup.getMenu());

        popup.setOnMenuItemClickListener( //리스너를 이용한 무명 클래스
                new PopupMenu.OnMenuItemClickListener() {
                    public boolean onMenuItemClick(MenuItem item) {
                        Toast.makeText(getApplicationContext(), "클릭된 팝업 메뉴: "
                                        + item.getTitle(),
                                Toast.LENGTH_SHORT).show();
                        return true;
                    }
                });

        popup.show();
    }
}
```

실행화면

버튼을 클릭시 팝업 메뉴를 팽창(inflate)해서 보여줌

<img src="https://user-images.githubusercontent.com/69203345/136693103-91b90286-5e5d-4449-889d-16b1ba3b1e8b.png" alt="image" style="zoom:80%;" />

클릭시 토스트 메세지 띄워줌

<img src="https://user-images.githubusercontent.com/69203345/136693170-de03b9b4-561f-4ada-a02b-e8669d000b80.png" alt="image" style="zoom:80%;" />

옵션메뉴와 팝업 메뉴는 inflate를 시키고 컨텍스트 메뉴는 시키지 않고 일반적으로 자바 코드에서 사용한다

### 액션바

애플리케이션의 로고 표시

탭이나 드롭다운 리스트를 이용해 내비게이션 메뉴와 뷰 젼환 기능을 제공

옵션메뉴를 사용

디자인

![image](https://user-images.githubusercontent.com/69203345/136694184-761e70ca-c782-4e66-b400-c65d68d3306e.png)

<img src="https://user-images.githubusercontent.com/69203345/136694231-ad6af614-ad91-4f6c-8153-ae2e5447471b.png" alt="image" style="zoom:80%;" />

![image](https://user-images.githubusercontent.com/69203345/136694261-fe68985e-b7aa-406b-840b-8bf518b4055e.png)

MainActivity.java

```java
    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        //메뉴 리소스 팽창, 액션바에 항목들 추가
        getMenuInflater().inflate(R.menu.action_bar,menu); //menu에 inflate
        return super.onCreateOptionsMenu(menu);
    }

    @Override
    public boolean onOptionsItemSelected(@NonNull MenuItem item) {
        switch (item.getItemId()){
            case R.id.action_refresh:
                Toast.makeText(this, "refresh", Toast.LENGTH_SHORT).show();
                return true;
            case R.id.action_search:
                Toast.makeText(this,"search",Toast.LENGTH_SHORT).show();
                return true;
            case R.id.action_setting:
                Toast.makeText(this,"settings",Toast.LENGTH_SHORT).show();
                return true;
            default:
                return super.onOptionsItemSelected(item);
        }

    }
}
```

실행화면

<img src="https://user-images.githubusercontent.com/69203345/136694323-1b5689d4-ab99-44a9-8b64-15fb10e00fbb.png" alt="image" style="zoom:80%;" />

<img src="https://user-images.githubusercontent.com/69203345/136694338-2edb07eb-c027-478f-9a31-b8596724eb40.png" alt="image" style="zoom:80%;" />

## 대화상자

대화상자(dialog)는 사용자에게 메시지를 출력하고 사용자로 부터 입력을 받아들이는 아주 보편적인 사용자 인터페이스

종류

- AlertDialog
- ProgressDialog
- DatePickerDialog
- TimePickerDialog

## AlertDialog

activity_main.xml

<img src="https://user-images.githubusercontent.com/69203345/136694871-9a393137-75c0-4a52-b9af-7dce63f9f7f0.png" alt="image" style="zoom:80%;" />

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    public void open(View view){
        AlertDialog.Builder alertDialogBuilder = new AlertDialog.Builder(this); //alertdialog를 만들려면 있어야함
        alertDialogBuilder.setMessage("결제하시겠습니까?");
        alertDialogBuilder.setPositiveButton("yes",
                new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface arg0, int arg1) {
                        Toast.makeText(MainActivity.this,"결제가 완료되었습니다.",Toast.LENGTH_LONG).show();
                    }
                });

        alertDialogBuilder.setNegativeButton("No",new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                Toast.makeText(MainActivity.this,"결제가 취소되었습니다.",Toast.LENGTH_LONG).show();
                finish();
            }
        });

        AlertDialog alertDialog = alertDialogBuilder.create();
        alertDialog.show();
    }
}

```

실행화면

<img src="https://user-images.githubusercontent.com/69203345/136694943-4e817bb4-c8d6-4b2a-ba0d-7745f6000fe3.png" alt="image" style="zoom:80%;" />

## DatePickerDialog

날짜와 시간을 입력받는 대화상자

<img src="https://user-images.githubusercontent.com/69203345/136695285-c2f1b619-2f9e-4cb3-b136-78db3446cf9a.png" alt="image" style="zoom:80%;" />

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {
    Button btnSelectDate, btnSelectTime;//객체 생성
    DatePickerDialog datePickerDialog;
    TimePickerDialog timePickerDialog;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState); //이전 화면으로 돌아가기 위해서 이전 상태 저장해놓음
        setContentView(R.layout.activity_main); //activity_main.xml로 구성 하시오
        btnSelectDate = (Button) findViewById(R.id.button); //객체에 저장
        btnSelectTime = (Button) findViewById(R.id.button2);
    }
    public void onClick(View v) { //함수
        if (v == btnSelectDate) {
            final Calendar c = Calendar.getInstance(); //현재 시간을 얻기위해 객체를 만듦
            int mYear = c.get(Calendar.YEAR);
            int mMonth = c.get(Calendar.MONTH);
            int mDay = c.get(Calendar.DAY_OF_MONTH);

            DatePickerDialog datePickerDialog = new DatePickerDialog(this,
                    new DatePickerDialog.OnDateSetListener() {
                        @Override
                        public void onDateSet(DatePicker view, int year,
                                              int monthOfYear, int dayOfMonth) {
                            btnSelectDate.setText(dayOfMonth + "/" + (monthOfYear + 1) + "/" + year);
                        }
                    }, mYear, mMonth, mDay);
            datePickerDialog.show();
        }
        if (v == btnSelectTime) { //위와 유사
            final Calendar c = Calendar.getInstance();
            int mHour = c.get(Calendar.HOUR_OF_DAY);
            int mMinute = c.get(Calendar.MINUTE);

            TimePickerDialog timePickerDialog = new TimePickerDialog(this,
                    new TimePickerDialog.OnTimeSetListener() {
                        @Override
                        public void onTimeSet(TimePicker view, int hourOfDay,
                                              int minute) {
                            btnSelectTime.setText(hourOfDay + ":" + minute);
                        }
                    }, mHour, mMinute, false);
            timePickerDialog.show();
        }
    }
}
```

실행화면

<img src="https://user-images.githubusercontent.com/69203345/136695614-745f7bc9-69fa-4778-86c4-f851b0c1ad58.png" alt="image" style="zoom:80%;" />

<img src="https://user-images.githubusercontent.com/69203345/136695642-1c8ebdbe-c036-4263-ad03-9ea8cd2fe7df.png" alt="image" style="zoom:80%;" />

<img src="https://user-images.githubusercontent.com/69203345/136695673-b3edee78-442e-4014-b68c-8ab4e2066153.png" alt="image" style="zoom:80%;" />

## 알림기능

어떤 이벤트가 발생했을때 앱이 사용자에게 전달하는 메시지 이다

디자인은 버튼하나만 생성, onClick 속성 주기

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {
    String NOTIFICATION_CHANNEL_ID = "my_channel_id_01";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
    public void sendNotification(View view) {
        NotificationCompat.Builder notificationBuilder = new NotificationCompat.Builder(this, NOTIFICATION_CHANNEL_ID);

        // 알림이 클릭되면 이 인텐트가 보내진다.
        Intent intent = new Intent(Intent.ACTION_VIEW,
                Uri.parse("http://www.google.com/"));
        PendingIntent pendingIntent = PendingIntent.getActivity(this, 0,
                intent, 0);

        notificationBuilder.setSmallIcon(R.mipmap.ic_launcher)
                .setContentTitle("메일 알림")
                .setContentText("새로운 메일이 도착하였습니다.")
                .setContentIntent(pendingIntent);

        NotificationManager notificationManager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
        notificationManager.notify(/*notification id*/1, notificationBuilder.build());
    }
}
```

실행화면

<img src="https://user-images.githubusercontent.com/69203345/136696567-61336834-ce36-43c9-ae91-4d16eea7555c.png" alt="image" style="zoom:80%;" />

알림생성시

<img src="https://user-images.githubusercontent.com/69203345/136696590-f0c589a7-441e-47ad-a756-90a88c4f2ec3.png" alt="image" style="zoom:80%;" />



