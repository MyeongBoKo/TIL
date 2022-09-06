# 날짜와 시간
## Calendar와 Date
1. java.util.Date
- 날짜와 시간을 다룰 목적으로 만들어진 클래스(JDK1.0)
- Date의 메서드는 거의 deprecated(앞으로 사용하지 말아라)되었지만, 여전히 쓰이고 있다.
2. java.util.Calendar
- Date클래스를 개선한 새로운 클래스(JDK1.1). 여전히 단점(날짜와 시간이 같이 다룬다는 점)이 존재
3. java.tile패키지
- Date와 calendar의 단점을 개선한 새로운 클래스들을 제공(JDK1.8)
- 날짜와 시간을 같이 다루거나(LocalDateTime) 혹은 따로 사용할 수 있도록 클래스(LocalDate, LocalTime)를 나눠놓음.

## Calendar클래스
1. get()으로 날짜와 시간 필드 가져오기 - int get(int field)
2. getAntualMaximul()으로 그 달의 마지막 요일 가져오기
3. set()를 통해서 우리가 원하는 날짜나 시간으로 바꿀수 있다.

### 1.get()으로 날짜와 시간지정하기 (예제10-1)
```java
Calendar cal = Calendar.getInstance();  // 현재 날짜와 시간으로 셋팅됨
int thisYear = cal.get(Calendar.Year);  // 올해가 몇년인지 알아낸다.
int lastDayOfMonth = cal.getActualMaximum(Calendar.Date);   // 이 달의 마지막날
```
필드명(날짜) | 설명
--|--
Year|년
MONTH|  월(0부터 시작), 0이면 1월을 의미
WEEK_OF_YEAR|1월 1일 ~ 지금까지 몇 번째 주
WEEK_OF_MONTH|그 달의 몇 번째 주
DATE|일
DAY_OF_MONTH|그 달의 몇 번째일
DAY_OF_YEAR|그 해의 몇 번째일
DAY_OF_WEEK|요일(1~7, 1:일요일)
DAY_OF_WEEK_IN_MONTH|그 달의 몇 번째 요일

필드명(시간) | 설명
--|--
HOUR|시간(0~11)
HOUR_OF_DAY|시간(0~23)
MINUTE|분
SECOND|초
MILLISECOND|천분의 일초(1/1000)
ZONE_OFFSEF|GMT기준 시차(천분의 일초 단위), 시간대
AM_PM|오전/오후

### 2.set()으로 날짜와 시긴지정하기(예제 10-2)
```java
void set(int field, int value)
void set(int year, int month, int date) // 년 월 일
void set(int year, int month, int date, int hourOfDay, int minute, int second) // 년 월 일 시 분 초
```
### set() 날짜 지정하는 방법, 월(MONTH)이 0부터 시작한다는 점에 주의
```java
Calendar date1 = Calendar.getInstance();
date1.set(2022, 8, 06);     // 2022년 9월 6일 (이떄 8월 아닌 것을 주의해야 한다.)
// 배열을 이용하기 때문에 0부터 시작한다.

// date1.set(Calendar.Year, 2022);
// date1.set(Calendar.MONTH, 8);
// date1.set(Calendar.DATE, 06);
```

### set() 시간 지정하는 방법
```java
Calendar time1 = Calendar.getInstance();

time1.set(Calendar.HOUR_OF_DAY, 10);    .// time1을 10시 20분 30초로 설정
time1.set(Calendar.MINUTE, 20);
time1.set(Calendar.SECOND, 30);
```

### 날짜와 다른 날짜 간의 차이를 구할 때
- 초로 변환한 후의 차이 값을 구한다.
- 초로 나타난 결과 값을 원하는 시간으로 변환해서 나타낸다.
- getTimeInMillis()메서는 천분의 일초 단위로 변환하기 때문에 1000을 나눠야 초로 나타낼 수 있다.

### 3.clear() 초기화하기
- Calendar 객체의 모든 필드를 초기화
```java
Calendar dt = Calendar.getInstance();   // 현재 시간

// Tue Aug 29 07:13:03 KST 2017
System.out.println(new Date(dt.getTimeInMillis()));

dt.clear(); // 모든 필드를 초기화
// Thu Jan 01 00:00:00 KST 1970 (EPOCH TIME(기준))
System.out.println(new Date(dt.getTimeInMillis()));
```

- Calendar 객체의 특정 필드를 초기화
```java
Calendar dt = Calendar.getInstance();

// Tue Aug 29 07:13:03 KST 2017
System.out.println(new Date(dt.getTimeInMillis()));

dt.clear(Calendar.SECOND);      // 초를 초기화
dt.clear(Calendar.MINUTE);      // 분을 초기화
dt.clear(Calendar.HOUR_OF_DAY); // 시간을 초기화
dt.clear(Calendar.HOUR);        // 시간을 초기화

// Thu Jan 01 00:00:00 KST 1970 (EPOCH TIME(기준))
System.out.println(new Date(dt.getTimeInMillis()));
```
- 객체를 생성한 후에 꼭 clear를 해줘야 한다. 그 후에 set()을 사용해야 값이 정확하게 나온다.

### <요약>
1. get() - 필드 읽기
2. set() - 필드 변경
3. clear() - 필드 초기화

### 4. add() 특정 필드의 값을 증가 또는 감소(다른 필드에 영향O)
```java
Calendar date = Calendar.getInstance();
date.claer();   // 모든 필드를 초기화
date.set(2020, 7, 31);  // 2020년 8월 31일로 설정

date.add(Calendar.Date, 1);     // 날짜(Date)에 1을 더한다.
date.add(Calendar.MONTH, -8);   // 월(MONTH)에서 8을 뺀다.
```
- 날짜에 1을 더해서 월도 바뀌는 것을 알 수 있다. 즉, 일 필드의 변화가 월 필드의 변화에 영향을 주었다.

### 5. roll()은 특정필드의 값을 증가 또는 감소(다른 필드에 영향X)
```java
date.set(2020, 7, 31);  // 2020년 8월 31일로 설정

// add()와 달리 roll()은 다른 필드에 영향을 미치지 않는다.
date.roll(Calendar.DATE, 1);    // 날짜(Date)에 1을 더한다.
date.roll(Calendar.MONTH, -8);  // 월(MONTH)에서 8을 뺀다
```
- 일 필드의 변화가 월 필드의 변화에 영향을 주지 않는다.

## Date와 Calendar간의 변환
- Date의 메서드는 대부분 deprecated(사용하지 않을 것을 권장)되었지만 여전히 사용
```java
// 1. Calendar를 Date로 변환
Calendar cal1 = Calendar.getInstance();
    ...
Date d = new Date(cal.getTimeInMillis()); // Date(long date)

// 2. Date를 Calendar로 변환
Date d = new Date();
    ...
Calendar cal = Calendar.getInstance();
cal.setTime(d)
```



# reference
자바의 정석 - 남궁성
