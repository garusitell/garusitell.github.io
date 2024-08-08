## QMk와 VIA
### QMK란?
[참조](https://docs.qmk.fm/)  

QMK(Quantun Mechanical Keyboard)는 컴퓨터 입력 장치 개발을 중심으로 하는 오픈 소스 커뮤니티를 총칭한다.

이후는 QMK를 펌웨어 하는 작업을 기술한다.

-----
### QMK 펌웨어 
1. https://msys.qmk.fm/ (QMK 설치)

2. Latest Version을 들어간 후 exe 설치. 중간에 나오는 것은 세게 다 체크 하는 것이 좋다. 

3. 시작 버튼이나 찾기 혹은 윈도우를 눌러 'QMK MSYS'를 누른다.

4. `qmk setup`을 입력한다. 그 뒤   
>`Could not find qmk_firmware!
Would you like to clone qmk/qmk_firmware to C:/Users/gameins/qmk_firmware? [y/n]`  

이런 문장이 나온다면 `Y`를 누른다

5. 완료가 되었다면 키보드를 불러와 보자

6. `qmk new-keyboad`

7. 그러면 Default Layout이 나올텐데. 키보드 배열이다. 58번이텐키리스 ansi이다.   
`Please enter your choice : [65] 이렇게 적혀있을텐데 58`  이라고 적는다.

8. MCU인데. 내가 생각하기론 여기서 연결하는 행과 열이 연결하는게 지정되어 있다고 결론 지었는데 이건 회로도를 판단하고 행각해봐야할 문제인것 같다. 일단 내가 검색한 사람이 제일 잘 알고있다는 `RP2040`을 선택해본다.

9. 이렇게 되면. 경로가 나오게 되는데 `C:/Users/gaeins/qmk_firmware/keyboards/test/에 컴파일 되었다고 나와있다.

https://gall.dcinside.com/mgallery/board/view/?id=mechanicalkeyboard&no=2020721&exception_mode=recommend&search_head=10&page=1

-> qmk 수정하는 방법 , via 올리는 방법

https://gall.dcinside.com/mgallery/board/view/?id=mechanicalkeyboard&no=1135747

-> vial 올리는 방법

-> 맥북에 블랙필 올리는 방법 올리기 ##