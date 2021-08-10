---
title:  "[Python] 예외처리,finally"

categories: python
tags: python

toc: true
toc_sticky: true

date: 2021-08-10 22:43:06
---

# 예외처리

어떠한 에러에 대한 처리

try:

except 에러:

```python
try:
    print ("나누기 전용 계산기 입니다")
    nums = []
    nums.append(int(input("첫번째 숫자를 입력하세요 : ")))
    nums.append(int(input("두번째 숫자를 입력하세요 : ")))
    #nums.append(int(nums[0]/nums[1])) #주석 일때 아닐때 둘다 해보기
    print ("{} / {} = {}".format(nums[0], nums[1],nums[2]))    
except ValueError:
    print("에러! 잘못된 값을 입력했습니다")
except ZeroDivisionError as err:
    print (err)
except Exception as err:
    print("알수없는 에러가 발생")
    print (err)
```

## 에러 발생시키기

```python
try:
    print("한 자리 숫자 나누기 전용 계산기 입니다")
    num1 = (int(input("첫번째 숫자를 입력하세요 : ")))
    num2 = (int(input("두번째 숫자를 입력하세요 : ")))
    if num1>=10 or num2>=10:
        raise ValueError #에러로 넘겨주기
    print ("{} / {} = {}".format(num1, num2,int(num1/num2)))
except ValueError:
    print("잘못된 값을 입력 하였습니다. 한자리 숫자만 입력하세요")    
```

## 사용자 정의 에러

```python
class BigNumberError(Exception):#사용자 정의 에러
    def __init__(self,msg):
        self.msg = msg

    def __str__(self):
        return self.msg

try:
    print("한 자리 숫자 나누기 전용 계산기 입니다")
    num1 = (int(input("첫번째 숫자를 입력하세요 : ")))
    num2 = (int(input("두번째 숫자를 입력하세요 : ")))
    if num1>=10 or num2>=10:
        raise BigNumberError("입력값 : {}, {}".format(num1, num2)) #에러 넘겨줌
    print ("{} / {} = {}".format(num1, num2,int(num1/num2)))
except ValueError:
    print("잘못된 값을 입력 하였습니다. 한자리 숫자만 입력하세요")    
except BigNumberError as err:
    print("에러가 발생하였습니다. 한자리 숫자만 입력하세요")    
    print(err)
    #사용자 정의 에러가 떳을때 어떤 메세지를 띄울지 정의해줌

```

\사용자가정의한 에러에대해서 어떤 메세지를 띄울지도 정의 가능

## finally

```python
class BigNumberError(Exception):
    def __init__(self,msg):
        self.msg = msg

    def __str__(self):
        return self.msg

try:
    print("한 자리 숫자 나누기 전용 계산기 입니다")
    num1 = (int(input("첫번째 숫자를 입력하세요 : ")))
    num2 = (int(input("두번째 숫자를 입력하세요 : ")))
    if num1>=10 or num2>=10:
        raise BigNumberError("입력값 : {}, {}".format(num1, num2)) #에러
    print ("{} / {} = {}".format(num1, num2,int(num1/num2)))
except ValueError:
    print("잘못된 값을 입력 하였습니다. 한자리 숫자만 입력하세요")    
except BigNumberError as err:
    print("에러가 발생하였습니다. 한자리 숫자만 입력하세요")    
    print(err)
finally: #에러가 떠도 안떠도 무조건 실행
    print("계산기를 이용해주셔서 감사합니다")

```

# 퀴즈

```python
'''
동네에 항상 대기 손님이 있는 치킨집이 있습니다
대기 손님의 시간을 줄이고자 자동 주문 시스템을 제작합니다
시스템 코드를 확인하고 적절한 예외처리 구문을 넣으시오

조건1 : 1보다 작거나 숫자가 아닌 입력밧이 들어올 때는 ValueError로 처리
        출력 메세지 : "잘못된 값을 입력하였습니다"
조건2 : 대기 손님이 주문할 수 있는 총 치킨량은 10마리로 한정
        치킨 소진 시 사용자 정의 에러[SoldOutError]를 발생시키고 프로그램 종료
        출력 메세지 : "재고가 소진되어 더 이상 주문을 받지 않습니다"
#[코드]
chicken=10
waiting = 1 #홀 안에는 현재 만석, 대기번호 1부터 시작
while(True):
    print("[남은 치킨 : {}]".format(chicken))
    order = int(input("치킨 몇마리 주문하시겠습니까? "))
    if order > chicken: #남은 치킨보다 주문량이 많을때
        print("재료가 부족합니다")
    else:
        print("[대기번호 {}] {}마리 주문이 완료되었습니다".format(waiting,order))
        waiting +=1
        chicken -=order
'''
class SoldOutError(Exception):
    pass

chicken=10
waiting = 1 #홀 안에는 현재 만석, 대기번호 1부터 시작
while(True):
    try:
        print("[남은 치킨 : {}]".format(chicken))
        order = int(input("치킨 몇마리 주문하시겠습니까? "))
        if order > chicken: #남은 치킨보다 주문량이 많을때
            print("재료가 부족합니다")
        elif order <=0: #-1,-2..마리 일때 에러
            raise ValueError #에러 만들어줌
        else:
            print("[대기번호 {}] {}마리 주문이 완료되었습니다".format(waiting,order))
            waiting +=1
            chicken -=order
        if chicken ==0:
            raise SoldOutError
    except ValueError:
        print("잘못된 값을 입력하였습니다")
    except SoldOutError: #사용자 정의 에러
        print("재고가 소진되어 더 이상 주문을 받지 않습니다")
        break
```

