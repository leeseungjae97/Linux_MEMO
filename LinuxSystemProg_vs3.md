# stat
```c
 1 // 0_owner.c
  2 #include <stdio.h>
  3 #include <sys/types.h>
  4 #include <sys/stat.h>
  5 #include <unistd.h>
  6
  7 int main(int argc, char**argv) {
  8     if (argc != 2) {
  9         fprintf(stderr, "usage: %s FILE\n", *argv);
 10         return -1;
 11     }
 12     --argc, ++argv;
 13
 14     struct stat sb;
 15     if(lstat(*argv, &sb) == -1 ) {
 16         perror("lstat");
 17         return -1;
 18     }
 19
 20     printf("%d\n", sb.st_uid);
 21     printf("%d\n", sb.st_gid);
 22
 23     printf("%s\n", *argv);
 24
 25     return 0;
 26
 27 }
~
```
```s
linux@ubuntu:~/0619$ gcc 0_owner.c
linux@ubuntu:~/0619$ ./a.out 0_owner.c
1000 # linux의 id
1000
0_owner.c
```
> lstat를 통해 user id와 group id를 가져왔다.
---
```c
  1 // 0_owner.c
  2 #include <stdio.h>
  3 #include <sys/types.h>
  4 #include <sys/stat.h>
  5 #include <unistd.h>
  6 #include <sys/types.h>
  7 #include <pwd.h>
  8 #include <grp.h>
  9
 10
 11 int main(int argc, char**argv) {
 12     if (argc != 2) {
 13         fprintf(stderr, "usage: %s FILE\n", *argv);
 14         return -1;
 15     }
 16     --argc, ++argv;
 17
 18     struct stat sb;
 19     if(lstat(*argv, &sb) == -1 ) {
 20         perror("lstat");
 21         return -1;
 22     }
 23
 24 //  printf("%d\n", sb.st_uid);
 25     struct passwd * pswd = getpwuid(sb.st_uid); #user id 에 대한 struct
 26     if(pswd == NULL) {
 27         perror("getpwuid");
 28         return -1;
 29     }
 30
 31 //  printf("%d\n", sb.st_gid);
 32 //  /etc/group
 33     struct group *grp = getgrgid(sb.st_gid); #group id에 대한 struct
 34     if(grp == NULL) {
 35         perror("getgrgid");
 36         return -1;
 37     }
 38
 39     printf("%s %s %s\n", pswd->pw_name, grp->gr_name, *argv);
 40
 41     return 0;
 42 }
```
```s
linux@ubuntu:~/0619$ gcc 0_owner.c
linux@ubuntu:~/0619$ ./a.out 0_owner.c
linux linux 0_owner.c
# 각각의 strcut에서 저장된 이름들을 불러왔다.
```
---
```c
  1 // 0_owner.c
  2 #include <stdio.h>
  3 #include <sys/types.h>
  4 #include <sys/stat.h>
  5 #include <unistd.h>
  6 #include <sys/types.h>
  7 #include <pwd.h>
  8 #include <grp.h>
  9
 10
 11 int main(int argc, char**argv) {
 12     if (argc != 2) {
 13         fprintf(stderr, "usage: %s FILE\n", *argv);
 14         return -1;
 15     }
 16     --argc, ++argv;
 17
 18     struct stat sb;
 19     if(lstat(*argv, &sb) == -1 ) {
 20         perror("lstat");
 21         return -1;
 22     }
 23
 24     printf("%ld %s\n", sb.st_size, *argv); 
        //파일의 크기 출력
 25
 26     return 0;
 27 }
```
```s
linux@ubuntu:~/0619$ ./a.out 1_fsize.c
427 1_fsize.c 
```
---
> 디렉토리나 일반파일에 대해서는 당연히 크기가 있지만<br/>
> 모니터나 마우스, 키보드같은 디바이스 특수파일은 사이즈가 없다<br/>

> 해당 디바이스와 같은 장치파일을 모아둔 /dev 를 보자
```s
linux@ubuntu:~/0619$ ls -l /dev
total 0
crw-------  1 root root     10, 175 Jun 18 17:39 agpgart
crw-r--r--  1 root root     10, 235 Jun 18 17:39 autofs
drwxr-xr-x  2 root root         460 Jun 18 17:39 block
drwxr-xr-x  2 root root          80 Jun 18 17:39 bsg
crw-------  1 root root     10, 234 Jun 18 17:39 btrfs-control
drwxr-xr-x  3 root root          60 Jun 18 17:38 bus
lrwxrwxrwx  1 root root           3 Jun 18 17:39 cdrom -> sr0
lrwxrwxrwx  1 root root           3 Jun 18 17:39 cdrw -> sr0
drwxr-xr-x  2 root root        3720 Jun 18 17:39 char
crw-------  1 root root      5,   1 Jun 18 17:40 console
lrwxrwxrwx  1 root root          11 Jun 18 17:38 core -> /proc/kcore
crw-------  1 root root     10,  59 Jun 18 17:39 cpu_dma_latency
crw-------  1 root root     10, 203 Jun 18 17:39 cuse
drwxr-xr-x  6 root root         120 Jun 18 17:39 disk

...

crw-------  1 root root     10, 241 Jun 18 17:39 vhost-vsock
crw-------  1 root root     10,  55 Jun 18 17:39 vmci
crw-rw-rw-  1 root root     10,  54 Jun 18 17:39 vsock
crw-rw-rw-  1 root root      1,   5 Jun 18 17:39 zero
crw-------  1 root root     10, 249 Jun 18 17:39 zfs
```

| crw------- | 1   | root | root | 10           | 249          | Jun 18 17:39 | zfs |
| ---------- | --- | ---- | ---- | :------------: | :------------: | ------------ | --- |
|       |     |      |      | major Number | minor Number |              |     |
|            |     |      |      | 상위 분류    | 하위 분류    |              |     |
---
>디바이스 파일에 대해 구분 지을 때 해당 major Number와 minor Number를 이용한다.
```c
  1 // 0_owner.c
  2 #include <stdio.h>
  3 #include <sys/types.h>
  4 #include <sys/stat.h>
  5 #include <unistd.h>
  6 #include <sys/types.h>
  7 #include <pwd.h>
  8 #include <grp.h>
  9 #include <sys/sysmacros.h>
 10
 11 int main(int argc, char**argv) {
 12     if (argc != 2) {
 13         fprintf(stderr, "usage: %s FILE\n", *argv);
 14         return -1;
 15     }
 16     --argc, ++argv;
 17
 18     struct stat sb;
 19     if(lstat(*argv, &sb) == -1 ) {
 20         perror("lstat");
 21         return -1;
 22     }
 23
 24 //  if( ((sb.st_mode & S_IFMT) == S_IFBLK) || ((sb.st_mode & S_IFMT) == S_IFCHR)) {
 25     if(S_ISBLK(sb.st_mode) || S_ISCHR(sb.st_mode)) {

 25     //현재파일이 블럭디바이스이거나 비어있는 파일일때

 27         //printf("%lu, %lu", (sb.st_rdev >> 8) & 0xFF, sb.st_rdev & 0xFF);
 28         printf("%u, %u",  major(sb.st_rdev), minor(sb.st_rdev));

 27         //차상위 2바이트를 버려야한다
 28         // major와 minor의 번호를 꺼내오는 코드
 29     }
 30     else {
 31         printf("%ld\n",sb.st_size);
 32     }
 33
 34     printf("%s\n",*argv);
 35
 36     return 0;
 37 }
```
```s
linux@ubuntu:~/0619$ ./a.out 1_fsize.c
773
1_fsize.c # 특수파일이 아닌경우
linux@ubuntu:~/0619$ ls -l 1_fsize.c
-rw-rw-r-- 1 linux linux 773 Jun 18 18:16 1_fsize.c

linux@ubuntu:~/0619$ ./a.out /dev/null
1, 3/dev/null # 특수파일인 경우 major와 minor를 뽑아온다
linux@ubuntu:~/0619$ ls -l /dev/null
crw-rw-rw- 1 root root 1, 3 Jun 18 17:39 /dev/null
```

```c
  1 // 0_owner.c
  2 #include <stdio.h>
  3 #include <sys/types.h>
  4 #include <sys/stat.h>
  5 #include <unistd.h>
  6 #include <sys/types.h>
  7 #include <pwd.h>
  8 #include <grp.h>
  9 #include <sys/sysmacros.h>
 10
 11 int main(int argc, char**argv) {
 12     if (argc != 2) {
 13         fprintf(stderr, "usage: %s FILE\n", *argv);
 14         return -1;
 15     }
 16     --argc, ++argv;
 17
 18     struct stat sb;
 19     if(lstat(*argv, &sb) == -1 ) {
 20         perror("lstat");
 21         return -1;
 22     }
 23
 24     printf("%lu ", sb.st_mtime);
 25
 26
 27     printf("%s\n",*argv);
 28     return 0;
 29 }
```
```s
linux@ubuntu:~/0619$ ./a.out 2_mtime.c
1592531359 2_mtime.c
```
> Epoch<br/>
> 1970년 1월 1일 00:00:00 협정 세계시(UTC) 부터의 경과 시간을 초로 환산하여 정수로 나타낸 것<br/>
```c
  1 // 0_owner.c
  2 #include <stdio.h>
  3 #include <sys/types.h>
  4 #include <sys/stat.h>
  5 #include <unistd.h>
  6 #include <sys/types.h>
  7 #include <pwd.h>
  8 #include <grp.h>
  9 #include <time.h>
 10 #include <sys/sysmacros.h>
 11
 12 int main(int argc, char**argv) {
 13     if (argc != 2) {
 14         fprintf(stderr, "usage: %s FILE\n", *argv);
 15         return -1;
 16     }
 17     --argc, ++argv;
 18
 19     struct stat sb;
 20     if(lstat(*argv, &sb) == -1 ) {
 21         perror("lstat");
 22         return -1;
 23     }
 24
 25     //yyyy-MM-dd hh:mm:ss
 26     //printf("%lu ", sb.st_mtime);
 27     char mtime[32] = {0, };
 28     struct tm *t = localtime(&sb.st_mtime);
 29     sprintf(mtime, "%04d-%02d-%02d %02d:%02d:%02d", t->tm_year + 1900, t->tm_mon + 1, t->tm_mday,
 30             t->tm_hour, t->tm_min, t->tm_sec);
 31
 32     strftime(mtime, sizeof(mtime), "%b %e %R" , t);
 33     printf("%s %s\n",mtime, *argv);
 34     return 0;
 35 }

```
```s
linux@ubuntu:~/0619$ ./a.out 2_mtime.c
Jun 18 19:01 2_mtime.c
```

```c
     switch (sb.st_mode & S_IFMT) {
           case S_IFBLK:  printf("b: block device\n");            break;
           case S_IFCHR:  printf("c: character device\n");        break;
           case S_IFDIR:  printf("d: directory\n");               break;
           case S_IFIFO:  printf("p: FIFO/pipe\n");               break;
           case S_IFLNK:  printf("l :symlink\n");                 break;
           case S_IFREG:  printf("- :regular file\n");            break;
           case S_IFSOCK: printf("s :socket\n");                  break;
             default:       printf("unknown?\n");                break;
       }
       if(S_ISBLK(sb.st_mode) || S_ISCHR(sb.st_mode)) {
            printf("%u, %u",  major(sb.st_rdev), minor(sb.st_rdev));
      }
      else {
          printf("%ld\n",sb.st_size);
      }

```

```c
#include <sys/types.h>
#include <dirent.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <errno.h>
#include <string.h>

// 하위 디렉터리 탐색을 위한 함수를 구현합니다.
int listDir(const char *dname) {
	if (dname == NULL || strlen(dname) == 0) {
		fprintf(stderr, "listDir: argument is wrong\n");
		return -1;
	}

	// 1. 해당 디렉터리로 이동
	if (chdir(dname) == -1) {
		perror("chdir");
		return -1;
	}

	// 2. 해당 디렉터리 경로 출력
	char curPath[256];
	if (getcwd(curPath, sizeof(curPath)) == NULL) {
		perror("getcwd");
		return -1;
	}
	printf("\n%s:\n", curPath);

	// 3. 해당 디렉터리를 오픈
	DIR *dir = opendir(".");
	if (dir == NULL) {				 	
		perror("opendir");		
		return -1;								
	}											

	// 4. 디렉터리 안의 내용을 출력
	while (1) {
		errno = 0;
		struct dirent *p = readdir(dir);	
		if (p == NULL) {	// EOF or ERROR
			if (errno != 0) {
				perror("readdir");
				return -1;
			}
			break;
		}

		if (strcmp(p->d_name, ".") && strcmp(p->d_name, "..")) {
			printf("%s\n", p->d_name);

			if (p->d_type == DT_DIR) {	// 현재 파일이 디렉터리인 경우, 재귀 호출
				if (listDir(p->d_name) == -1) 
					break;
			}
		}
	}

	// 5. 현재 디렉터리를 닫고 상위 디렉터리로 이동
	if (closedir(dir) == -1) {		
		perror("closedir");
		return -1;
	}

	if (chdir("..") == -1) {
		perror("chdir");
		exit(1);
	}

	return 0;
}

int main(int argc, char **argv) {
	if (argc != 2) {
		fprintf(stderr, "usage: %s DIRECTORY\n", *argv);
		return -1;
	}
	--argc, ++argv;
	listDir(*argv);
	return 0;
}
```
>디렉터리에 대해서 하드링크로 접근하면 무한루프에 빠지게된다 <br/>
> a.out - > .. -> a.out -> -> <br/>
> .  ..  에 대해서 

---
```c
#include <sys/types.h>
#include <dirent.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <errno.h>
#include <string.h>
typedef struct Node {
    char dname[256];
    struct Node *next;
} Node;
int insert(Node *head, const char *dname) {
    if(head ==NULL || dname ==NULL) {
        fprintf(stderr, "insert : argument is null\n");
        return -1;
    }
    Node *node=calloc(1, sizeof(Node));

    strcp(node->dname, dname);

    node->next= head->next;
    head->next= node;

    return 0;

}
// 하위 디렉터리 탐색을 위한 함수를 구현합니다.
int listDir(const char *dname) {
	if (dname == NULL || strlen(dname) == 0) {
		fprintf(stderr, "listDir: argument is wrong\n");
		return -1;
	}

	// 1. 해당 디렉터리로 이동
	if (chdir(dname) == -1) {
		perror("chdir");
		return -1;
	}

	// 2. 해당 디렉터리 경로 출력
	char curPath[256];
	if (getcwd(curPath, sizeof(curPath)) == NULL) {
		perror("getcwd");
		return -1;
	}
	printf("\n%s:\n", curPath);

	// 3. 해당 디렉터리를 오픈
	DIR *dir = opendir(".");
	if (dir == NULL) {				 	
		perror("opendir");		
		return -1;								
	}											

	// 4. 디렉터리 안의 내용을 출력
    Node head = {0, } // 단순 연결 리스트의 더미 헤드
	while (1) {
		errno = 0;
		

		if (strcmp(p->d_name, ".") && strcmp(p->d_name, "..")) {
			printf("%s\n", p->d_name);

			if (p->d_type == DT_DIR) {	// 현재 파일이 디렉터리인 경우, 재귀 호출
				insert(&head, p->d_name);//if (listDir(p->d_name) == -1)	{ break;
			} 
		}
	}
    //5. 하위 디렉터리 순회

	// 5. 현재 디렉터리를 닫고 상위 디렉터리로 이동
	if (closedir(dir) == -1) {		
		perror("closedir");
		return -1;
	}

	if (chdir("..") == -1) {
		perror("chdir");
		exit(1);
	}

	return 0;
}

int main(int argc, char **argv) {
	if (argc != 2) {
		fprintf(stderr, "usage: %s DIRECTORY\n", *argv);
		return -1;
	}
	--argc, ++argv;
	listDir(*argv);
	return 0;
}
```
```c
#include <sys/types.h>
#include <dirent.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <errno.h>
#include <string.h>

// 하위 디렉터리 탐색을 위한 함수를 구현합니다.
int listDir(const char *dname) {
	if (dname == NULL || strlen(dname) == 0) {
		fprintf(stderr, "listDir: argument is wrong\n");
		return -1;
	}

	// 1. 해당 디렉터리로 이동
	if (chdir(dname) == -1) {
		perror("chdir");
		return -1;
	}

	// 2. 해당 디렉터리 경로 출력
	char curPath[256];
	if (getcwd(curPath, sizeof(curPath)) == NULL) {
		perror("getcwd");
		return -1;
	}
	printf("\n%s:\n", curPath);

	// 3. 해당 디렉터리를 오픈
	DIR *dir = opendir(".");
	if (dir == NULL) {				 	
		perror("opendir");		
		return -1;								
	}											

	// 4. 디렉터리 안의 내용을 출력
	while (1) {
		errno = 0;
		struct dirent *p = readdir(dir);	
		if (p == NULL) {	// EOF or ERROR
			if (errno != 0) {
				perror("readdir");
				return -1;
			}
			break;
		}
			printf("%s\n", p->d_name);
	}

	// 5. 현재 디렉터리를 닫고 상위 디렉터리로 이동
	if (closedir(dir) == -1) {		
		perror("closedir");
		return -1;
	}

	if (chdir("..") == -1) {
		perror("chdir");
		exit(1);
	}

	return 0;
}

int main(int argc, char **argv) {
	if (argc != 2) {
		fprintf(stderr, "usage: %s DIRECTORY\n", *argv);
		return -1;
	}
	--argc, ++argv;
	listDir(*argv);
	return 0;
}
```
---
## 시그널(SIGNAL)

1. 개념    
        
        프로세스 사이의 동기화 또는 통신을 위해 사용되는 메커니즘

시그널은 아래와 같이 전송될 수 있음
    -   한 프로세스가 다른 프로세스에게 전송
    -   커널이 프로세스에게 전송
    -   소프트웨어 인터럽트


2. 시그널의 발생
    -   인위적으로 발생 
        -   ex) kill 명령어 or 함수
        -   이벤트 발생 ex) 알람, 프로세스 종료
        -   에러가 발생 ex) 잘못된 메모리 참조
        -   외부상황 발생 ex) CTRL + C
---
### 시그널 처리 방법
1.  무시
2.  보류(pending)
3.  종료
4.  처리(handling)

만약 시그널에 대하여 아무런 처리를 하지 않으면 프로세스는 기본적으로 종료된다

아래의 시그널들은 처리할 수없다.
-   SIGKILL
-   SIGSTOP
-   
----

#### alarm
```
NAME
       alarm - set an alarm clock for delivery of a signal

SYNOPSIS
       #include <unistd.h>

       unsigned int alarm(unsigned int seconds);

DESCRIPTION
       alarm()  arranges  for  a  SIGALRM signal to be delivered to the calling process in
       seconds seconds.

       If seconds is zero, any pending alarm is canceled.

       In any event any previously set alarm() is canceled.

RETURN VALUE
       alarm() returns the number of seconds  remaining  until  any  previously  scheduled
       alarm was due to be delivered, or zero if there was no previously scheduled alarm.

```
```c
  7 #include <stdio.h>
  8 #include <unistd.h>
  9
 10 int main (){
 11     alarm(10);
 12     while(1) // 아무런 처리를 하지 않으면 프로그램이 그냥 종료되기 때문에 while을 돌려준다
 13         ;
 14     return 0;
 15 }

```
```s
linux@ubuntu:~/0619$ gcc 5_signal.c
linux@ubuntu:~/0619$ ./a.out
Alarm clock #10초가 지나고 출력된 모습
```
---
#### signal
```
NAME
       signal - ANSI C signal handling

SYNOPSIS
       #include <signal.h>

       typedef void (*sighandler_t)(int);

       sighandler_t signal(int signum, sighandler_t handler);

DESCRIPTION
       The  behavior of signal() varies across UNIX versions, and has also varied historically
       across different versions of Linux.  Avoid its  use:  use  sigaction(2)  instead.   See
       Portability below.

       signal() sets the disposition of the signal signum to handler, which is either SIG_IGN,
       SIG_DFL, or the address of a programmer-defined function (a "signal handler").

       If the signal signum is delivered to the process, then one of the following happens:

       *  If the disposition is set to SIG_IGN, then the signal is ignored.

       *  If the disposition is set to SIG_DFL, then the default action  associated  with  the
          signal (see signal(7)) occurs.

       *  If  the disposition is set to a function, then first either the disposition is reset
          to SIG_DFL, or the signal is blocked (see Portability below), and  then  handler  is
          called  with  argument signum.  If invocation of the handler caused the signal to be
          blocked, then the signal is unblocked upon return from the handler.

       The signals SIGKILL and SIGSTOP cannot be caught or ignored.

RETURN VALUE
       signal() returns the previous value of the signal handler, or SIG_ERR on error.  In the
       event of an error, errno is set to indicate the cause.

```
```c
  7 #include <stdio.h>
  8 #include <unistd.h>
  9 #include <signal.h>
 10 void sigHandler(int signo) {
 11     printf("SIGALRM!\n");
 12     alarm(1);
 13 }
 14 int main (){
 15     if(signal(SIGALRM, sigHandler) == SIG_ERR) { //== trap sigHandler SIGALRM
 16         perror("signal");                        // trap sigHandler SIGINT
 17         return -1;                               // 프로세스에는 하나이상의 signal을 등록할 >    수 있다.
 18     }
 19
 20     alarm(10);
 21     while(1)
 22         ;
 23     return 0;
 24 }
```
```c
  1 // 5_signal.c
  2
  3 // 알람 시그널 : 알람 함수에 의해 발생되는 시그널
  4 // 알람 함수에 시간(초)를 전달하고 지정된 시간이 지나면 알람 함수를 수행한
  5 // 프로세스에게 SIGALRM을 보냄
  6
  7 #include <stdio.h>
  8 #include <unistd.h>
  9 #include <signal.h>
 10
 11 //프로세스는 하나 이상의 시그널을 등록할 수 있음
 12
 13 void SIGALRM_Handler(int signo) {
 14     printf("SIGALRM!\n");
        alarm(1);
 15 }
 16
 17 void SIGINT_Handler(int signo) {
 18     printf("SIGINT\n");
 19 }
 20 int main (){
 21     if(signal(SIGALRM, SIGALRM_Handler == SIG_ERR) {
 22         perror("signal");
 23         return -1;
 24     }
 25
 26     if(signal(SIGINT, SIGINT_Handler == SIG_ERR) {
 27         perror("signal");
 28         return -1;
 29     }
 30     alarm(10);
 31     while(1)
 32         ;
 33     return 0;
 34 }
```
```c
  7 #include <stdio.h>
  8 #include <unistd.h>
  9 #include <signal.h>
 10
 11 //핸들러의 인자로는 발생된 시그널의 번호가 전달
 12 void sigHandler(int signo) {
 13     switch (signo) {
 14         case SIGALRM:
 15             printf("SIGARLM\n");
 16             alarm(1);
 17             break;
 18         case SIGINT:
 19             printf("SIGINT");
 20             break;
 21     }
 22 }
 23 void SIGALRM_Handler(int signo) {
 24     printf("SIGALRM!\n");
 25     alarm(1);
 26 }
 27
 28 void SIGINT_Handler(int signo) {
 29     printf("SIGINT\n");
 30 }
 31 int main (){
 32     if(signal(SIGALRM, sigHandler)== SIG_ERR) {
 33         perror("signal");
 34         return -1;
 35     }
 36
 37     if(signal(SIGINT, sigHandler) == SIG_ERR) {
 38         perror("signal");
 39         return -1;
 40     }
 42     while(1)
 43         ;
 44     return 0;
 45 }
```
> 시그널을 무시한다는 것은 핸들러 안에서 아무것도 하지 않는 것을 의미하는게 아니라
> 핸들러가 아무런 일을 하지 않는다 해도
> 처리를 한것이나 다름없음
> 시그널을 무시하려면 SIG_IGN(IGN : ignore)
```c
 17     if(signal(SIGINT, SIG_IGN) == SIG_ERR) { //signal을 받지만 받고 ignore해준다
 18         perror("signal");
 19         return -1;
 20     }
```
#### 시그널 펜딩(보류)
> 내부의 프로세스가 방해받지 않게 하고싶다<br/>
> 혹시나 SIGINT가 오게되면 핸들러를 통해 보낸다<br/>
```
무언가 동작중에 SIGINT가 오면 SIGNAL을 처리하기위해 하던일으 멈춰야 한다.
하지만 작업이 도중 정지되면 안된다고 한다면

그전 작업에 쓰이던 데이터는 쓸 수 가 없게된다.

코딩을 하다보면 어쩔 수 없이 시그널을 받을 수 밖에 없다

이러한 상황을 위해 시그널 블럭을 시켜놓는다

지연이라는 개념 -delay 출발하는 시점이 지연된 것 아예 출발이 안됨
               -pending 출발이 되긴 되는데 아직은 안된것 지금말고 나중에 하겠다

```
어떤 프로세스에 시그널이 발생되었을 때, 시그널을 미리 등록해 <br> 두었다면 핸들러가 호출된다<br/>
핸들러를 등록하지 않았다면 기본적으로 종료됨<br/>

만약 중요한 일을 하는 시점에 시그널을 받지 않고 보류시키고 싶다면<br/>
sigprocmask 함수를 사용하면 된다.
```
NAME
       sigprocmask, rt_sigprocmask - examine and change blocked signals

SYNOPSIS
       #include <signal.h>

       /* Prototype for the glibc wrapper function */
       int sigprocmask(int how, const sigset_t *set, sigset_t *oldset);

       /* Prototype for the underlying system call */
       int rt_sigprocmask(int how, const kernel_sigset_t *set,
                          kernel_sigset_t *oldset, size_t sigsetsize);

       /* Prototype for the legacy system call (deprecated) */
       int sigprocmask(int how, const old_kernel_sigset_t *set,
                       old_kernel_sigset_t *oldset);

   Feature Test Macro Requirements for glibc (see feature_test_macros(7)):

       sigprocmask(): _POSIX_C_SOURCE
```
```c

```
> int sigprocmask(int how, const old_kernel_sigset_t *set, old_kernel_sigset_t *oldset);

HOW의 값에 따라 동작 방식이 달라진다.

1. SIG_SETMASK : 시그널 마스크를 set으로 변경
2. SIG_BLOCK : 시그널 마스크에 set에 포함된 시그널을 추가한다.
3. SIG_UNBLOCK : 시그널 마스크에 set에 포함된 시그널을 제거한다.

oldset이 NULL이 아니라면 이전 시그널 모음을 oldset에 저장한다
set이 NULL이라면 how를 무시하고 시그널 마스크를 oldset에 저장한다.
```c
#include <unistd.h>
#include <signal.h>
#include <stdio.h>

// 시그널 펜딩(보류)
// 1. 차단과 해제
void showMask() {
	sigset_t curMask;
	if (sigprocmask(0, NULL, &curMask) == -1) {
		perror("sigprocmask");
		return;
	}

	printf("blocked signal list: ");
	if (sigismember(&curMask, SIGINT)) printf("SIGINT ");
	if (sigismember(&curMask, SIGQUIT)) printf("SIGQUIT ");
	if (sigismember(&curMask, SIGALRM)) printf("SIGALRM ");
	printf("\n");
}

int main() {
	// 시그널 마스크 데이터 생성 및 초기화
	sigset_t newMask;
	if (sigemptyset(&newMask) == -1) {
		perror("sigemptyset");
		return -1;
	}

	// 차단할 시그널을 설정
	if (sigaddset(&newMask, SIGINT) == -1) {
		perror("sigaddset");
		return -1;
	}

	// 차단할 시그널을 등록
	sigset_t oldMask;
	if (sigprocmask(SIG_BLOCK, &newMask, &oldMask) == -1) {
		perror("sigprocmask");
		return -1;
	}

	// 차단할 시그널 목록을 확인
	showMask();
	getchar();


	// 이전 시그널로 복원하고 싶은 경우 
	if (sigprocmask(SIG_SETMASK, &oldMask, NULL) == -1) {
		perror("sigprocmask");
		return -1;
	}
	showMask();

	return 0;
}
```