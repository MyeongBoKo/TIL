# 헤더 Header
제목을 작성할 때 사용한다.  
#을 사용하는 텍스트이다.   
#을 최대 6개까지 사용한다.   
#이 늘어날때마다 글자의 크기가 작아진다.  
#을 하나만 사용하면 자동으로 수평선이 생긴다.

# Hello world!
## Hello world!
### Hello world!
#### Hello world!
##### Hello world!
###### Hello world!<br>

# 줄바꿈
문장 끝에 빈칸 2개 이상 넣는다.  
<> 안에 br을 집어넣은 후에 문장 끝에 작성한다.




# 수평선
"***, -, _**" 중에서 한 가지를 선택해서 사용한다.  



   
# 강조 
별모양(**)을 앞 뒤이면 붙이면 볼드체 생성한다.   
ex) **bold**<br>
별모양을(*)을 앞 뒤에 붙이면 이탈릭체 생성한다.  
ex) *italic*<br>
물결모양(~~)을 앞 뒤에 붙이면 취소선 생성한다.  
ex) ~~strikethrough~~<br>

# 인용구(Quote) 사용
(>)을 통해서 나타낸다.
>Hello world!

# 목록
(*, -, number)를 통해서 나타낸다.

Alphabet:
* a
* b

Other alphabet:
- c
- D

Numbers:
1. first
2. second
3. third

# 링크(Link)
[] 안에 원하는 단어를 작성한 뒤, () 안에 원하는 링크를 작성하면 클릭이 가능하게 나타낼 수 있다.

Click [Hello](https://github.com/MyeongBoKo)


# 이미지 추가
느낌표 옆에 대골호 안에 이미지에 대한 설명을 작성한 후에 소괄호 안에 이미지에 링크를 추가하면 이미지가 나오는 것을 확인할 수 있다.
![]()

# 테이블
많은 데이터를 효율적으로 표현할 수 있는 기능<br>
"|", "-"를 이용해서 나타낸다. <br>
":"을 오른쪽에 붙이면 오른쪽 정렬표현<br>
":"을 왼쪽에 붙이면 왼쪽 정렬표현<br>
":"을 양쪽에 붙이면 중간 정렬표현<br>
가장 자리에는 "|" 생략 가능<br>
"|Hello|World|"<br>
"|--|--|"<br>

|Hello|World|
|--:|:--:|
|Hi|미국|
|Hi|한국|
|Hi|일본|
|Hi|중국|

# code
"`"(백틱) 기호를 사용한다<br>  

println(`Hello World!`)

다수의 코드가 존재하면 "`"(백틱) 기호를 3번 두줄로 작성 하면 코드블럭이 생성되고 그 안에 코드를 집어넣으면 된다.


이때 "**```**" 앞에 언어를 지정해주면 **syntax color**가 지정된다.

```java
class CodeEx {
    public static void main(String[] args){
        System.out.println("Hello World!");
    }
}
```
