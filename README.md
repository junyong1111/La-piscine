# 42Seoul

## 00 쉘 기본 명령어 정리

### C Piscine Shell 00

1. **Exercise 00**

- **cat명령어를 사용하여 지정된 파일에 내용을 확인**
    - e 옵션을 주면 개행 여부도 확인이 가능하다
1. **Exercise 01**

    - **ls명령어로 현재 경로에 있는 폴더 및 파일을 확인하고 정보를 수정**
        - l 옵션 : 퍼미션(권한)정보, 소유권, 소유그룹, 파일(폴더)용량, 생성날짜, 파일(폴더)이름
        
        --# 파일의 경우 퍼미션(권한)정보 앞에 '-'로 표시가 되며 폴더의 경우 'd'로 표시가 된다.
        --# chmod 명령어로 퍼미션 정보를 수정이 가능하다 4:read, 2:write, 1:execute
        
2. **Exercise 02**

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
        
3. **Exercise 03**

- **ssh-keygen 프로그램을 사용하여 공개키와 개인키 생성**
    - Key 생성 방법
        
        ```bash
        cd ~/.ssh #-- ssh 정보가 저장되어 있는 디렉토리로 이동
        ssh-keygen #-- 기본적으로 내장된 keygen 프로그램을 이용하여 개인키와 공용키 발급
        ls #-- 해당 명령어로 .pub 공용키 내용 확인
        ```
        
    - 공개키는 git 저장소에 등록하고 개인키는 자신이 보관 한다.
    - 개인키를 통해 ssh 접속 후 개인키와 매칭되는 공개키를 이용하여 저장소에 접근이 가능.
