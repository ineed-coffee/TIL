# 쉘 명령 정리

 

### :arrow_right:mkdir

- `make directory` 의 약어로 디렉토리를 생성한다.

```shell
$ mkdir [폴더명]
```

 

### :arrow_right:cd

- `change directory`의 약어로 명령을 실행할 디렉토리를 변경한다.

```shell
$ cd [폴더 경로]
```

※ `.` 혹은 `..` 로 상대경로를 활용할 수 있고 `~`를 활용하여 홈 디렉토리로 바로 이동이 가능하다.

 

### :arrow_right:ls

- `list`의 약어로 현재 디렉토리의 파일 목록을 보여준다.

```shell
$ ls -a
```

※ `-a` 옵션을 활용하면 디렉토리 내 모든 파일을 확인할 수 있다.

  

### :arrow_right: pwd

- 현재 디렉토리의 절대 경로를 출력

 

### :arrow_right: rm

- `remove` 의 약어로 폴더/파일을 삭제할 수 있다.

```shell
$ rm [파일명] # 삭제할 파일명을 입력
$ rm -r [폴더명] # 폴더 삭제시 recursive 한 옵션을 주어야 한다
```

 

### :arrow_right: touch

- CLI 에서 파일을 생성할 때 사용한다.

```shell
$ touch [파일명.확장자]
```

 

### :arrow_right: cat

- CLI 에서 파일의 내용을 출력할 때 사용한다.

```shell
$ cat [파일명]
```

  


### :arrow_right: cp

- `copy` 의 약어로 파일/폴더를 복사한다.

```shell
$ cp [파일 or 폴더명] [경로]
```

※ rm 과 마찬가지로 폴더를 복사 시 -r 옵션이 필수다.

 

### :arrow_right: mv 

- `move` 의 약어로 파일/폴더를 복사한다.

```shell
$ mv [파일 or 폴더명] [경로]
```

※ 파일의 이름을 변경 시에도 활용 가능하다. _mv [기존 파일명] [새로운 파일명]_



### :arrow_right: echo

- 파일의 출력 / 생성이 모두 가능한 명령이다.

```shell
$ echo 'hello'  # 터미너에 hello 가 출력된다.
```

```shell
$ echo 'hello' > [파일명] # 'hello' 내용이 담긴 파일이 현재 디렉토리에 생성된다.
```

