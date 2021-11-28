---
title:  "[Android][Java] 연습문제-캘린더뷰,타임피커"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-11-21 22:41:43


---

# 연습문제

구성

<img src="https://user-images.githubusercontent.com/69203345/142764354-0a377d5c-a19d-4767-8e08-b156ae451dc6.png" alt="image" style="zoom: 67%;" />

날짜 설정은 캘린더뷰

시간 설정은 타임 피커     

​     

작동

타이머 기능 : 예약 시작과 예약완료를 클릭하면 크로노미터가 타이머로 동작

날짜/ 시간 설정 : 날짜 설정과 시간 설정을 클릭하면 예약할 날짜와 시간 변경

날짜/ 시간 결정 : 예약 완료를 클릭하면 설정한 날짜와 시간 결정



activity_main.xml

```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical">

            <Chronometer
                android:id="@+id/chronometer1"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:format="예약에 걸린 시간 %s"
                android:gravity="center"
                android:textSize="20sp" />

            <Button
                android:id="@+id/btnStart"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:text="예약 시작" />

        </LinearLayout>

        <RadioGroup
            android:layout_width="match_parent"
            android:layout_height="wrap_content">

            <RadioButton
                android:id="@+id/rdoCal"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:text="날짜 설정(캘린더 뷰)" />

            <RadioButton
                android:id="@+id/rdoTime"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:text="시간 설정" />
        </RadioGroup>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:orientation="vertical">

            <FrameLayout
                android:layout_width="wrap_content"
                android:layout_height="wrap_content">

                <CalendarView
                    android:id="@+id/calendarView1"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent" />

                <TimePicker
                    android:id="@+id/timePicker1"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent" />
            </FrameLayout>
        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="horizontal">

            <Button
                android:id="@+id/btnEnd"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="예약 완료" />

            <TextView
                android:id="@+id/tvYear"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="0000" />

            <TextView
                android:id="@+id/textView2"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="년" />

            <TextView
                android:id="@+id/tvMonth"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="00" />

            <TextView
                android:id="@+id/textView4"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="월" />

            <TextView
                android:id="@+id/tvDay"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="00" />

            <TextView
                android:id="@+id/textView6"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="일" />

            <TextView
                android:id="@+id/tvHour"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="00" />

            <TextView
                android:id="@+id/textView8"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="시" />

            <TextView
                android:id="@+id/tvMinute"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="00" />

            <TextView
                android:id="@+id/textView10"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="분 예약됨" />
        </LinearLayout>
    </LinearLayout>

```

MainActivity.java

```java
public class MainActivity extends AppCompatActivity {
    Chronometer chrono;
    Button btnStart, btnEnd;
    RadioButton rdoCal, rdoTime;
    CalendarView calView;
    TimePicker tPicker;
    TextView tvYear, tvMonth, tvDay, tvHour, tvMinute;
    int SelectYear, SelectMonth, SelectDay;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        setTitle("시간 예약");
        btnStart = (Button) findViewById(R.id.btnStart);
        btnEnd = (Button) findViewById(R.id.btnEnd);

        chrono = (Chronometer) findViewById(R.id.chronometer1);

        rdoCal = (RadioButton) findViewById(R.id.rdoCal);
        rdoTime = (RadioButton) findViewById(R.id.rdoTime);

        calView = (CalendarView) findViewById(R.id.calendarView1);
        tPicker = (TimePicker) findViewById(R.id.timePicker1);

        tvYear = (TextView) findViewById(R.id.tvYear);
        tvMonth = (TextView) findViewById(R.id.tvMonth);
        tvDay = (TextView) findViewById(R.id.tvDay);
        tvHour = (TextView) findViewById(R.id.tvHour);
        tvMinute = (TextView) findViewById(R.id.tvMinute);

        calView.setVisibility(View.INVISIBLE);
        tPicker.setVisibility(View.INVISIBLE);

        rdoCal.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                calView.setVisibility(View.VISIBLE);
                tPicker.setVisibility(View.INVISIBLE);
            }
        });
        rdoTime.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                calView.setVisibility(View.INVISIBLE);
                tPicker.setVisibility(View.VISIBLE);
            }
        });

        btnStart.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                chrono.setBase(SystemClock.elapsedRealtime());
                chrono.start();
                chrono.setTextColor(Color.RED);
            }
        });
        btnEnd.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                chrono.stop();
                chrono.setTextColor(Color.BLUE);

                tvYear.setText(Integer.toString(SelectYear));
                tvMonth.setText(Integer.toString(SelectMonth));
                tvDay.setText(Integer.toString(SelectDay));
                tvHour.setText(Integer.toString(tPicker.getCurrentHour()));
                tvMinute.setText(Integer.toString(tPicker.getCurrentMinute()));
                
            }
        });

        calView.setOnDateChangeListener(new CalendarView.OnDateChangeListener() {
            @Override
            public void onSelectedDayChange(@NonNull CalendarView calendarView, int i, int i1, int i2) {
                SelectYear = i;
                SelectMonth = i1+1;
                SelectDay = i2;
            }
        });

    }
}
```

실행

<img src="https://user-images.githubusercontent.com/69203345/142767832-79dc57bd-4d7a-4961-a9fa-426447508415.png" alt="Screenshot_1637507870" style="zoom:33%;" />

