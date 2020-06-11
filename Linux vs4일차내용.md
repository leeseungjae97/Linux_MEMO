# 1. Grep
      Global REgex Print의 약자 정규 표현식과 일치하는 패턴 출력 명령어

```powershell

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

```

# 2. 정규표현식
    Regular Expression 또는 Regex라고 하며 규칙을 가진 문자열 집합을 말한다

    -메타문자
        일반적인 문자들은 리터럴 문자라고한다 : 그대로 해석되는 문자
        메타문자는 정규표현식에 단순 문자로 해석되는것이 아니라 다른 의미로 해석되는 문자
    참고링크 : https://ko.wikipedia.org/wiki/%EC%A0%95%EA%B7%9C_%ED%91%9C%ED%98%84%EC%8B%9D
     ex> ^ $ . [] {} = ? * + () | ...
        위 와 같은 메타문자를 기본정규표현식(Base Regular Expression, BRE)라고 한다.
       
- 1.  . : 임의의 1개의 문자와 일치하는 메타 문자.
```powershell
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
```

- 2. ^ : 특정 패턴으로 시작되는 것을 검색 할 때 사용

          
```powershell
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

```

- 3 . & : 특정 패턴으로 끝나는 것을 검색 할 때 사용

```powershell

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
```
```powershell
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
```
```powershell
        1. [] : 문자집합중에 특정 문자와 일치하는지 확인 
            linux@ubuntu:~/0611$ grep '[123][123]' sample.txt
            411toppm
            base32
            crc32
            linux32
            m2300w
            m2300w-wrapper
```
```powershell
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
```
```powershell
        2. * : *앞의 문자가 0개 이상 반복되는 것을 표현한 메타문자
            linux@ubuntu:~/0611$ echo "hello \
            > www
            > world" | grep 'w*'

            hello www
            world
            # ex> ab aab aaab aaaab aaaaab a...b
```
        
        하지만 쓰다보니 기본정규표현식만으로 표현할 수 없는 것도 생겨 확장되었다.
        BRE () {} ? + | : 확장정규표현식(Extended Regular Expression, ERE)
- 1. | : 대안(alternative)의 or 개념
```powershell
              #어떤 파일에서 bz 또는 gz 또는 zip이 포함되어 있는 패턴을 찾고 싶은 경우
              #grep에서 확장정규표현식을 해석하려면 -e 옵션을 써주어야한다.
              linux@ubuntu:~/0611$ grep -E 'bz|gz|zip' sample.txt
                zip
                bunzip2
                bzcat
                bzcmp
                bzdiff
                bzegrep

              #혹은 egrep을 써주어도 된다.
```
- 2. () : 검색을 위해 메타문자가 아닌 정규표현식의 요소를 결합하여 사용
```powershell
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
```
- 1. ? : 앞의 문자가 0또는 1회 반복되는 패턴 
```powershell
              linux@ubuntu:~/0611$ echo "http://xxx.com
              https://xxx.com
              www.xxx.com" | egrep "https?"
              #https의 앞문자 즉 's'가 없거나 하나 있는 경우를 검색.
              http://xxx.com
              https://xxx.com
```
- 2. (+) : 앞의 문자가 1번 이상 반복 
```c
      그러나 사용에 어려움이 따른다.. 몇번 반복하는건지 사용하는 입장에서 모름
```
- 3. {N} : 앞의 문자가 N번 반복
```powershell
              linux@ubuntu:~/0611$ echo "www.xyz.com
              ftp.xyz.com
              xyz.com" | egrep "w{3}"# w가 3번 반복
              www.xyz.com 
              5.1 {MIN,MAX} : 앞의 문자가 MIN 혹은 MIN~MAX 만큼 반복
                linux@ubuntu:~/0611$ echo "www.xyz.com
                ftp.xyz.com
                xyz.com" | egrep "w{0,3}" #w가 최소 0번 최대 3번 반복
                www.xyz.com
                ftp.xyz.com
                xyz.com

                linux@ubuntu:~/0611$ echo "www.xyz.com
                http://ftp.xyz.com
                https://xyz.com
                htt://hhh.com" | egrep "https{0,1}"
                http://ftp.xyz.com #s가 {0,1}도 포함되어있다. 즉 http(s{0,1}){0,1} 이런느낌
                https://xyz.com 
```

    파일 작업을 하다보면 다수의 파일을 하나의 파일로 묶어어야 하는 경우 발생
      이처럼 다수의 파일을 하나로 묶는 작업 Archiving

      이를 위해 유닉스 또는 리눅스는 tar 명령어 제공

```powershell

Usage: tar [OPTION...] [FILE]...
GNU 'tar' saves many files together into a single tape or disk archive, and can
restore individual files from the archive.

Examples:
  tar -cf archive.tar foo bar  # Create archive.tar from files foo and bar.
  tar -tvf archive.tar         # List all files in archive.tar verbosely.
  tar -xf archive.tar          # Extract all files from archive.tar.
```
 Local file name selection:

          --add-file=FILE        add given FILE to the archive (useful if its name starts with a dash)
      -C, --directory=DIR        change to directory DIR
          --exclude=PATTERN      exclude files, given as a PATTERN
          --exclude-backups      exclude backup and lock files
          --exclude-caches       exclude contents of directories containing
                                CACHEDIR.TAG, except for the tag file itself
          --exclude-caches-all   exclude directories containing CACHEDIR.TAG
          --exclude-caches-under exclude everything under directories containing
                                CACHEDIR.TAG
          --exclude-ignore=FILE  read exclude patterns for each directory from
                                FILE, if it exists
          --exclude-ignore-recursive=FILE
                                read exclude patterns for each directory and its
                                subdirectories from FILE, if it exists
          --exclude-tag=FILE     exclude contents of directories containing FILE,
                                except for FILE itself
          --exclude-tag-all=FILE exclude directories containing FILE
          --exclude-tag-under=FILE   exclude everything under directories
                                containing FILE
          --exclude-vcs          exclude version control system directories
          --exclude-vcs-ignores  read exclude patterns from the VCS ignore files
          --no-null              disable the effect of the previous --null option
          --no-recursion         avoid descending automatically in directories
          --no-unquote           do not unquote input file or member names
          --no-verbatim-files-from   -T treats file names starting with dash as
                                options (default)
          --null                 -T reads null-terminated names; implies
                                --verbatim-files-from
          --recursion            recurse into directories (default)
      -T, --files-from=FILE      get names to extract or create from FILE
          --unquote              unquote input file or member names (default)
          --verbatim-files-from  -T reads file names verbatim (no option handling)
      -X, --exclude-from=FILE    exclude patterns listed in FILE


 File name matching options (affect both exclude and include patterns):

      --anchored             patterns match file name start
      --ignore-case          ignore case
      --no-anchored          patterns match after any '/' (default for
                             exclusion)
      --no-ignore-case       case sensitive matching (default)
      --no-wildcards         verbatim string matching
      --no-wildcards-match-slash   wildcards do not match '/'
      --wildcards            use wildcards (default for exclusion)
      --wildcards-match-slash   wildcards match '/' (default for exclusion)

 Main operation mode:

    -A, --catenate, --concatenate   append tar files to an archive
    -c, --create               create a new archive
    -d, --diff, --compare      find differences between archive and file system
    --delete               delete from the archive (not on mag tapes!)
    -r, --append               append files to the end of an archive
    -t, --list                 list the contents of an archive
        --test-label           test the archive volume label and exit
    -u, --update               only append files newer than copy in archive
    -x, --extract, --get       extract files from an archive

 Operation modifiers:

      --check-device         check device numbers when creating incremental
                             archives (default)
    -g, --listed-incremental=FILE   handle new GNU-format incremental backup
    -G, --incremental          handle old GNU-format incremental backup
        --hole-detection=TYPE  technique to detect holes
        --ignore-failed-read   do not exit with nonzero on unreadable files
        --level=NUMBER         dump level for created listed-incremental archive
    -n, --seek                 archive is seekable
      --no-check-device      do not check device numbers when creating
                             incremental archives
      --no-seek              archive is not seekable
      --occurrence[=NUMBER]  process only the NUMBERth occurrence of each file
                             in the archive; this option is valid only in
                             conjunction with one of the subcommands --delete,
                             --diff, --extract or --list and when a list of
                             files is given either on the command line or via
                             the -T option; NUMBER defaults to 1
      --sparse-version=MAJOR[.MINOR]
                             set version of the sparse format to use (implies
                             --sparse)
    -S, --sparse               handle sparse files efficiently

 Overwrite control:

    -k, --keep-old-files       don't replace existing files when extracting,
                              treat them as errors
        --keep-directory-symlink   preserve existing symlinks to directories when
                              extracting
        --keep-newer-files     don't replace existing files that are newer than
                              their archive copies
        --no-overwrite-dir     preserve metadata of existing directories
        --one-top-level[=DIR]  create a subdirectory to avoid having loose files
                              extracted
        --overwrite            overwrite existing files when extracting
        --overwrite-dir        overwrite metadata of existing directories when
                              extracting (default)
        --recursive-unlink     empty hierarchies prior to extracting directory
        --remove-files         remove files after adding them to the archive
        --skip-old-files       don't replace existing files when extracting,
                              silently skip over them
    -U, --unlink-first         remove each file prior to extracting over it
    -W, --verify               attempt to verify the archive after writing it

 Select output stream:

      --ignore-command-error ignore exit codes of children
      --no-ignore-command-error   treat non-zero exit codes of children as
                             error
    -O, --to-stdout            extract files to standard output
      --to-command=COMMAND   pipe extracted files to another program

 Handling of file attributes:

      --atime-preserve[=METHOD]   preserve access times on dumped files, either
                             by restoring the times after reading
                             (METHOD='replace'; default) or by not setting the
                             times in the first place (METHOD='system')
      --clamp-mtime          only set time when the file is more recent than
                             what was given with --mtime
      --delay-directory-restore   delay setting modification times and
                             permissions of extracted directories until the end
                             of extraction
      --group=NAME           force NAME as group for added files
      --group-map=FILE       use FILE to map file owner GIDs and names
      --mode=CHANGES         force (symbolic) mode CHANGES for added files
      --mtime=DATE-OR-FILE   set mtime for added files from DATE-OR-FILE
     -m, --touch                don't extract file modified time
      --no-delay-directory-restore
                             cancel the effect of --delay-directory-restore
                             option
      --no-same-owner        extract files as yourself (default for ordinary
                             users)
      --no-same-permissions  apply the user's umask when extracting permissions
                             from the archive (default for ordinary users)
      --numeric-owner        always use numbers for user/group names
      --owner=NAME           force NAME as owner for added files
      --owner-map=FILE       use FILE to map file owner UIDs and names
     -p, --preserve-permissions, --same-permissions
                             extract information about file permissions
                             (default for superuser)
      --same-owner           try extracting files with the same ownership as
                             exists in the archive (default for superuser)
      -s, --preserve-order, --same-order
                             member arguments are listed in the same order as
                             the files in the archive
      --sort=ORDER           directory sorting order: none (default), name or
                             inode

 Handling of extended file attributes:

      --acls                 Enable the POSIX ACLs support
      --no-acls              Disable the POSIX ACLs support
      --no-selinux           Disable the SELinux context support
      --no-xattrs            Disable extended attributes support
      --selinux              Enable the SELinux context support
      --xattrs               Enable extended attributes support
      --xattrs-exclude=MASK  specify the exclude pattern for xattr keys
      --xattrs-include=MASK  specify the include pattern for xattr keys

 Device selection and switching:

      -f, --file=ARCHIVE         use archive file or device ARCHIVE
          --force-local          archive file is local even if it has a colon
      -F, --info-script=NAME, --new-volume-script=NAME
                                run script at end of each tape (implies -M)
      -L, --tape-length=NUMBER   change tape after writing NUMBER x 1024 bytes
      -M, --multi-volume         create/list/extract multi-volume archive
          --rmt-command=COMMAND  use given rmt COMMAND instead of rmt
          --rsh-command=COMMAND  use remote COMMAND instead of rsh
          --volno-file=FILE      use/update the volume number in FILE

    Device blocking:

      -b, --blocking-factor=BLOCKS   BLOCKS x 512 bytes per record
      -B, --read-full-records    reblock as we read (for 4.2BSD pipes)
      -i, --ignore-zeros         ignore zeroed blocks in archive (means EOF)
          --record-size=NUMBER   NUMBER of bytes per record, multiple of 512

 Archive format selection:

      -H, --format=FORMAT        create archive of the given format

 FORMAT is one of the following:

    gnu                      GNU tar 1.13.x format
    oldgnu                   GNU format as per tar <= 1.12
    pax                      POSIX 1003.1-2001 (pax) format
    posix                    same as pax
    ustar                    POSIX 1003.1-1988 (ustar) format
    v7                       old V7 tar format

      --old-archive, --portability
                             same as --format=v7
      --pax-option=keyword[[:]=value][,keyword[[:]=value]]...
                             control pax keywords
      --posix                same as --format=posix
      -V, --label=TEXT           create archive with volume name TEXT; at
                             list/extract time, use TEXT as a globbing pattern
                             for volume name

 Compression options:

      -a, --auto-compress        use archive suffix to determine the compression
                                program
      -I, --use-compress-program=PROG
                                filter through PROG (must accept -d)
      -j, --bzip2                filter the archive through bzip2
      -J, --xz                   filter the archive through xz
          --lzip                 filter the archive through lzip
          --lzma                 filter the archive through xz
          --lzop                 filter the archive through xz
          --no-auto-compress     do not use archive suffix to determine the
                                compression program
      -z, --gzip, --gunzip, --ungzip   filter the archive through gzip
      -Z, --compress, --uncompress   filter the archive through compress

 Local file selection:

          --backup[=CONTROL]     backup before removal, choose version CONTROL
      -h, --dereference          follow symlinks; archive and dump the files they
                                point to
          --hard-dereference     follow hard links; archive and dump the files they
                                refer to
      -K, --starting-file=MEMBER-NAME
                                begin at member MEMBER-NAME when reading the
                                archive
          --newer-mtime=DATE     compare date and time when data changed only
      -N, --newer=DATE-OR-FILE, --after-date=DATE-OR-FILE
                                only store files newer than DATE-OR-FILE
          --one-file-system      stay in local file system when creating archive
      -P, --absolute-names       don't strip leading '/'s from file names
          --suffix=STRING        backup before removal, override usual suffix ('~'
                                unless overridden by environment variable
                                SIMPLE_BACKUP_SUFFIX)

 File name transformations:

      --strip-components=NUMBER   strip NUMBER leading components from file
                             names on extraction
      --transform=EXPRESSION, --xform=EXPRESSION
                             use sed replace EXPRESSION to transform file
                             names

 Informative output:

          --checkpoint[=NUMBER]  display progress messages every NUMBERth record
                                (default 10)
          --checkpoint-action=ACTION   execute ACTION on each checkpoint
          --full-time            print file time to its full resolution
          --index-file=FILE      send verbose output to FILE
      -l, --check-links          print a message if not all links are dumped
          --no-quote-chars=STRING   disable quoting for characters from STRING
          --quote-chars=STRING   additionally quote characters from STRING
          --quoting-style=STYLE  set name quoting style; see below for valid STYLE
                                values
      -R, --block-number         show block number within archive with each message

          --show-defaults        show tar defaults
          --show-omitted-dirs    when listing or extracting, list each directory
                                that does not match search criteria
          --show-snapshot-field-ranges
                                show valid ranges for snapshot-file fields
          --show-transformed-names, --show-stored-names
                                show file or archive names after transformation
          --totals[=SIGNAL]      print total bytes after processing the archive;
                                with an argument - print total bytes when this
                                SIGNAL is delivered; Allowed signals are: SIGHUP,
                                SIGQUIT, SIGINT, SIGUSR1 and SIGUSR2; the names
                                without SIG prefix are also accepted
          --utc                  print file modification times in UTC
      -v, --verbose              verbosely list files processed
          --warning=KEYWORD      warning control
      -w, --interactive, --confirmation
                                ask for confirmation for every action

 Compatibility options:

      -o                         when creating, same as --old-archive; when
                             extracting, same as --no-same-owner

 Other options:

      -?, --help                 give this help list
          --restrict             disable use of some potentially harmful options
          --usage                give a short usage message
          --version              print program version

    Mandatory or optional arguments to long options are also mandatory or optional
    for any corresponding short options.

    The backup suffix is '~', unless set with --suffix or SIMPLE_BACKUP_SUFFIX.
    The version control may be set with --backup or VERSION_CONTROL, values are:

    none, off       never make backups
    t, numbered     make numbered backups
    nil, existing   numbered if numbered backups exist, simple otherwise
    never, simple   always make simple backups

    Valid arguments for the --quoting-style option are:
    shellscript
    -literal<br/>
    -shell<br/>
    -shell-always<br/>
    -c<br/>
    -c-maybe<br/>
    -escape<br/>
    -locale<br/>
    -clocale<br/>


아카이브 파일 생성 시, 확장자가 없지만 가독성의 이유로 .tar를 사용한다
- tar cvf 압축
- tar tf 열기
- tar xvf 해제
  
  - gzip, bzip2 : 리눅스에서 제공하고는 무손실 압출 프로그램
  - <gzip>
    gzip : Gun zip의 약자로 유닉스 시스템에서 쓰이던 압축 프로그램을 대체
      사용방법 gzip 파일명
      관례적인 의미로 .gzip을 쓴다.
```powershell
    linux@ubuntu:~/0611$ ls -lh
    total 11M < 읽을 수 있는 데이터 단위로 찍힌다.
    -rw-rw-r-- 1 linux linux 11M Jun 10 20:15 ls.txt
    -rw-rw-r-- 1 linux linux 17K Jun 10 18:16 sample.txt
    -rw-rw-r-- 1 linux linux 20K Jun 10 20:10 test.tar
    linux@ubuntu:~/0611$  

    linux@ubuntu:~/0611$ gzip ls.txt < 압축
    total 1276
    drwxrwxr-x  2 linux linux    4096 Jun 10 20:17 ./
    drwxr-xr-x 16 linux linux    4096 Jun 10 18:00 ../
    -rw-rw-r--  1 linux linux 1256393 Jun 10 20:15 ls.txt.gz < 압축된 모습
    
    linux@ubuntu:~/0611$ gunzip ls.txt.gz < 압축 해제
    drwxrwxr-x  2 linux linux     4096 Jun 10 20:18 ./
    drwxr-xr-x 16 linux linux     4096 Jun 10 18:00 ../
    -rw-rw-r--  1 linux linux 10830726 Jun 10 20:15 ls.txt < 압축을 해제하면 gzip이 없어진다.
    -rw-rw-r--  1 linux linux    16833 Jun 10 18:16 sample.txt
    -rw-rw-r--  1 linux linux    20480 Jun 10 20:10 test.tar
```
ls -R | gzip >ls.txt.gz

일반적으로 압축은 하나 이상의 파일에 대하여 수행
  하지만 매번 tar와 gzip명령어를 개별적으로 사용하면 생산성이 떨어짐
  이를 해결하기 위해 파이프 라인과 리다이렉션 사용

```powershell
  $tar cv | gzip > test.tar.gz

  tar에서는 archiving과 동시에 압축을 수행할 수 있는 z 옵션제공
    linux@ubuntu:~/0611$ tar cvzf test.tar.gz *.txt
    sample.txt
    linux@ubuntu:~/0611$ ll
    total 1268
    drwxrwxr-x  2 linux linux    4096 Jun 10 20:39 ./
    drwxr-xr-x 16 linux linux    4096 Jun 10 18:00 ../
    -rw-rw-r--  1 linux linux 1256393 Jun 10 20:15 ls.txt.gz
    -rw-rw-r--  1 linux linux   16833 Jun 10 18:16 sample.txt
    -rw-rw-r--  1 linux linux      20 Jun 10 20:39 test.tar
    -rw-rw-r--  1 linux linux    7379 Jun 10 20:46 test.tar.gz

 
```
```powershell
   $tar xvzf test.tar.gz
    이런식으로 tar로 묶고 또 gzip로 묶는다면 .tgz 라는 형식으로 작성한다.
```

# 3. vim
    sudo apt install vim 을 통해 vim 설치
```powershell
linux@ubuntu:~/0611$ sudo apt install vim
[sudo] password for linux:
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  vim-runtime
Suggested packages:
  ctags vim-doc vim-scripts
The following NEW packages will be installed:
  vim vim-runtime
0 upgraded, 2 newly installed, 0 to remove and 85 not upgraded.
Need to get 6,589 kB of archives.
After this operation, 32.0 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
    ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...

```

## 3.1. vim의 모드
    vi을 통해 실행을 하게 되면 command mode로 진입하게 된다.

## 3.2. <noname>
![캡처](/assets/캡처.JPG)

    vi는 왜 이렇게 3개로 나누어 놨을까

## 3.3. <noname>
    vi를 만드는 사람이 기존 Window와 같은 단축키를 이용하려 했지만 기존 Terminal에서 쓰고있으므로 사용할 수 없다. 그렇게 만들어진게 명령모드이다.

          ed -> ex -> vi -> vim

## 3.4. 명령모드 
  
      기존에 타이핑해서 가지고 있는 값과 terminal의 명령어를 구분하기위해서 썻는데    명령모드에서는 해당 명령을 가지고있어서 해당 명령을 ctrl을 조합하지 않아도 해당하는 모든 키가 해당 명령어와 조합되어 있다.

      또한 사용자가 키를 원하는 명령어를 만들어 쓸 수 있게된다.

 ## 3.5. 명령모드 사용 <br/>
  ```powershell  
      linux@ubuntu:~/0611$ write [filename], w[filename]
      ex) w hello.txt
  ```

# 4. vi 편집기
## 4.1. 커서이동 
명령모드에서만 사용가능
```
  - h 왼쪽이동
  - l 오른쪽이동
  - k 위쪽이동
  - j 아래쪽이동  
```  
  #
## 4.2. 편집기능
```
  - i(insert) 커서 위치에 글자 삽입
  - I(Insert) 행 앞으로 이동하여 삽입
  - a(append) 커서 다음 위치에 글자 삽입
  - A(Apeend) 행 뒤로 이동하여 추가
  - o(open line) 커서 아래에 새로운 행을 삽입
  - O(Open line) 커서 위에 새로운 행을 삽입
```
```c
    #include <stdio.h>

    int main() {
      printf("hello, world\n"); //이쪽 라인에서 o 
      //이쪽으로 개행된다.
      return 0;
    }
```
```c
    #include <stdio.h>

    int main() {
      //이쪽으로 개행된다.
      printf("hello, world\n");//이쪽 라인에서 O
      return 0;
    }
```
  #
  ## 4.3. 저장과 종료
```
  - w or write [파일명] : 파일저장
  - w! 파일명 : 현재 내용을 파일에 덮어씀
  - q or quit : 종료
  - q! or quit! : 변경된 내용을 저장하지 않고 바로 종료
  - wq or x : 저장과 종료를 동시에 
```
  #
  ## 4.4. 삭제
편집모드에서 delete 나 backspace사용
명령모드에 삭제수행
```
  - x : 현재 커서에 있는문자 1개를 삭제(delete와 동일)
  - dd : 현재행을 삭제
  - D : 현재 커서에서 부터 끝까지 삭제
  - J : 현재 행에 위치한 개행 문자, 삭제 아래행 앞에 존재하는 공백은 삭제됨
```
  #
  ## 4.5. 복사 및 붙여넣기
   명령모드에서 수행
```
   - yy: 해당 행 단위로 복사 
   - p : 붙여넣기
```
#
  ## 4.6. 잘라내기
  명령모드에서 수행. 앞에서 설명한 삭제는 잘라내기 이다, 잘라내기 후 사용하지 않으면 이는 삭제된 것과 동일
```
  - x : 현재 커서에위치한 문자를 잘라냄
  - dd : 현재 행을 자라냄
  - D : 현재 위치부터 행의 끝부분 까지 잘라낸다.
```
  #
  ## 4.7. 취소 및 되돌리기(undo, redo)
```
  - u(undo) : 바로 이전에 수행했던 명령 하나를 취소
  - ctrl + r(redo) : 바로 이전에 취소했던 명령을 다시 실행
```
  #
  ## 4.8. 비주얼 모드(블럭지정)
  명령모드에서 수행
```
  - v(visual) : 문자 단위로 블럭 지정
```
```c
    #include <stdio.h>

    int main()/*v 를 누르면 블럭 지정.*/ {
      printf("hello, world\n);
      return 0;
    }
```
```
  - V(Visual) : 행 단위로 블럭 지정
  - ctrl + v : 열 단위로 블럭을 지정
```
        tip: 블럭 지정 후, ~를 누르면 대소문자 변환.
  #
  ## 4.9. 화면 스크롤
  명령모드에서 수행
```
  - ctrl + b(backward) : 한 화면 위로 스크롤
  - ctrl + f(forward) : 한 화면 아래로 스크롤
  - ctrl + u(up) : 한 화면의 반만 위로 스크롤
  - ctrl + d(down) : 한 화면의 반만 아래로 스크롤
```
  #
  ## 4.10. 치환
  ex 모드에서 수행
  - 형식 : 시작행,끝행s / 원래문자열 / 변경문자열 / 옵션 
```
    ex> 1~10행의 모든 Hello를 Bye로 변경 - :1,10s/Hello/Bye/g
    ex> 문서 전체의 모든 Hello를 Bye로 변경 - :%s/Hello/Bye/g
    ex> 현재 행에서 마지막 행 까지의 모든 Hello를 Bye로 변경 - :.,$s/Hello/Bye/g
```
  ## 4.11. 윈도우 모드
  명령모드
```
 ※windonw 모드 진입시 사용하는 단축키 : ctrl + w
  - 수평분할 : ctrl + w + s(split)
  - 수직분할 : ctrl + w + v(vertical)
  - 창 닫기 : ctrl + w +c(close)
  - 창 이동: ctrl + w + hjkl(좌아래위우)
```
```powershell
  - edit.  #자기자신의 디렉토리 열기
      만약에 윈도우처럼 탐색기로 올라가서 보고싶다면 edit. 로 열어서 본다면
      자신의 파일로 따라가기때문에 파일탐색기처럼 사용가능하다.
```