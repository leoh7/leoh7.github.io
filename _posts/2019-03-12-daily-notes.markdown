---
layout: post
title:  "2019-03-12 일지"
date:   2019-03-12
categories: notes
---

### **리액트 진도 재시작**
  - **작업환경 세팅**
	- 노트북을 바꾸면서 node 관련 개발도구를 복구하지 않았단 점을 깨달았다.
	- [x] Node.js / npm, yarn 재설치 (윈도우 & WSL)
    - [x] WSL에 Node.js 설치

		macOS나 Ubuntu에서는 Node.js를 여러 버전으로 설치해 관리해 주는 nvm 도구를 권유한다고 한다.
		추후 Node.js 버전을 업데이트하거나 프로젝트별로 버전이 다른 Node.js를 사용해야 할 때, 이 도구가 가장 용이하기 때문이라 함.
	
			$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
			(터미널 재시작 후) $ nvm --version
			(재시작 후 버전이 나타나지 않을 땐) ~./bashrc 파일에 다음 내용 추가
			export NVM_DIR="$HOME/.nvm"
			[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"

			$ nvm install --lts
 
    - [x] 윈도우에 Node.js 설치
    - [x] WSL 에 yarn 설치

			$ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
			$ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
			$ sudo apt-get update && sudo apt-get install yarn
			$ echo 'export PATH="$(yarn global bin):$PATH"' >> ~/.bashrc

    - [x] 윈도우에 yarn 설치
    - 헛짓거리 (사유: vscode 상의 bash terminal에서 yarn 명령어가 먹히지 않음)

			vscode 상에서 터미널로(bash) node나 yarn 명령어를 쓰려면 bash 상에서 설치를 했어야 했나????? 아니면 ~/.bashrc 에 path를 적어줬어야 했나???
			그랬다! Ubuntu에 설치하듯이 curl 명령어로 설치를 진행하니 C:/Users/사용자명/.nvm 에 설치가 들어왔다!
			
			그러나 nvm 명령어를 인식하지 못하는 것을 보니 ~/.bashrc 파일을 건드려야 하는 것인가 싶어 건드려본다. 현재 윈도우 사용자 폴더엔 git을 쓸 때의 편의성을 위해 GitHub 폴더를 실행 기본폴더로 하려고 인위적인 .bashrc 파일을 생성해놓은 상황.
			~/.bashrc에 설정을 해주었고... 버전이 뜬다! 위에 Ubuntu에서 nvm 인식이 안될 때를 대비한 작업이 여기서 먹힐줄은 몰랐지...
			
			그러나 $ nvm install --lts는 먹히지 않는다.. 후후 python도 찾고 난리가 났네. 
			yarn 도 설치가 안되는건 마찬가지. 삽질은 여기까지 했으면 충분한 것 같으니 본래 목적으로 돌아가기로 하자.

    - Node.js 와 yarn을 설치 한 후, $ yarn start 를 치고 나서야 create-react-app 으로 개발을 진행하면서 생성했던 모듈이 지금은 없는 걸 깨달았다. gitignore에 포함되는 내용들이었기 때문에...
    - 어차피 공부하기 위함이니 갈아 엎고 다시 만들자! [(해당커밋)][갈아엎는커밋]
	- WSL 에 git 설치 및 create-react-app 전역 설치

			$ sudo apt-get install git-all
			$ yarn global add create-react-app
  
  - **create-react-app 사용해서 프로젝트 생성**
    - CRA v2 이전 버전 사용하기
  			
			$ npx create-react-app sample-project --scripts-version=1.1.5

	- CRA를 사용해서 프로젝트 생성
		- 컴포넌트 스타일링 프로젝트 [(styling-react)][styling]
		- 리덕스 실습 프로젝트 [(redux-counter)][redux]

### **jekyll 과 친해지기**
  - vscode extension 중 Markdown Preview Enhanced 가 보여주는 모습과 실제 페이지의 모습이 부분부분 다른 곳이 있어 jekyll 의 livereload 기능을 쓰기로 했다.

		$ jekyll serve --livereload

  - _config.yml 에 YAML 머리말 default 설정 넣어보기 [(참고링크)][머리말참조]
  
  - jekyll 에 disqus 를 붙여보자

### **다음 계획**
  - 만만하게 봤으나 실패한 블로그에 disqus 붙이기... ㅠㅠ 왜 나만 없어 왜 나만 빼고 다 있어 ㅠㅠ
  - 컴포넌트 스타일링, 리덕스 프로젝트 진행하기

### **오늘의 생각들**
- 생활 다잡기
- 조급하지 말고 성실하자. 초조할 때 일수록 노력하자.
- 꾸준히 조금씩이라도 해나가야 하는 중요성을 느낀다.
- 환경 바뀌는 거 참 힘들다...
  - 그래서 WSL 쓰는게 불안불안하다... 아우씨
  - CHEF 배우고 싶다.
  - 이러고 나면 다시 생각나는게 Docker 고 도돌이 도돌이 되는 세팅 욕심..
- '야크 쉐이빙'
- 노트북이 오래되어 키보드가 잘 안먹는게 있다... 
	키보드 마우스 세트를 하나 장만하자.
- 블로그 카테고리 분류를 develop 과 daily notes 두 가지로 나눠야겠다. 그날 그날의 기록과 정리된 안내문의 개념으로 나누고 싶다.




[갈아엎는커밋]: https://github.com/leoh7/study-react/commit/bfc5b3779da97d97d59a7dcc87c280d5292e05c1
[styling]: https://github.com/leoh7/study-react/tree/master/styling-react
[redux]: https://github.com/leoh7/study-react/tree/master/redux-counter
[머리말참조]: https://jekyllrb-ko.github.io/docs/configuration/#front-matter-defaults