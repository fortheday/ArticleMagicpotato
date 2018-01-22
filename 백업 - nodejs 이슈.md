# node.js 개인이슈 정리
* 2016-11-02. magicpotato.

# 실행
  * node.exe, npm.exe를 방화벽 등록해줘야 한다.
  * npm install 만으로 로컬설치하면 현재경로밑에 패키지를 설치하게 된다.
  
# 디펜던시 설치
  * myNodeJsApp/packages.json에 디펜던시 정보가 들어있다.
  * myNodeJsApp 폴더에서 "npm install"만 해주면 알아서 설치해준다.
  * 윈도우 환경은 귀찮으니 --global을 붙여주자.

# 토큰값 변경문제
  * 깃헙에 토큰을 올리면 안된다. 로컬에서 읽게 해야함. 토큰 커밋금지.
  
  EOF
