# 파일의 권한

```
-DRAGLINE-
-중요!
-찾아보기
-TODO
```
## 권한
- 파일 및 디렉토리 권한
#
![th](/assets/th.JPG)

![sda](/assets/sda.JPG)
- 각각의 기능
![캡처ewe](/assets/캡처ewe.JPG)
파일권한을 바꾸는 모습
```powershell
linux@ubuntu:~/0612$ touch hello.txt
linux@ubuntu:~/0612$ ls ll
drwxrwxr-x  2 linux linux 4096 Jun 11 17:49 ./
drwxr-xr-x 17 linux linux 4096 Jun 11 17:49 ../
-rw-rw-r--  1 linux linux    0 Jun 11 17:49 hello.txt
```
```powershell
linux@ubuntu:~/0612$ chmod -r hello.txt
    #읽기권한을 뺀 hello.txt
linux@ubuntu:~/0612$ ll
total 8
drwxrwxr-x  2 linux linux 4096 Jun 11 17:49 ./
drwxr-xr-x 17 linux linux 4096 Jun 11 17:49 ../
--w--w----  1 linux linux    0 Jun 11 17:49 hello.txt
#모든 읽기권한이 없어졌다.
```
```powershell
linux@ubuntu:~/0612$ cat hello.txt
cat: hello.txt: Permission denied
#권한이 없어 hello.txt의 내용을 알 수 없다.
```
## 파일의 권한 변경 방법
![캡werqwr처](/assets/캡werqwr처.JPG)
    
    퍼미션을 정수로 사용하여 8진수로 저장 설정
    ex> chmod 444 a.txt
#
    8진법의 장점 : 다수의 권한을 한 번에 설정할 수 있다
            단점 : 일부 권한을 설정할 수 없으며 다른 권한이 변경될 수 있음
```powershell
-rw-rw-r-- 1 linux linux 0 Jun 11 17:39 hello.txt
linux@ubuntu:~/0612$ chmod 644 hello.txt
```
- chmod 명령어 사용
  - 1. 관리자 (root)
  - 2. 파일 소유자
#

    사용 방법 : chmod [permission] [filename]
```
Usage: chmod [OPTION]... MODE[,MODE]... FILE...
  or:  chmod [OPTION]... OCTAL-MODE FILE...
  or:  chmod [OPTION]... --reference=RFILE FILE...
Change the mode of each FILE to MODE.
With --reference, change the mode of each FILE to that of RFILE.

  -c, --changes          like verbose but report only when a change is made
  -f, --silent, --quiet  suppress most error messages
  -v, --verbose          output a diagnostic for every file processed
      --no-preserve-root  do not treat '/' specially (the default)
      --preserve-root    fail to operate recursively on '/'
      --reference=RFILE  use RFILE's mode instead of MODE values
  -R, --recursive        change files and directories recursively
      --help     display this help and exit
      --version  output version information and exit

Each MODE is of the form '[ugoa]*([-+=]([rwxXst]*|[ugo]))+|[-+=][0-7]+'.

```
```powershell
linux@ubuntu:~/0612$ chmod 444 hello.txt
linux@ubuntu:~/0612$ ll
total 8
drwxrwxr-x  2 linux linux 4096 Jun 11 17:49 ./
drwxr-xr-x 17 linux linux 4096 Jun 11 17:54 ../
-r--r--r--  1 linux linux    0 Jun 11 17:54 hello.txt
```


| 구분           | 문자 | 의미                     |
| -------------- | ---- | ------------------------ |
| 카테고리       | u    | 파일소유자(user)         |
|                | g    | 소유자가 속한 그룹(group |
|                | o    | 이외의 나머지(other)     |
|                | a    | 전체 사용자(all)         |
| 연산자 기호    | +    | 권한 추가                |
|                | -    | 권한 삭제                |
|                | =    | 권한 설정                |
| 접근 권한 문자 | r    | 읽기                     |
|                | w    | 쓰기                     |
|                | x    | 실행                     |



    