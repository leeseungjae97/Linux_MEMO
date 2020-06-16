```s
복습내용
linux@ubuntu:~/0615$ vi 0612.sh
  1 #!/bin/bash
  2
  3 read -p "input your name: "
  4
  5 echo "your name : $REPLY"

```
---
# vi 분기문
## test 명령어
 - 사용법 : test Express
>표현식이 참이면 0, 거짓이면 1의 종료 상태를 반환

    if test... -> test의 표현식이 참인 경우 종료 상태가 0으로 설정되고 
    if 문은 종료 상태를 보고 0이면 참으로 인식하여 실행

- 기호를 쓰지않고 옵션을 사용하여 대소 비교
>int1 -eq int2: int 1 == int2<br/>
int1 -ne int2: int 1 != int2<br/>
int1 -gt int2: int 1 > int2<br/>
int1 -lt int2: int 1 < int2<br/>
int1 -ge int2: int 1 >= int2<br/>
int1 -le int2: int 1 <= int2
---
SYNOPSIS

       test EXPRESSION
       test

       [ EXPRESSION ]
       [ ]
       [ OPTION
DESCRIPTION

       Exit with the status determined by EXPRESSION.

       --help display this help and exit

       --version
              output version information and exit

       An  omitted  EXPRESSION defaults to false.  Otherwise, EXPRESSION is true or false and
       sets exit status.  It is one of:

       ( EXPRESSION )
              EXPRESSION is true

       ! EXPRESSION
              EXPRESSION is false

       EXPRESSION1 -a EXPRESSION2
              both EXPRESSION1 and EXPRESSION2 are true

       EXPRESSION1 -o EXPRESSION2
              either EXPRESSION1 or EXPRESSION2 is true

       -n STRING
              the length of STRING is nonzero

       STRING equivalent to -n STRING

       -z STRING
             the length of STRING is zero

       STRING1 = STRING2
              the strings are equal

       STRING1 != STRING2
              the strings are not equal

       INTEGER1 -eq INTEGER2
              INTEGER1 is equal to INTEGER2

       INTEGER1 -ge INTEGER2
              INTEGER1 is greater than or equal to INTEGER2

       INTEGER1 -gt INTEGER2
              INTEGER1 is greater than INTEGER2

       INTEGER1 -le INTEGER2
              INTEGER1 is less than or equal to INTEGER2

       INTEGER1 -lt INTEGER2
              INTEGER1 is less than INTEGER2

       INTEGER1 -ne INTEGER2
              INTEGER1 is not equal to INTEGER2

       FILE1 -ef FILE2
              FILE1 and FILE2 have the same device and inode numbers

       FILE1 -nt FILE2
              FILE1 is newer (modification date) than FILE2

       FILE1 -ot FILE2
              FILE1 is older than FILE2

       -b FILE
              FILE exists and is block special

       -c FILE
              FILE exists and is character special
     -d FILE
              FILE exists and is a directory
            디렉토리 존재여부 확인

       -e FILE
              FILE exists

       -f FILE
              FILE exists and is a regular file

       -g FILE
              FILE exists and is set-group-ID

       -G FILE
              FILE exists and is owned by the effective group ID

       -h FILE
              FILE exists and is a symbolic link (same as -L)

       -k FILE
              FILE exists and has its sticky bit set

       -L FILE
              FILE exists and is a symbolic link (same as -h)

       -O FILE
              FILE exists and is owned by the effective user ID

       -p FILE
              FILE exists and is a named pipe

       -r FILE
              FILE exists and read permission is granted

       -s FILE
              FILE exists and has a size greater than zero

       -S FILE
              FILE exists and is a socket

       -t FD  file descriptor FD is opened on a terminal
       -u FILE
              FILE exists and its set-user-ID bit is set

       -w FILE
              FILE exists and write permission is granted

       -x FILE
              FILE exists and execute (or search) permission is granted

       Except for -h and -L, all FILE-related tests dereference symbolic links.  Beware  that
       parentheses need to be escaped (e.g., by backslashes) for shells.  INTEGER may also be
       -l STRING, which evaluates to the length of STRING.

       NOTE: Binary -a and -o are inherently ambiguous.  Use 'test EXPR1 &&  test  EXPR2'  or
       'test EXPR1 || test EXPR2' instead.

       NOTE:  [ honors the --help and --version options, but test does not.  test treats each
       of those as it treats any other nonempty STRING.

```bash
  1 # #!/bin/bash
  2
  3 # 사용자로부터 입력 받은 숫자가 0인지 아닌지 판단하는 코드
  4 # if...
  5 #
  6 # else
  7 #....
  8 # endif
  9 read -p "input integer: "
 10 if test "$REPLY" -eq 0 #reply가 0과 같냐는 분기문
 11                        #reply가 공백이 있는 문자일수도 있기때문에 큰따옴표로 묶어준다
 12 #if (REPLY == 0}
 13 # {
 14 # printf("zero\n");
 15 #}
 16
 17 then
 18  echo "zero"
 19 fi
 20
 21 if test "$REPLY" -ne 0 #if (REPLY !=0)
 22 then                   #{
 23  echo "not zero"       # printf("not zero\n")
 24 fi                     #
```
---
```bash
 21 if test "$REPLY" -ne 0;then #if (REPLY !=0)
 22  echo "not zero"       # printf("not zero\n")
 23 fi 
```
>- test와 표현식의 조합이 복잡해지는 경향이 있으므로 이를 해결하기 위해 단축 표기법을 제공
---
> - test Express == [ Express ]
>>[ ]와 test는 완전히 동일하게 해석된다.
---
```bash
if test $REPLY -eq 0; then
    echo "zero"
fi

if [ $REPLY -eq 0 ] ; then
    echo "zero"
fi

! 대괄호 내부의 각각의 토큰은 공백으로 띄워 주어야한다.
# 세미콜론은 붙여도, 띄워도 된다.
```
---
```bash
if [ "$REPLY" -eq 0 ]; then  # if(REPLY == 0)
    echo "zero"              # printf("zero\n");
else                         # }else{
    echo "not zero"          # printf("not zero\n");
fi                           #}
```
---
```bash                        
 44 if [ "$REPLY" -eq 0 ]; then #if (REPLY == 0 ) {}
 45     echo "zero"             #   printf("zero\n");
 46 else                        #} else {
 47     if [ "$REPLY" -gt 0 ]; then    #   if (REPLY >0) {
 48         echo "positive"     #       printf("printf\n);
 49     else                    #   } else {
 50         echo "negative"     #       printf("negative\n");
 51     fi                      #   }
 52 fi                          #}
#else if ==> elif
```
---
> 자동들여쓰기 미동작시 해당코드 수행
>>vi ~/.vimrc
filetype indent on  
: 들여쓰기 자동수행 명령어

> 들여쓰기 수정
>>  현재 커서를 기준으로 아래의 모든행에 대하여 들여쓰기 수행 :=G
>> 현재 커서를 기준으로 위의 모든 행에 대하여 들여쓰기를 수행 :=gg   

---
>else if로 바꿔보자
```bash
if [ "$REPLY" -gt 0 ]; then   #if( REPLY > 0) {
    echo "positive"           #  printf("positive\n");
elif [ "$REPLY" -lt 0 ]; then # }else if (REPLY >0 ) {
    echo "negative"           #     printf("negative\n");
else                          #else 
    echo "zero"               #     printf("zero\n");
fi                            #}
```

>REPLY 재사용의 문제 
>>    두번째의 입력시에는 REPLY를 사용하지않고 일반적인 변수를 사용해야한다
```bash
  4 # 비밀번호 확인 프로그램
  5 read -p "input password: "
  6 if [ -z "$REPLY" ]; then
  7     echo "비밀번호를 입력하지 않으셨습니다"
  8     exit 1
  9 fi
 10
 11 read -p "confirm your password: " pswd
 12 if [ "$pswd" = "$REPLY" ]; then  #if (strcmp(pswd, REPLY) ==0) {
 13     echo "OK!"
 14 else
 15     echo "wrong password"
 16 fi
```
|-출력!|
|-|
```s
input password: linux
confirm your password: linux
OK!

Press ENTER or type command to continue
```
---
|-출력!|
|-|
```s
input password: linux
confirm your password: ll
wrong password

Press ENTER or type command to continue
```
<br/>
---
- [ 조건검사 ] || 동작 : 조건이 참이 아니면 동작을 수행
- [ 조건검사 ] && 동작 : 조건이 참이면 동작을 수행

        ex> 인자가 3개인 스크립트 작성  
        ./test.sh 1 2 - > 명령행의 개수는 #변수에 저장된다.

        int main(int argc, ...) {})
                이부분과 같은 내용
---
<br/>

    if (argc != 3){
        fprintf("3개의 인자가 필요하다.\n");
    }
    (argument count)
        [ "$#" -lt 3] || echo "3개 이상의 인자가 필요합니다"

---
```bash
#test
filename="./control.sh"
if [ -e "$filename" ]; then     #파일의 존재여부 확인
    echo "해당 파일이 존재합니다"
else
    echo "해당 파일은 존재하지 않습니다"
fi
```
```bash
 21 #특정 디렉토리가 존재하지 않을 경우 그 디렉토리 생성 코드
 22  dirname="mysub"
 23  if [ !-d "$dirname" ]; then # 해당 디렉토리가 없다면.
 24    mkdir "$dirname"
 25  else
 26    echo "존재하는 파일입니다."
 27  fi
```
> 이러한 연산은 매우 많이 쓰인다
```bash
 29 dirname="subdir"
 30 [ -d "$dirname" ] || mkdir "$dirname"
```
---
> linux 환경 파일에서 사용된 위의 분기문
```bash
~/.bashrc의 내용 .
 30 # make less more friendly for non-text input files, see lesspipe(1)
 31 [ -x /usr/bin/lesspipe ] && eval "$(SHELL=/bin/sh lesspipe)"
 32
 33 # set variable identifying the chroot you work in (used in the prompt below)
 34 if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
 35     debian_chroot=$(cat /etc/debian_chroot)
 36 fi
```
---
## test 합성명령어
>test 명령어는 정규표현식을 지원하지 않는다.
>>test 명령어 + 정규표현식 = 합성 명령어([[]])

    사용방법 : [[표현식]]

- 기존의 test 명령어의 기능을 제공하고 추가적으로 정규표현식도 지원

---
>정규표현식에 대한 패턴 비교 : 

|문자열 ~= 패턴|
|-|

    if [[ "$str" =~ hello ]]; then
---
>연습문제 : 사용자로부터 정수를 입력 받아 0인지 아닌지 판별하는 스크립트 구현

단 정수가 아닌 문자열이 입력될 경우 오류메세지를 출력하고 종료.

```bash
  1 # #!/bin/bash
  2
  3 read -p "input integer : " # -20 300 300 0 070
  4                            # 수의 패턴은 0으로 시작할 필요가없다.
  5 if [[ ! "$REPLY" =~ ^-?[:dight:]+$ ]]; then # 집합의 범위를 표현하기위>    해 -를 쓰는 표현은 Unix의 표현이므로 다른 shell에서 호환성을 보장받을 수 없다.
  6     echo "input date is not number"
  7 else
  8     echo "not zero error"
  9     exit 1
 10 fi
```
---
>분기문이 많아지면 연산수행능력이 떨어진다는 단점이 존재
## case문

```bash
  1 # #!/bin/bash
  2
  3 # 3가지 메뉴 시스템
  4 clear
  5
  6 echo "
  7 1. 짜장면
  8 2. 짬뽕
  9 3. 탕수육
 10 0. 종료"
 11
 12 read -p "*메뉴를 선택해 주세요 : "
 13 #if문으로 코드 작성 시 장황하다 case문 활용
 14
 15 # usage : case 변수명 in
 16 case $REPLY in             # switch (REPLY) {
 17     0)  exit 0             #        case 0 : exit (0);
 18         ;;                 #        break;
 19     1) echo "짜장면선택";; # case 1 : printf("짜장면선택\n") break;
 20     2) echo "짬뽕선택";;   # case 2 : printf("짬뽕선택\n")break;
 21     3) echo "탕수육선택";; # case 3 : printf("탕수육선택\n")break;
 22     *) echo "잘못된선택"   # default : printf("잘못된선택\n")
 23         exit;;             #            exit; break;
 24 esac   
```
|-출력!|
|-|
```s
1. 짜장면
2. 짬뽕
3. 탕수육
0. 종료
*메뉴를 선택해 주세요 : 1
짜장면선택

Press ENTER or type command to continue
```
---
case에서 정규표현식은 일반적인 정규표현식과 다른 방식으로 지원된다.
case에서 제공되는 자기자신의 정규표현식이 따로 있다

    a): a 완벽하게 일치하는경우
    a|A): a 또는 A와 완벽하게 일치하는 경우
    ???): 정확히 세 글자로 이루어진 단어
    *.txt): 확장자가 txt인 경우
    *) 모든 단어로 이루어진 케이스 == default

|-주의!|
|-|
|범위가 넓은 case문이 위에 존재하고 세부사항에 대한 case문이 하위로 들어가면 실행되지 못한다.|
---
```bash
 27 clear
 28
 29 echo "
 30 a. 짜장면
 31 b. 짬뽕
 32 c. 탕수육
 33 q. 종료"
 34
 35 read -p "*메뉴를 선택해 주세요 : "
 36
 37
 38 # 서로다른 문자열을 쓸수 있게 OR을 써준다
 39 case $REPLY in
 40     q|Q)    exit 0;; # 대문자를 입력해도 case에서 걸리게끔 만들었다.
 41     a|A) echo "짜장면선택";;
 42     b|B) echo "짬뽕선택";;
 43     c|C) echo "탕수육선택";;
 44     *) echo "잘못된선택"
 45         exit;;
 46 esac

```
|-출력!|
|-|
```s
a. 짜장면
b. 짬뽕
c. 탕수육
q. 종료
*메뉴를 선택해 주세요 : B
짬뽕선택

Press ENTER or type command to continue
```
---

## while 표현식
```bash
while 1                 #while(1)
do                      # {
    echo "hello, world" #   printf("hello, world");
done                    # }
```
> 해당 코드는 오류, 1에 대한 command 설정이 되어있지않다
---
```bash
while true                 #while(true)
do                      # {
    echo "hello, world" #   printf("hello, world");
done                    # }
```
>true라고 써주어야 while문이 작동
 
    while true; do 
    와 같은식으로 한줄 입력도 가능하다.

---
>bash에서는 입력되는 모든 문자열들은 수가 아니라 숫자로 해석되기 때문에
연산식이 동작하지 않는다.
>> while을 제어하려면 수를 제어하는 방식을 알아야한다.

- shell에서는 직접적인 수 입력이 되지 않는다
```s
    linux@ubuntu:~/0615$ 3 + 2 # 3은 명령어로 해석되어 들어가고 
                               #나머지는 해석되지 않는다
    3: command not found
```
---
### 수 계산

- expr 명령어 사용
```s
expr 정수 연산자 정수 
linux@ubuntu:~/0615$ expr 2 + 2
4
linux@ubuntu:~/0615$ expr 2 - 2
0
linux@ubuntu:~/0615$ expr 4 % 4
0
linux@ubuntu:~/0615$ expr 9 * 9 # *가 와일드카드로 해석되지 않도록
                                # 백슬래시(\)를 써주자
expr: syntax error
```
```s
linux@ubuntu:~/0615$ expr 9 \* 9
```

>expr는 %연산자를 포함한 5칙연산 가능

|-주의!|
|-|
|expr 사용시 반드시 띄어씌기 해주어야한다.|
---
- $[ ] 사용
```s
linux@ubuntu:~/0615$ $[1 + 1] #expr은 echo로 치환되어 지지만
                              #$[]은 치환되지 않는다
2: command not found
```
```s
linux@ubuntu:~/0615$ echo $[1 + 1] # echo를 사용해 주어야한다.
2
linux@ubuntu:~/0615$ echo $[9 * 1]
9
linux@ubuntu:~/0615$ echo $[9 / 1]
9
linux@ubuntu:~/0615$ echo $[9 - 1]
8
linux@ubuntu:~/0615$ echo $[2 ** 10]
1024
```
>$[ ]는 승수 연산까지 포함한 6칙연산 가능

|-주의!|
|-|
|대괄호에는 연산자와 피연산자만 들어갈 수 있다.|

---
- $(( )) 사용
```s
linux@ubuntu:~/0615$ echo $(( 1 + 1 ))
2
linux@ubuntu:~/0615$ echo $(( 2 ** 20 ))
1048576
```
> $[ ]와 마찬가지로 6칙(+, -, /, %, *, **)연산 가능

---
```bash
  1 #!/bin/bash
  2
  3 #아래의 두 변수는 모두 문자열을 저장하는 코드
  4
  5 n1=10
  6 n2=20
  7
  8 expr $n1 + $n2
    # expr에 대하여 피연산자로 변수가 올 수 있다. 
  9 expr ++$n1 # n1+=1 해당코드는 동작하지 않는다
               # 단항연산자에 대해서 동작하지 않는다.
```
|-출력!|
|-|
```
30
++10

Press ENTER or type command to continue
```
---
>대괄호에서는 연산자만 알수 있다면 나머지 피연산자에 대해서 알 수 있다
```bash
expr $[n1 + n2]
```
> 그러므로 $를 생략할 수 있다.
---
```s
 12 age=0 # 0이라는 문자가 저장된 것을 의미
 13 echo $[age = age + 1]
 14 echo $[age += 1]
 15 echo $[++age]
```
|-주의!|
|-|
|가급적 연산식에 들어가는 변수에 대해서 연산가능한 형식의 값만 넣어주자|
---
```s
 17 age=0
 18 echo $((age = age + 1))
 19 echo $((age += 1))
 20 echo $((++age))
```
> 소괄호에 대한 연산도 대괄호와 동일하게 수행된다.
---
```bash
  8 cnt=1
  9 while [ "$cnt" -le 5 ]; do      #while (cnt <=5) {
 10     echo "$cnt:hello, world"    #   printf("%d: hello, world\n", cnt);
 11     ((++cnt))                   #   ++cnt;
 12 done  
```
|-주의!|
|-|
|while와 대괄호, 대괄호 내부 매개변수에 대해서 띄어쓰기를 올바르게하자|
---
```bash
  8 cnt=1
  9 while (cnt <=5) {
 10    printf("%d: hello, world\n", cnt);
 11    ++cnt;
 12 done  
```
> 위와 같은 방법도 있지만 Open Source에서는 해당코드의 상위 코드를 더 많이쓴다.
---
> break와 continue로 while문을 제어하는 모습
```bash
 34 # 1부터 100까지 자연수중 짝수만 저장하는 스크립트 구현
 35
 36 cnt=0
 37 sum=0
 38
 39 while true; do
 40     ((++cnt))
 41     if  ((cnt > 100)); then
 42         break
 43     fi
 44
 45     if (( (cnt % 2) != 0 )); then
 46         continue
 47     else
 48         ((sum += cnt))
 49     fi
 50 done
 51
 52 echo "$sum"

    #while 표현식이 참인 경우 루프실행
    #until 표현식이 거짓인 경우 루프실행
    #사용방법
    #until 표현식; to
    #....
    #done
```
---
## for : list-based
> C언어 기반의 loop는 for loop에 해당하는 loop를 만들어 주었어야했는데
> 이미 가공되어있는 loop를 사용하게되면 코드가 좀더 줄어든다

>> 반복문이 for-loop기반의 반복문을 주지않고 list를 주어 반복을 실행함으로써
> 좀 더 강력한 loop문을 만든다
```bash
  3 #bash에서는 list 기반의 반복밖에 안된다
  4 #for: list-based loop
  5 #사용 방법
  6 # for 변수명 in 리스트
  7 #do
  8 #   ...
  9 #done
 10
 11 for var in 0 1 2 3 4 5 6 7 8 9
 12 do
 13     echo "$var: hello, world"
 14 done
```
---
```bash
 17 for var in {0..9}; do
 18     echo "$var: hello, world"
 19 done
```
---
```bash
 29 read -p "input number "
 30 sum=0
 31 for var in {0..$REPLY}; do
 32     ((sum+=var))
 33 done
 34 echo "$sum"
```
> 위 코드는 에러가 발생한다 중괄호 확장은 상수만 사용가능하다

|-출력!|
|-|
```s
input number 10
./for.sh: line 32: ((: {0..10}: syntax error: operand expected (error token is "{0..10}")
0

Press ENTER or type command to continue

숫자로 나오지않고 {0..$REPLY}의 값 그대로 찍히는 모습
```
---
## seq
NAME
       seq - print a sequence of numbers

SYNOPSIS

       seq [OPTION]... LAST = 처음값
       seq [OPTION]... FIRST LAST =+ FIRST LAST
       seq [OPTION]... FIRST INCREMENT LAST = 증가후 마지막값

DESCRIPTION

       Print numbers from FIRST to LAST, in steps of INCREMENT.

       Mandatory arguments to long options are mandatory for short options too.

       -f, --format=FORMAT
              use printf style floating-point FORMAT

       -s, --separator=STRING
              use STRING to separate numbers (default: \n)

       -w, --equal-width
              equalize width by padding with leading zeroes
```s
linux@ubuntu:~/0615$ seq 1 1 15
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
```
---
```bash
 29 read -p "input number "
 30 sum=0
 31 for var in $(seq $REPLY); do
 32     ((sum+=var))
 33 done
 34 echo "$sum"
```
>seq을 이용한 for loop 기반 반복문

|-출력!|
|-|
```s
input number 55
1540

Press ENTER or type command to continue
```
---
### C language for loop
```bash
 36 # bash최근 업데이트를 통해 C언어와 유사한 형태의 for loop를 제공한다
 37 #usage: for((expr1;expr2;expr3));do
 38 #...
 39 #done
 40 for i in {0..4};do
 41     echo "$i: hello, world"
 42 done
 43
 44 for ((i = 0 ; i < 5; i ++));do
 45     echo "$i : hello, world"
 46 done
```
|-출력!|
|-|
```s
0: hello, world
1: hello, world
2: hello, world
3: hello, world
4: hello, world
0 : hello, world
1 : hello, world
2 : hello, world
3 : hello, world
4 : hello, world

Press ENTER or type command to continue
```
> 둘다 적절히 사용하자
---
### 반복문의 중첩
```bash
 48 #반복문도 중첩이 가능하다
 49 for (( i=2; i<10; i++ )); do
 50     for (( j=0; j<10; j++ ));do
 51         printf "%d x %d = %d\n" $i $j $((i * j))
 52     done
 53     echo        #개행의 의미로 사용
 54 done
```
|-출력!|
|-|
```s
2 x 0 = 0
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6
2 x 4 = 8
2 x 5 = 10

...

9 x 6 = 54
9 x 7 = 63
9 x 8 = 72
9 x 9 = 81


Press ENTER or type command to continue
```
```bash
 56 # Su Mo Tu We Th Fr Sa
 57 #  1  2  3  4  5  6  7
 58 #  8  9 10 11 12 13 14
 59 # ..................
 60 # 31
 61
 62 echo "Su Mo Tu We Th Fr Sa"
 63 for (( i=1; i<32; i++ ));do
 64     if (( ($i % 7) ==0 )); then
 65         printf "%2d " $i
 66         echo
 67     else
 68         printf "%2d " $i
 69     fi
 70 done
```
|-출력!|
|-|
```s
Su Mo Tu We Th Fr Sa
 1  2  3  4  5  6  7
 8  9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29 30 31
Press ENTER or type command to continue
```
---
> 강사님 코드
```bash
    for day in {0..31};do
        printf "%3d" $day
        (( (day%7 )==0 )) && echo
    done
    echo
```
---
## bash : Positional Parameter
```c
  2 
  3         // a.out hello world
  4         // argv:[0]   [1]   [2]
  5 int main(int argc, char** argv) {
                        // bash : positional Parameter
                        // C : opional parameter
  6    for (int i=0; i< argc; i++)
  7        printf("argv[%d] = %s\n", argv[i])
  8 }
```
```bash
  1 #!/bin/bash
  9
 10
 11 # C : argument
 12 # bash  : positional parameter
 13
 14 #pre-defined variable: ?, REPLY,
 15 #                      0 1 2 3 4 5 6 7 ...
 16
 17 echo $0
 18 echo $1
```
|-출력!|
|-|
```
./argument.sh

Press ENTER or type command to continue
```
```s
linux@ubuntu:~/0615$ ./argument.sh hello my
./argument.sh
hello
```
```bash
 21 echo $1 $2 $3 $4 $5 $6 $7 $8 $9 $10
                                #두자리 수는 $1 == 첫번째 매개변수 + 0
                                #첫번째원소에 '1'+'0' = '10'
```
|-출력!|
|-|
```s
linux@ubuntu:~/0615$ ./argument.sh 1 2 3 4 5 6 7 8 9 10
1 2 3 4 5 6 7 8 9 10
linux@ubuntu:~/0615$ ./argument.sh 1 2 3 4 5 6 7 8 9 99
1 2 3 4 5 6 7 8 9 10
# 값이 똑같이 나오게된다
```

```bash
#위치매개변수 사용 시, 2자리수 이상의 매개 변수에 접근하려면
# 반드시 중괄호로 묶어주어야 한다.
21 echo $1 $2 $3 $4 $5 $6 $7 $8 $9 ${10}
```
|-출력!|
|-|
```s
linux@ubuntu:~/0615$ ./argument.sh 1 2 3 4 5 6 7 8 9 99
1 2 3 4 5 6 7 8 9 99
```
---
## bash : 
```c
  2 
  3         // a.out hello world
  4         // argv:[0]   [1]   [2]
  5 int main(int argc, char** argv) {
            // bash : #
  6    for (int i=0; i< argc; i++)
  7        printf("argv[%d] = %s\n", argv[i])
  8 }
```
```bash
23 echo $#
# 스크립트 이름을 제외한 나머지의 개수만 전달된다.
```
```s
linux@ubuntu:~/0615$ ./argument.sh hello world
                    # 매개변수 2개가 전달되어
2                   # 그 개수가 찍힌모습
```
---
```bash
 25 #연습문제 아래의 기능과 동일하게 동작하는 스크립트 작성
 26 # int main(int argc, char** argv) {
 27 #   for (int i =0  ; i < argc; i++)
 28 #       printf("%s\n", argv[i])
 29 # }
 30 echo $1 $2 $3 $4 $5 $6 $7 $8
 31 for var in {0..10}; do
 32     if (($var<11)); then
 33         continue
 34     fi
 35     echo $var
 36 done
 37 echo $#
 38
```
---
강사님 코드
- 첫번째 방법
shift를 통해 위치 매개변수 전체를 왼쪽으로 한칸씩 이동
> $1 번째 라인 출력 = hello
for문으로 shift

||||./argument|hello|wrold|
|-|-|-|-|-|-|
||||0|1|2|
---

> $1 번째 라인 출력 = world

|||./argument|hello|wrold||
|-|-|-|-|-|-|
||||0|1|2|
---
> $1 값 없음

||./argument|hello|wrold|||
|-|-|-|-|-|-|
||||0|1|2|
---
> 아무것도 없으므로 출력종료

|./argument|hello|wrold||||
|-|-|-|-|-|-|
||||0|1|2|

|입력종료|
|-|
> 첫번째 위치에 아무것도 없으므로 1을 return 

```bash
 32 # shift : 위치 매개변수 전체를 왼쪽으로 한칸씩 이동
 33 # ex)               ./argument hello world
 34 #                       0       1       2
 35 #1 .while
 36 while [ -n "$1" ]; do   #while ($1 != NULL) {
 37     echo "$1"
 38     shift
 39 done
```
---
- 두번째 방법
> $@(위치 매개변수 전체를 저장하고 있는 내장 변수) 사용
 
```bash
    41 for arg in $@; do
    42     echo "$arg"
    43 done
    44 echo $#
# 2. for + @(위치 매개변수 전체를 저장하고 있는 내장 변수)
```
|-출력!|
|-|
```s
linux@ubuntu:~/0615$ ./argument.sh hello world ll
hello # $@로 for문을 돌려 출력한 모습
world
ll
3 # $#로 argument 즉 positional parameter의 개수를 찍은 모습
```
---
> 연습문제 
> ./test.sh -a -b -c
> option a
> option b
> option c

> ./test.sh -a
> option a

> ./test.sh -b
> option b

> ./test.sh -c
> option c

단 잘못된 옵션에 대해서는 사용 방법에 대하여 출력
./test -a -x
option a
usage: ./text [-a] [-b] [-c]

---
강사님 코드

```bash
while[ -n "$(echo | grep '-')" ]; do
    case "$1" in
        -a) echo "option a";;
        -b) echo "option a";;
        -c) echo "option a";;
        *) echo "usage: ./text [-a] [-b] [-c]"
        exit 1;;
    esac
    shift
done
```
---