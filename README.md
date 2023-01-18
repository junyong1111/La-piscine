### C Piscine Shell 00

1. **Exercise 00**

- **cat명령어를 사용하여 지정된 파일에 내용을 확인**
    - e 옵션을 주면 개행 여부도 확인이 가능하다
2. **Exercise 01**

    - **ls명령어로 현재 경로에 있는 폴더 및 파일을 확인하고 정보를 수정**
        - l 옵션 : 퍼미션(권한)정보, 소유권, 소유그룹, 파일(폴더)용량, 생성날짜, 파일(폴더)이름
        
        --# 파일의 경우 퍼미션(권한)정보 앞에 '-'로 표시가 되며 폴더의 경우 'd'로 표시가 된다.  
        --# chmod 명령어로 퍼미션 정보를 수정이 가능하다 4:read, 2:write, 1:execute
        
3. **Exercise 02**

    - **폴더 및 파일을 만들어 해당 파일 및 폴더와 하드링크, 소프트(심볼릭)링크를 연결**
        - 하드링크
            - 바로가기와 비슷하지만 파일이 아닌 원본 파일이 가르키는 파일시스템 데이터를 가르키며 원본이 삭제되어도 유지가 된다는 특징이 존재한다.
            - 하드링크는 원본과 i-node 번호가 같고 링크 개수가 증가
            - 사용법
                
                ```bash
                ln 원본파일 하드링크파일
                ```
                
        - 소프트링크
            - 바로가기라고 생각하면 된다. 원본이 삭제되면 하드링크와 달리 사용이 불가능하다.
            - 소프트링크는 원본과 i-node 번호가 다르고 링크 개수도 증가하지 않는다.
            - 사용법
                
                ```bash
                ln -s 원본파일 하드링크파일
                ```
                
        
        —# touch -t 옵션을 사용하면 파일에 시간 수정이 가능 (년원일시간)
        
        ```bash
        touch -t 202301011212 파일명
        ```
    

    
        —# touch -h -t 옵션을 사용하면 심볼릭 파일에도 적용 가능
        
        ```bash
        touch -h -t 202301011212 파일명
        ```
        
4. **Exercise 03**

- **ssh-keygen 프로그램을 사용하여 공개키와 개인키 생성**
    - Key 생성 방법
        
        ```bash
        cd ~/.ssh #-- ssh 정보가 저장되어 있는 디렉토리로 이동
        ssh-keygen #-- 기본적으로 내장된 keygen 프로그램을 이용하여 개인키와 공용키 발급
        ls #-- 해당 명령어로 .pub 공용키 내용 확인
        ```
        
    - 공개키는 git 저장소에 등록하고 개인키는 자신이 보관 한다.
    - 개인키를 통해 ssh 접속 후 개인키와 매칭되는 공개키를 이용하여 저장소에 접근이 가능.

5. **Exercise 04**

- l**s 명령에서 여러가지 옵션을 사용**
    - -t : 출력 결과를 파일의 수정시간으로 정렬
    - -m : 파일을 ‘,’로 구분함
    - -p : 폴더를 ‘/’로 구분함
    - 현재 경로에 있는 파일 및 디렉토리를 파일 수정시간으로 정렬하고 파일을  ‘,’로 구분하며 폴더는 ‘/’로 구분하는 방법
        
        ```bash
        ls -tmp
        ```
        
    
6. **Exercise 05**

- **git log 명령어를 이용하여 커밋 log 확인**
    - -n : n개만큼의 커밋 로그 확인 가능
    - —pretty =”{foramt}” : 특정 format을 지정하여 출력
        
        —# 포멧 종류
        
        - %H : 커밋 ID만을 보여줌
        - %h : 축약된 형태의 커밋 ID만을 보여줌
        - %an : 저자 이메일
        - %cd : 커밋 날짜

```bash
git log -5 --pretty ="%H"
//# 최근 5개의 커밋 ID만을 보여줌
```

7. **Exercise 06**

- **git ls files 명령어를 이용하여 현재 작업공간에 있는 파일들 확인**
    - —others 옵션 : Staging에 올라가지 않은 파일도 확인.
    - —ignore 옵션 : git ignore에 올라간 목록을 확인, 단독으로 사용이 불가능
        - —exclude-standard 옵션을 사용 (git ignore파일의 규칙을 따르며, 표준 git ignore를 추가한다.)

```bash
git ls files --others --ignore --exclude-standard
```

8. **Exercise 07**

- **두 파일간의 차이점과 수정내용을 패치 적용**
    - 문장이 들어 있는 a파일과 수정 사항이 들어있는 .diff파일을 patch 명령어를 사용하여 그 결과를 b 파일에 저장

```bash
patch a sw.diff -o b
```

1. **Exercise 08**

- **find 명령어는 특정 타입의 데이터들을 찾아주는 명령어**
    - type -f : 파일타입만을 찾음
    - -name “원하는패턴” : 원하는 패턴의 이름을 찾아줌 연
        
        ```bash
        \( -name "#*#" -or -name "*~"\)
        #-- 연속적으로 사용시 괄호 안에 넣어서 -or 옵션을 주면 된다.
        #-- 리눅스에서 괄호 사용시 탈출문자 '\'를 사용하여 구분해야 함
        ```
        
    - print : 찾은 파일들을 출력
    - delete : 찾은 파일들을 삭제
    
    ```bash
    find -type f \( -name "#*#" -or -name "*~"\) -print -delete
    ```
    
9. **Exercise 09**

- **file 명령어는 지정된 파일의 타입을 확인할 수 있다.**
    - -m : 지정된 magic 파일을 이용하여 타입을 확인
    
    —# magic 파일 구조 : [바이트수][자료형][찾을문자열]반환타입형식
    
    ```bash
    41 string 42 42 file
    ```
    
    ```bash
    file -m "매직파일" "찾고자하는유형의 파일"
    ```
    

### C Piscine Shell 01

1. **Exercise 01**

- **print_groups : 소속된 그룹의 목록을 표시하는 id 명령어를 이용하면 사용자의 user,group정보를 확인 가능**
    - -G : 모든 그룹 ID들을 출력 가능 → 사용자 번호로 출력이 된다.
    - -n : 사용자 번호 대신 이름으로 출력
    
    —# export를 이용하여 환경변수 설정이 간능하다 
    
    ```bash
    export FT_USER=Hello
    env #-- 등록된 환경변수 정보 확인 가능
    ```
    
    출력된 ID값들을 조건에 맞게 전처리 필요 
    
    —# tr 명령어는 지정한 문자를 변환하거나 삭제하는 명령어
    
    - tr “” “,”  :  공백을 ‘,’로 치환  (tr “바꾸려는 문자”, “바꾸고 싶은 문자”)
    - tr -d ‘\n’ : -d 옵션은 해당 패턴 문자를 삭제한다는 의미 따라서 개행삭제
    
    ```bash
    id -G -n | tr "" "," | tr -d '\n'
    ```
    
2. **Exercise 02**

- **현재 폴더와 그 하위 폴더에 파일 이름이 ‘.sh’ 로 끝나는 모든 파일을 Search 후 파일 이름만 추출**
    - find 명령어를 통해 확장자가 sh인 파일을 찾고 그 찾은 파일을 받아 basename 명령어 실행하며 {}안에 데이터가 전달된다.
    
    —# basename : 해당 파일의 경로는 제외하고 오직 파일의 이름만을 가져옴
    
    ```bash
    find . -type -f -name '*.sh' -exec basename {} \;
    ```
    
    —# cut 명령어를 이용하여 원하는 데이터 전처리 가능 
    
    - -d : 원하는 패턴에 맞게 데이터 분할이 가능하며 -f 옵션으로 원하는 필드 추출 가능
    
    ```bash
    cit -d '.' -f 1
    #-- 마침표로 필드를 구분하며 그 중 1번째 필드를 가져오며 필드 번호의 시작은 0이 아닌 1
    ```
    
3. **Exercise 03**

- **현재 폴더와 그 하위 폴더에 파일 및 폴더의 개수를 확인**
    - find 명령어를 이용 하여 현재 모든 파일 및 폴더를 추출
    
    —# wc 명령어는 word count의 약자로 파일안에 정보뿐 아니라 파일 수 계산에서도 사용 가능
    
    - - l : 현재 word의 행의 개수를 알려준다. 파일 정보들의 행의 개수이기 때문에 결국 파일의 개수라는 의미
    - 위 명령어를 통해 나온 결과값의 앞의 공백을 모두 제거 → sed ‘s/ //g’
    
    —# sed 
    
    ```bash
    find . -type -f | wc -l | sed 's/ //g'
    ```
    
4. **Exercise 04**

- **컴퓨터의 MAC 주소 확인**
    
    —# MAC주소란 : 하드웨어 주소라고도 하며 IP와 달리 고정된 주소이다.
    
    - ip 주소 : 도로명, 주소, 이름 등 언제든지 변경이 가능하다.
    - MAC 주소 : 주민번호와 같이 한 번 생성되면 변경이 불가능한 고정된 값이며 하드웨어 주소라고도 한다.
        - MAC주소 ⇒  ehter
    - ifconfig : 컴퓨터에  있는 인터넷(네트워크) 관련된 정보 확인 가능
    - grep -w “text” : 원하는 text만 추출하며 -w 옵션이 있으면 정확히 일치해야만 추출
    - cut -d “ “ -f 2 : 추출된 정보들을 스페이스를 기준으로 필드를 나누고 그 중 2번째 필드 추출
    
    ```bash
    ifconfig | grep -w "ether" | cut -d " " -f 2
    ```
    
5. **Exercise 04**

- **컴퓨터의 MAC 주소 확인**
    
    —# MAC주소란 : 하드웨어 주소라고도 하며 IP와 달리 고정된 주소이다.
    
    - ip 주소 : 도로명, 주소, 이름 등 언제든지 변경이 가능하다.
    - MAC 주소 : 주민번호와 같이 한 번 생성되면 변경이 불가능한 고정된 값이며 하드웨어 주소라고도 한다.
        - MAC주소 ⇒  ehter
    - ifconfig : 컴퓨터에  있는 인터넷(네트워크) 관련된 정보 확인 가능
    - grep -w “text” : 원하는 text만 추출하며 -w 옵션이 있으면 정확히 일치해야만 추출
    - cut -d “ “ -f 2 : 추출된 정보들을 스페이스를 기준으로 필드를 나누고 그 중 2번째 필드 추출
    
    ```bash
    ifconfig | grep -w "ether" | cut -d " " -f 2
    ```
    
6. **Exercise 05**

- **파일 생성 규칙을 무시한 채 파일을 만드는 과제 (파일 생성 규칙 → 특수문자 사용금지)**
- 42이라는 문자열만 포함하는 크기가 2바이트인 파일 생생
    
    —# 리눅스에서 특수문자는 각각 다른  특수한 기능들이 있다 여기서 단순히 문자라는 걸 알려주려면 특수문자앞에 ‘\’ (백슬래쉬)를 넣어 일반 문자라는 표시를 해줘야 한다.
    
    - 이스케이프 문자를 사용하여 각각의 특수문자를 단순한 문자열로 인식
    - echo -n “원하는데이터” > “파일명” :  원하는데이터로 파일을 만드는데 개행은 제거
    
    ```bash
    echo -n 42 > \"\\\?\$\*\'\MaRViN\'\*\$\?\\\"
    ```
    
7. **Exercise 06**

- **ls -l 명령어의 첫 번째 행부터 시작하여 한 줄 걸러 보여주는 명령어 작성**
    
    —# awk : 데이터를 조작하고 리포트를 생성하기 위한 언어로 다양한 데이터 전처리가 가능하게 도와줌
    
    —# NR : The number of record so far (현재 라인 번호) → cat -n 으로 라인번호 확인 가능
    
    ```bash
    awk 'NR%2!=0' 
    #-- 현재 라인넘버를 몫이 0이 아니면 즉 혹수의 경우는 출력
    ```
    
8. **Exercise 07**

- **cat/etc/passwd 명령어의 출력 결과를 가공하여 출력**
    
    **—# 요구조건** 
    
    1. 주석 삭제
    2. 2번째 행부터 짝수 행만 출력
    3. 각 로그인 정보를 반전하고 알파벳 역순으로 정렬
    4. 환경변수1, 환경변수2를 포함한 그 사이값
    5. 각 로그인은 ‘,’로 구분하며 마지막은 ‘.’로 치환
    - 주석 삭제 ⇒ grep -v ‘^#’  : -v 옵션은 해당 패턴을 제외함
        - 주석은 #으로 시작
    - 2번째 행부터 짝수 ⇒ ex06 과 같음 awk ‘NR%2==0 을 사용
    - 각 로그인 문자열을 반전, 알파벳 역순으로 정렬
        - cut -d ‘:’ -f 1 :  “:” 를 기준으로 필드를 나누며 그 중 1번 필드를 가져옴
        - rev : 문자열 반전
        - sort -r : 알파벳 역순으로 정렬
    - 환경변수1, 환경변수2를 포함한 그 사이값
        
        —# sed -n 시작점 종료지점p: 원하는 시작 인덱스부터 종료 인덱스까지 추출 후 출력 
        
        ```bash
        sed -n ${변수명}, ${변수명}p
        ```
        
    - 각 로그인은 ‘,’로 구분하며 마지막은 ‘.’로 치환
        - 각 로그인은 ‘,’로 구분 → tr ‘\n’ ‘,’ 명령어로 개행을 ‘,’로 구분
        - sed ‘s/,/, /g’ → 기존 변경했던 ‘,’를 ‘, ‘로 치환 (공백 추가)
    - 마지막 ‘,’대신 ‘.’ 사용 → sed ‘s/..$/./g’ 이용하여 마지막 텍스트 ;.;로 치환
    
    —# $은 맨 마지막이라는 의미이며 ..은 맨 마지막부터 2칸 변경 하겠다는 뜻
    
    ```bash
    cat /etc/passwd | grep -v '^#' | awk 'NR%2==0' | cut -d ':' -f 1 | rev | sort -r | sed -n ${FT_LINE1},${FT_LINE2}p | tr '\n' ',' | sed 's/,/, /g' | sed 's/..$/./g' | tr -d "\n"
    ```
    

9. **Exercise 08**

- 주어진 조건에 맞는 진수 변환 후 그 값을 연산하고 또 다른 조건을 밑으로 하는 문자로 출**력**
    
    **—# 요구조건** 
    
    1. “’\"?! “을 밑으로 하는 5진수 NUMBER 1
    2. “mrdoc” 을 밑으로 하는 5진수 NUMBER 2
    3. 위 두 변수를 더하기 연산 
    4. 결과값을 “gtaio luSnemf”을 밑으로 하는 13진수 결과로 출력
    5. 
    - 주석 삭제 ⇒ grep -v ‘^#’  : -v 옵션은 해당 패턴을 제외함
        - 주석은 #으로 시작
    - 2번째 행부터 짝수 ⇒ ex06 과 같음 awk ‘NR%2==0 을 사용
    - 각 로그인 문자열을 반전, 알파벳 역순으로 정렬
        - cut -d ‘:’ -f 1 :  “:” 를 기준으로 필드를 나누며 그 중 1번 필드를 가져옴
        - rev : 문자열 반전
        - sort -r : 알파벳 역순으로 정렬
    - 환경변수1, 환경변수2를 포함한 그 사이값
        
        —# sed -n 시작점 종료지점p: 원하는 시작 인덱스부터 종료 인덱스까지 추출 후 출력 
        
        ```bash
        sed -n ${변수명}, ${변수명}p
        ```
        
    - 각 로그인은 ‘,’로 구분하며 마지막은 ‘.’로 치환
        - 각 로그인은 ‘,’로 구분 → tr ‘\n’ ‘,’ 명령어로 개행을 ‘,’로 구분
        - sed ‘s/,/, /g’ → 기존 변경했던 ‘,’를 ‘, ‘로 치환 (공백 추가)
    - 마지막 ‘,’대신 ‘.’ 사용 → sed ‘s/..$/./g’ 이용하여 마지막 텍스트 ;.;로 치환
    
    —# $은 맨 마지막이라는 의미이며 ..은 맨 마지막부터 2칸 변경 하겠다는 뜻
    
    ```bash
    cat /etc/passwd | grep -v '^#' | awk 'NR%2==0' | cut -d ':' -f 1 | rev | sort -r | sed -n ${FT_LINE1},${FT_LINE2}p | tr '\n' ',' | sed 's/,/, /g' | sed 's/..$/./g' | tr -d "\n"
    ```

## 2. C언어

### C Piscine C 00

1. **Exercise 00**

- **함수에 인자로 전달받은 값을 write를 이용하여 출력**
    - write : 문자열 단위로 파일에 입력하는 함수
        - 1번째 인자 : 0 → 표준 입력, 1→ 표준 출력, 2→ 표준 에러
        - 2번째 인자 : 문자열 주소
        - 3번째 인자 : 몇 바이트 즉 몇 글자 출력 할지
    
    ```c
    #include <unistd.h>
    
    void    ft_putchar(char c)
     18 {
     19     write(1, &c, 1);
     20 }
    ```
    
    2번째 인자로 받은 값 1글자를 표준 출력(화면에 보이게) 
    
1. **Exercise 01**

- **알파벳 소문자를 오름차순으로 정렬하여 출력**
    - write : 문자열 단위로 파일에 입력하는 함수
        - 1번째 인자 : 0 → 표준 입력, 1→ 표준 출력, 2→ 표준 에러
        - 2번째 인자 : 문자열 주소
        - 3번째 인자 : 몇 바이트 즉 몇 글자 출력 할지
    
    ```c
    #include <unistd.h>
     14 
     15 void    ft_print_alphabet(void);
     16 
     17 void    ft_print_alphabet(void)
     18 {
     19     write(1, "abcdefghijklnmopqrstuvwxyz", 26);
     20 }
    ```
    
    변수를 사용하지 않고 문자열을 바로 입력해도 상관없다.
    

1. **Exercise 02**

- **알파벳 소문자를 내림차순로 정렬하여 출력**
    - write : 문자열 단위로 파일에 입력하는 함수
        - 1번째 인자 : 0 → 표준 입력, 1→ 표준 출력, 2→ 표준 에러
        - 2번째 인자 : 문자열 주소
        - 3번째 인자 : 몇 바이트 즉 몇 글자 출력 할지
    
    ```c
    #include <unistd.h>
     14 
     15 void    ft_print_reverse_alphabet(void);
     16 
     17 void    ft_print_reverse_alphabet(void)
     18 {
     19     write(1, "zyxwvutsrqpomnlkjihgfedcba", 26);
     20 }
    ```
    
    변수를 사용하지 않고 문자열을 바로 입력해도 상관없다.
    
1. **Exercise 03**

- **모든 숫자를 오름차순으로 정렬하여 출력**
    - write : 문자열 단위로 파일에 입력하는 함수
        - 1번째 인자 : 0 → 표준 입력, 1→ 표준 출력, 2→ 표준 에러
        - 2번째 인자 : 문자열 주소
        - 3번째 인자 : 몇 바이트 즉 몇 글자 출력 할지
    
    ```c
    #include <unistd.h>
     14 
     15 void    ft_print_number(void);
     16 
     17 void    ft_print_number(void)
     18 {
     19     write(1, "0123456789", 10);
     20 }
    ```
    
    변수를 사용하지 않고 문자열을 바로 입력해도 상관없다.
    
1. **Exercise 04**

- **입력받은 숫자가 음수인지 양수인지 구분하고 상황에 맞게 출력(조건문 필요)**
    - write : 문자열 단위로 파일에 입력하는 함수
        - 1번째 인자 : 0 → 표준 입력, 1→ 표준 출력, 2→ 표준 에러
        - 2번째 인자 : 문자열 주소
        - 3번째 인자 : 몇 바이트 즉 몇 글자 출력 할지
    
    ```c
    #include <unistd.h>
     14 
     15 void    ft_is_negative(int n);
     16 
     17 void    ft_is_negative(int n)
     18 {
     19     if (n < 0)
     20     {
     21         write(1, 'N', 1);
     22     }
     23     else
     24     {
     25         write(1, 'P', 1);
     26     }
     27 }
    ```
    
1. **Exercise 05**

- **세자릿수의 모두 다른 조합을 오름차순으로 출력**
    - write : 문자열 단위로 파일에 입력하는 함수
        - 1번째 인자 : 0 → 표준 입력, 1→ 표준 출력, 2→ 표준 에러
        - 2번째 인자 : 문자열 주소
        - 3번째 인자 : 몇 바이트 즉 몇 글자 출력 할지
    
    ```c
    #include <unistd.h>
    
    void	ft_print_comb(void);
    /*
    int main(){
    
    	ft_print_comb();
    	return 0;
    }
    */
    
    void	ft_print_comb(void)
    {
    	char	i;
    	char	j;
    	char	k;
    
    	i = '0' - 1;
    	while (i++ < '7')
    	{
    		j = i;
    		while (j++ < '8')
    		{
    			k = j;
    			while (k++ < '9')
    			{
    				write(1, &i, 1);
    				write(1, &j, 1);
    				write(1, &k, 1);
    				if (!(i == '7' && j == '8' && k == '9'))
    					write(1, ", ", 2);
    			}
    		}
    	}
    }
    ```
    
    - 반복문을 사용하여 해결 n값이 정해져 있으므로 10 - n(3) 부터 시작하면 해결이 가능
    - 코드를 단축시키기 위해 조건문 안에 연산자를 사용
        - 이 때 i = -1 부터 시작해야 제대로 출력이 된다.
    

```bash
#include <unistd.h>

void ft_print_combn(int n);
int IsPossible(int pre, int curr);
void Backtracking(char arr[], int pre, int idx, int n, int check);
void PrintNumber(char arr[], int idx, int check);

int main(){
    ft_print_combn(2);
    return 0;
}

int IsPossible(int pre, int curr){
    if(pre<curr )
        return 1;
    else
        return 0;
}
void PrintNumber(char arr[], int idx, int check){
    char str[2];
    write(1, arr, idx);
    if(!check){
        str[0] = ',';
        str[1] = ' ';
        write(1, str, 2);
    } 
        return;
    
}
void Backtracking(char arr[], int pre, int idx,  int n, int check){
    if(n==0){
        PrintNumber(arr, idx, check);
    }
    for(int i=0; i<10; i++){ // 0또는 pre부터 시작
        if(IsPossible(pre,i)){
            char ch = '0'+i;
            arr[idx] = ch;
            Backtracking(arr, i, idx+1,n-1,check);
        }
    }
}

void ft_print_combn(int n){
    if(n>10 || n<0)
        return ; // 예외처리
    char arr[10]; 
    int check = 0; // 마지막인지 확인하기 위해 
    for(int i=0; i<10; i++){
        char start = '0'+i; // 최초 값 삽입
        int idx = 0;
        arr[idx] = start;
        if(i==(10-n))check = 1;  // 최대 크기 - n => 마지막
        Backtracking(arr, i,idx+1, n-1,check); //  시작점 부터, 노드는 1칸 줄어듬
        if(check ==1) return;
    }
}
```