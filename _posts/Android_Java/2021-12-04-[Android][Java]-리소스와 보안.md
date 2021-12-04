---
title:  "[Android][Java] 리소스와 보안, 서비스와 방송 수신자, 스레드"

categories: android_java
tags: [android_java]

toc: true
toc_sticky: true

date: 2021-12-04 12:39:54

---
# 리소스와 보안

## 리소스 
리소스(resource)란 이미지, 문자열, 레이아웃, 동영상 파일등을 의미한다  
리소스는 특별하게 이름 지어진 리소스 디렉토리에 모여 있어야 한다

### 리소스의 종류
|  디렉토리 |                                                       리소스 타입                                                      |
|:---------:|:----------------------------------------------------------------------------------------------------------------------:|
|   anim/   |                                           트윈 애니메이션을 정의하는 xml 파일                                          |
|   color/  |                                         컬러의 상태 리스트를 정의하는 xml 파일                                         |
| drawable/ |                             비트맵 파일이나 다음과 같은 리소스 타입으로 컴파일되는 xml파일                             |
|  layout/  |                                     사용자 인터페이스 레이아웃을 정의하는 xml 파일                                     |
|   menu/   |                                          애플리케이션 메뉴를 정의하는 xml 파일                                         |
|    raw/   |                                         시스템에 의하여 압축되지 않는 원본 파일                                        |
|  values/  |                           단순한 값을 저장하는 xml파일, 문자열, 정수, 색상등이 여기에 해당됨                           |
|    xml/   | 실행 시간에 Resource.getXML()을 호출하여서 읽을 수 있는 xml 파일. xml 구성(configuration) 파일은 여기에 저장되어야한다 |

## 기본 리소스와 대체 리소스
기본 리소스 (defalut resource)
- 장치 구성과 상관없이 기본적으로 사용되는 리소스이다
- 기본리소스만 있는 경우, 똑같은 레이아웃 사용됨

대체 리소스 (alternative resource)
- 대체 리소스는 특정한 장치 구성을 위하여 설계된 리소스이다
- 기본 리소스와 대체 리소스가 있는 경우, 장치의 크기에따라 서로 다른 레이아웃이 사용된다

### 대체 리소스를 제공하는 방법
- 기본 디렉토리 이름에 특정한 장치 구성의 이름을 붙인 디렉토리에 리소스들이 저장

![image](https://user-images.githubusercontent.com/69203345/144634605-188e8a3e-502f-4020-875b-76aac5ac1065.png)

## 참조 방법

- 코드에서 참조
  - R.리소스타입.리소스이름
  - R.string.hello 
- xml에서 참조
  - @리소스타입/리소스이름
  - @string/hello

![image](https://user-images.githubusercontent.com/69203345/144634963-156b6f00-7a33-4c53-8f4e-a242796e7ac8.png)

### 리소스 수식자

![image](https://user-images.githubusercontent.com/69203345/144635145-ae46860e-e32c-4c95-a55d-077d8e0de966.png)
![image](https://user-images.githubusercontent.com/69203345/144635234-81c5870e-b2c3-47f2-9d00-825c009ce3cc.png)

### 탐색과정

![image](https://user-images.githubusercontent.com/69203345/144635363-b7519e54-570c-4f65-99ce-2b07eb745dba.png)
![image](https://user-images.githubusercontent.com/69203345/144635466-4b814e60-477e-42f4-a8b0-6d5685a48e5f.png)

### 지역화
문자열이나 통화, 이미지 같은 여러 가지 리소스들을 사용자가 이쓴 지역에 따라 변경하는것

## 보안
- 안드로이드에서도 애플리케이션이 마음대로 시스템이나 다른 애플리케이션을 건드릴 수 있다면 심각한 위협
- 안드로이드에서 각 애플리케이션은 자신의 프로세스 안에서 실행
- 다른 애플리케이션을 건드릴 수 없다
  - Sandboxing

### 권한 요청하기
만약 애플리케이션이 보호된 기능이나 장치안의 데이터에 접근 하려면 AndroidManifest.xml 파일에 필요한 권한을 표시
- 태그 <uses-permission>을 사용

### 권한의 종류
![image](https://user-images.githubusercontent.com/69203345/144692946-8c51616b-51d9-4720-8f55-99ea2865b3d2.png)

# 서비스와 방송 수신자
- 사용자 인터페이스 없이 백그라운드에서 실행되는 컴포넌트
  - 배경음악을 재생
  - 웹사이트에서 주기적으로 데이터를 읽음
  - 주기적으로 폰의 사용량을 계산
  - 애플리케이션의 업데이트를 주기적으로 검사

## 서비스의 종류
시작 타입의 서비스(started service)
- 액티비티가 startedService()를 호출하여 서비스 시작

연결 타입의 서비스(bound service)
- 액티비티가 bindService()를 호출하여 서비스 시작

## 예제 
배경에서 음악을 연주하는 서비스  
음악파일 1개 필요 /res/raw/디렉토리에 저장

AndroidManifest.xml
서비스 부분 추가 해주기
```xml
        </activity>
        <service
            android:name=".MusicService"
            android:enabled="true" />
    </application>
```
activity_main.xml
```xml
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:gravity="top|center"
        android:orientation="vertical" >

        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center"
            android:padding="20dp"
            android:text="음악 서비스 테스트"
            android:textSize="20sp" />

        <Button
            android:id="@+id/start"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:text="시작" >
        </Button>

        <Button
            android:id="@+id/stop"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:text="중지" >
        </Button>

    </LinearLayout>
```
MainActivity.java
```java
public class MainActivity extends AppCompatActivity implements View.OnClickListener {
    private static final String TAG = "MusicService";
    Button start, stop;

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);

        start = (Button) findViewById(R.id.start);
        stop = (Button) findViewById(R.id.stop);

        start.setOnClickListener(this);
        stop.setOnClickListener(this);
    }

    public void onClick(View src) {
        switch (src.getId()) {
            case R.id.start:
                Log.d(TAG, "onClick() start ");
                startService(new Intent(this, MusicService.class));
                break;
            case R.id.stop:
                Log.d(TAG, "onClick() stop");
                stopService(new Intent(this, MusicService.class));
                break;
        }
    }
}
```
MusicService.java
```java
public class MusicService extends Service {
	private static final String TAG = "MusicService";
	MediaPlayer player;

	@Override
	public IBinder onBind(Intent intent) {
		return null;
	}

	@Override
	public void onCreate() {
		Log.d(TAG, "onCreate()");

		player = MediaPlayer.create(this, R.raw.old_pop);
		player.setLooping(false); // Set looping
	}

	@Override
	public void onDestroy() {
		Toast.makeText(this, "Music Service가 중지되었습니다.", Toast.LENGTH_LONG)
				.show();
		Log.d(TAG, "onDestroy()");
		player.stop();
	}

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        Toast.makeText(this, "Music Service가 시작되었습니다.", Toast.LENGTH_LONG)
                .show();
        Log.d(TAG, "onStart()");
        player.start();
        return super.onStartCommand(intent, flags, startId);
    }
}
```
실행

<img src="https://user-images.githubusercontent.com/69203345/144694144-cea79e28-df91-4a8b-a2e0-f446953b2d0a.png" alt="Screenshot_1638585911" style="zoom:30%;" />

# 스레드

## 다중 스레딩
- 하나의 애플리케이션이 동시에 여러가지 작업을 하는것
- 이들 작업은 스레드(thread) 라고 불린다

## 안드로이드에서의 프로세스와 스레드
애플리케이션이 시작되면 안드로이드 시스템은 새로운 리눅스 프로세스를 실행한다  
기본적으로 애플리케이션 안의 모든 컴포넌트들은 동일한 프로세스의 동일한 스레드로 실행된다  
이 기본적인 스레드를 메인 스레드(main thread)라고 부른다

## 메인 스레드
메인 스레드는 사용자 인터페이스 위젯에게 이벤트를 전달하거나 화면을 그리는 작업을 담당
UI스레드(user interface thread)라고도 불림

## 안드로이드의 단일 스레드 모델 원칙

UI스레드는 블록시키면 안된다  
UI스레드 외부에서 안드로이드 UI툴킷을 조작하면 안된다

## 작업 작업스레드
별도로 생성되는 스레드  
배경 스레드(background thread)라고도 불림

### 작업 스레드를 작성한는 방법
Thread 클래스를 상속받아서 스레드 작성  
Runnable 인터페이스를 구현한후에 Thread 객체에 전달

## 예제 
Thread 상속방법
MainActivity.java
```java
public class MainActivity extends AppCompatActivity {

    WorkerThread w;
    boolean running = true;

    class WorkerThread extends Thread {
        public void run() {
            int i = 0;
            for (i = 0; i < 20 && running; i++) {
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                }
                Log.v("THREAD", "time=" + i);
            }
        }
    }

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    @Override
    public void onStart() {
        super.onStart();
        w = new WorkerThread();
        running = true;
        w.start();
    }

    @Override
    public void onStop() {
        super.onStop();
        running = false;
    }
}
```

실행  
logcat 확인  
![image](https://user-images.githubusercontent.com/69203345/144694778-55f4f044-ce54-49af-88c0-40adee8f57cf.png)

## 예제
Runnable 인터페이스 사용

MainActivity.java
```java
public class MainActivity extends AppCompatActivity {
    Thread w;
    boolean running = true;

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    @Override
    public void onStart() {
        super.onStart();
        w = new Thread(new Runnable() {
            public void run() {
                int i = 0;
                for (i = 0; i < 20 && running; i++) {
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                    }
                    Log.v("THREAD", "time=" + i);
                }
            }
        });
        running = true;
        w.start();
    }

    @Override
    public void onStop() {
        super.onStop();
        running = false;
    }
}
```

실행  
logcat확인  
![image](https://user-images.githubusercontent.com/69203345/144694973-ebf24ec4-f795-4d2f-aa49-dd1bf09dcada.png)

### 주의할점
스레드에서 직접적으로 사용자 인터페이스 위젯을 변경하면 안된다  

**해결방법 3가지**
- Activity.runOnUiThread(Runnable)
- View.post(Runnable)
- View.postDelayed(Runnable.long)

## Handler 클래스를 사용한 예제
Handler 클래스 - Runnable 객체를 UI스레드로 보낼 수 있음

activity_main.xml
```xml
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        android:orientation="vertical" >

        <TextView
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:text="Progress Bar Test" />

        <ProgressBar
            android:id="@+id/progress_bar"
            style="?android:attr/progressBarStyleHorizontal"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content" >
        </ProgressBar>

    </LinearLayout>
```

Mainactivity.java
```java
public class MainActivity extends AppCompatActivity {

    private static final int PROGRESS = 0x1;
    private ProgressBar mProgress;
    private int mProgressStatus = 0;
    private Handler mHandler = new Handler();
    int i = 0;

    protected void onCreate(Bundle icicle) {
        super.onCreate(icicle);
        setContentView(R.layout.activity_main);
        mProgress = (ProgressBar) findViewById(R.id.progress_bar);

        // Start lengthy operation in a background thread
        new Thread(new Runnable() {//작업스레드가 무명클래스로 정의됨
            public void run() {
                while (mProgressStatus < 100) {
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                    }
                    mProgressStatus = i++;

                    // Update the progress bar
                    mHandler.post(new Runnable() {//UI를 업데이트하는 러너블 객체를 전송
                        public void run() {
                            mProgress.setProgress(mProgressStatus);
                        }
                    });
                }
            }
        }).start();
    }
}
```
실행

<img src="https://user-images.githubusercontent.com/69203345/144695563-2bbee5d8-946b-4b89-bdc5-1ddef4829367.png" alt="Screenshot_1638588915" style="zoom:30%;" />