<grep>
    #Global REgex Print의 약자 정규 표현식과 일치하는 패턴 출력 명령어

Usage: grep [OPTION]... PATTERN [FILE]...
    Pattern selection and interpretation:
  -E, --extended-regexp     PATTERN is an extended regular expression
    '확장정규표현식 사용 시 사용되는 옵션'
  -F, --fixed-strings       PATTERN is a set of newline-separated strings
  -G, --basic-regexp        PATTERN is a basic regular expression (default)
  -P, --perl-regexp         PATTERN is a Perl regular expression
  -e, --regexp=PATTERN      use PATTERN for matching
  -f, --file=FILE           obtain PATTERN from FILE
  -i, --ignore-case         ignore case distinctions
    '패턴 검색 시, 대소문자 구분 X'
  -w, --word-regexp         force PATTERN to match only whole words
    '해당 단어에 대해 검색'
  -x, --line-regexp         force PATTERN to match only whole lines
  -z, --null-data           a data line ends in 0 byte, not newline
Miscellaneous:
  -s, --no-messages         suppress error messages
  -v, --invert-match        select non-matching lines
  -V, --version             display version information and exit
      --help                display this help text and exit

Output control:
  -m, --max-count=NUM       stop after NUM selected lines
  -b, --byte-offset         print the byte offset with output lines
  -n, --line-number         print line number with output lines
      --line-buffered       flush output on every line
  -H, --with-filename       print file name with output lines
  -h, --no-filename         suppress the file name prefix on output
      --label=LABEL         use LABEL as the standard input file name prefix
  -o, --only-matching       show only the part of a line matching PATTERN
  -q, --quiet, --silent     suppress all normal output
      --binary-files=TYPE   assume that binary files are TYPE;
                            TYPE is 'binary', 'text', or 'without-match'
  -a, --text                equivalent to --binary-files=text
  -I                        equivalent to --binary-files=without-match
  -d, --directories=ACTION  how to handle directories;
                            ACTION is 'read', 'recurse', or 'skip'
  -D, --devices=ACTION      how to handle devices, FIFOs and sockets;
                            ACTION is 'read' or 'skip'
  -r, --recursive           like --directories=recurse
    '하위 디렉터리의 파일까지 패턴 검색'
  -R, --dereference-recursive  likewise, but follow all symlinks
      --include=FILE_PATTERN  search only files that match FILE_PATTERN
      --exclude=FILE_PATTERN  skip files and directories matching FILE_PATTERN
      --exclude-from=FILE   skip files matching any file pattern from FILE
      --exclude-dir=PATTERN  directories that match PATTERN will be skipped.
  -L, --files-without-match  print only names of FILEs with no selectedlines
    '패턴이 포함되지 않는 file 출력'
  -l, --files-with-matches  print only names of FILEs with selected lines
    '패턴이 포함된 file 출력'
  -c, --count               print only a count of selected lines per FILE
    '패턴이 일치하는 행의 개수 출력'
  -T, --initial-tab         make tabs line up (if needed)
  -Z, --null                print 0 byte after FILE name

Context control:
  -B, --before-context=NUM  print NUM lines of leading context
  -A, --after-context=NUM   print NUM lines of trailing context
  -C, --context=NUM         print NUM lines of output context
  -NUM                      same as --context=NUM
      --color[=WHEN],
      --colour[=WHEN]       use markers to highlight the matching strings;
                            WHEN is 'always', 'never', or 'auto'
  -U, --binary              do not strip CR characters at EOL (MSDOS/Windows)
Pattern selection and interpretation:
  -E, --extended-regexp     PATTERN is an extended regular expression
  -F, --fixed-strings       PATTERN is a set of newline-separated strings
  -G, --basic-regexp        PATTERN is a basic regular expression (default)
  -P, --perl-regexp         PATTERN is a Perl regular expression
  -e, --regexp=PATTERN      use PATTERN for matching
  -f, --file=FILE           obtain PATTERN from FILE
  -i, --ignore-case         ignore case distinctions
  -w, --word-regexp         force PATTERN to match only whole words
  -x, --line-regexp         force PATTERN to match only whole lines
  -z, --null-data           a data line ends in 0 byte, not newline

Miscellaneous:
  -s, --no-messages         suppress error messages
  -v, --invert-match        select non-matching lines
  -V, --version             display version information and exit
      --help                display this help text and exit

Output control:
  -m, --max-count=NUM       stop after NUM selected lines
  -b, --byte-offset         print the byte offset with output lines
  -n, --line-number         print line number with output lines
     '패턴이 일치하는 행의 번호를 함께 출력'
      --line-buffered       flush output on every line
  -H, --with-filename       print file name with output lines
  -h, --no-filename         suppress the file name prefix on output
      --label=LABEL         use LABEL as the standard input file name prefix
  -o, --only-matching       show only the part of a line matching PATTERN
  -q, --quiet, --silent     suppress all normal output
      --binary-files=TYPE   assume that binary files are TYPE;
                            TYPE is 'binary', 'text', or 'without-match'
  -a, --text                equivalent to --binary-files=text
  -I                        equivalent to --binary-files=without-match
  -d, --directories=ACTION  how to handle directories;
                            ACTION is 'read', 'recurse', or 'skip'
  -D, --devices=ACTION      how to handle devices, FIFOs and sockets;
                            ACTION is 'read' or 'skip'
  -r, --recursive           like --directories=recurse
  -R, --dereference-recursive  likewise, but follow all symlinks
      --include=FILE_PATTERN  search only files that match FILE_PATTERN
      --exclude=FILE_PATTERN  skip files and directories matching FILE_PATTERN
      --exclude-from=FILE   skip files matching any file pattern from FILE
      --exclude-dir=PATTERN  directories that match PATTERN will be skipped.
  -L, --files-without-match  print only names of FILEs with no selected lines
  -l, --files-with-matches  print only names of FILEs with selected lines
  -c, --count               print only a count of selected lines per FILE
  -T, --initial-tab         make tabs line up (if needed)
  -Z, --null                print 0 byte after FILE name

Context control:
  -B, --before-context=NUM  print NUM lines of leading context
  -A, --after-context=NUM   print NUM lines of trailing context
  -C, --context=NUM         print NUM lines of output context
  -NUM                      same as --context=NUM
      --color[=WHEN],
      --colour[=WHEN]       use markers to highlight the matching strings;
                            WHEN is 'always', 'never', or 'auto'
  -U, --binary              do not strip CR characters at EOL (MSDOS/Windows)


<정규표현식>
    #Regular Expression 또는 Regex라고 하며 규칙을 가진 문자열 집합을 말한다
    -메타문자
        일반적인 문자들은 리터럴 문자라고한다 : 그대로 해석되는 문자
        메타문자는 정규표현식에 단순 문자로 해석되는것이 아니라 다른 의미로 해석되는 문자
    참고링크 : https://ko.wikipedia.org/wiki/%EC%A0%95%EA%B7%9C_%ED%91%9C%ED%98%84%EC%8B%9D
        ex> ^ $ . [] {} = ? * + () | ...
        위 와 같은 메타문자를 기본정규표현식(Base Regular Expression, BRE)라고 한다.
        1. . : 임의의 1개의 문자와 일치하는 메타 문자.
           # ex> zip 앞의 한문자 더 있는 문자를 찾고 싶을 때
             grep .zip *
             linux@ubuntu:~/0611$ grep -w .zip *
             gzip
        
             #1개 이상도 사용이 가능
             linux@ubuntu:~/0611$ grep -w '...zip' sample.txt 
             linux@ubuntu:~/0611$ grep -w 'g..z.p' sample.txt
             gunzip

             #만약 . 을 메타 문자가 아닌 리터럴 문자로 해석하게 하려면 백슬래시(\)를 사용한다.
           # ex> linux@ubuntu:~/0611$ echo "bzip \.zip" | grep 'zip'
               bzip \.zip

            검색을 위해 내용추가 linux@ubuntu:~/0611$ ls /usr/bin >>sample.txt
        2. ^ : 특정 패턴으로 시작되는 것을 검색 할 때 사용
           # ex> zip으로 시작되는 패턴을 찾고 싶은 경우
             linux@ubuntu:~/0611$ grep '^zip' sample.txt
             zip
             zip
             zipcloak
             zipdetails
             zipgrep
             zipinfo
             zipnote
             zipsplit
        3. & : 특정 패턴으로 끝나는 것을 검색 할 때 사용
           # ex> zip으로 끝나는 패턴을 찾고 싶은 경우
             linux@ubuntu:~/0611$ grep 'zip$' sample.txt
             zip
             gunzip
             gzip
             funzip
             gpg-zip
             mzip
             preunzip
             prezip
             unzip
             zip
            3-1 특정 단어만 있는 행을 검색
              # ex> zip단어만 검색
                linux@ubuntu:~/0611$ grep -w '^zip$' sample.txt
                zip
                zip

                linux@ubuntu:~/0611$ grep -w 'zip' sample.txt
                zip
                gpg-zip #하이푼으로 나뉘어져 있기 때문에 zip하나를 단어로 인식한다.
                zip
              # ^$ -> 공백문자

        4. [] : 문자집합중에 특정 문자와 일치하는지 확인 
            linux@ubuntu:~/0611$ grep '[123][123]' sample.txt
            411toppm
            base32
            crc32
            linux32
            m2300w
            m2300w-wrapper

            # ex> 대문자로 시작하는 패턴을 찾고싶은 경우
             linux@ubuntu:~/0611$ grep '^[[:upper:]][[:upper:]]' sample.txt
             GET
             HEAD
             POST
            
            # 해당 문자집합 이외의 집합을 표현하려면 ^을 이용
             linux@ubuntu:~/0611$ grep '^[^[:lower:]]' sample.txt
             [ #이것도 명령어 이다.
             411toppm
             GET
             HEAD
             POST

            # 숫자나 문자 집합
            linux@ubuntu:~/0611$ grep '[0-9A-Za-z]' sample.txt
            zip
            bash
            brltty
            bunzip2

            ...

            zipnote
            zipsplit
            zjsdecode
            zlib-flate

        5. * : *앞의 문자가 0개 이상 반복되는 것을 표현한 메타문자
            linux@ubuntu:~/0611$ echo "hello \
            > www
            > world" | grep 'w*'

            hello www
            world
            # ex> ab aab aaab aaaab aaaaab a...b

        
        하지만 쓰다보니 기본정규표현식만으로 표현할 수 없는 것도 생겨 확장되었다.
        BRE () {} ? + | : 확장정규표현식(Extended Regular Expression, ERE)
            1. | : 대안(alternative)의 or 개념
                어떤 파일에서 bz 또는 gz 또는 zip이 포함되어 있는 패턴을 찾고 싶은 경우
                grep에서 확장정규표현식을 해석하려면 -e 옵션을 써주어야한다.
                linux@ubuntu:~/0611$ grep -E 'bz|gz|zip' sample.txt
                 zip
                 bunzip2
                 bzcat
                 bzcmp
                 bzdiff
                 bzegrep
                #혹은 egrep을 써주어도 된다.
            2. () : 검색을 위해 메타문자가 아닌 정규표현식의 요소를 결합하여 사용
                linux@ubuntu:~/0611$ grep -E '^(bz|gz|zip)' sample.txt
                #정규표현식의 ^ 와 확장표현식의 | 를 동시에 사용. 
                 zip
                 bzcat
                 bzcmp
                 bzdiff
                 bzegrep
                 bzexe
                 bzfgrep
                 bzgrep
            3. ? : 앞의 문자가 0또는 1회 반복되는 패턴 
                linux@ubuntu:~/0611$ echo "http://xxx.com
                https://xxx.com
                www.xxx.com" | egrep "https?"
                #https의 앞문자 즉 's'가 없거나 하나 있는 경우를 검색.
                http://xxx.com
                https://xxx.com
            4. {}
            5. +



