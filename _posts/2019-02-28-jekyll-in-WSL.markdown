---
layout: post
comments: true
title:  "윈도우에서 WSL에 지킬을 설치해서 블로깅을 해보자"
date:   2019-02-28
categories: develop
---
- 먼저 Jekyll 은 ruby 스크립트로 만들어져 있다.
- https://jekyllrb-ko.github.io/docs/windows/ 에 따르면
윈도우즈가 공식적으로 지원되는 플랫폼은 아니지만 Jekyll 을 실행할 수 있다고 한다.

-- 글을 따라 rubyinstaller를 설치하러 간다.
https://rubyinstaller.org/downloads/
어떤 버젼을 써야할 지 모르겠다면 Ruby+Devkit 2.5.X (x64)를 추천한다고 한다
-- Jekyll github.io 에서도 RubyInstaller-2.4 또는 그 이상의 버전을 다룬다고 하니 추천을 따라 받아서 설치하기로 한다.

- 설치를 진행하고 있는데
'윈도우즈 10 에서 Bash 를 통한 설치' 가 눈에 띄었다
설치를 해보기로 한다
- 윈도우에는 Ruby+Devkit 이 설치되고 있는 동안에 
https://code.apptilus.com/posts/tools/windows-subsystem-linux
https://webnautes.tistory.com/1170 를 살펴본다

- 에러등장
http://blog.naver.com/PostView.nhn?blogId=pubcrawl_&logNo=221315457132
해결

- $ sudo apt-get update -y && sudo apt-get upgrade -y
로 업데이트 및 업그레이드를 진행해준다.
이제 루비를 받을 준비가 끝!

- 2019-02-28 까지의 상황을 이어 2019-03-01 의 상황

- 켜자마자 에러가 반긴다
0x800703fa
https://memory.today/dev/24 -> 
제어판/모든제어판/전원옵션/시스템설정/빠른 시작 켜기 체크 해제

이미 해제되어 있으므로 트러블슈팅 실패

- 아 씨... 하고 다시 켜봤더니 부팅이 되었다?
쓰지마??

- 경고들
WSL을 이용해서 윈도우 파일을 마운트하고 조작할 수 있습니다. 하지만 반대로 안정성의 문제로 윈도우 탐색기 등 윈도우 환경에서 WSL 내부 파일을 조작하는 것은 금지됩니다.
윈도우즈에서 리눅스 내부의 파일을 생성/변경하면 리눅스 환경이 손상되어 배포판을 제거하고 다시 설치해야 할 수 있습니다.
-> 윈도우에서 리눅스 접근하지 말아라
리눅스 명령어 기반 도구(Ruby, Rails, Git, apt-get, vim 등)는 WSL에 설치하고, 텍스트 에디터 등의 GUI 도구는 윈도우에 설치된 것을 사용하는 방식으로 개발 방식을 구성할 수 있습니다.
이때 프로젝트 폴더 등은 윈도우에 만들고, WSL에서 마운트하여 접근할 수 있습니다.
심볼릭 링크를 사용하면 WSL에서 편하게 윈도우 폴더에 접근할 수 있습니다.
(https://code.apptilus.com/posts/tools/windows-subsystem-linux)


WSL 내에서 윈도우 파일시스템에 접근하기 위해서는 다음과 같이 필요한 폴더를 마운트 합니다.

# D드라이브 하위의 workspace 폴더에 접근하기
cd /mnt/d/workspace
매번 윈도우 내부의 작업 디렉토리로 이동하기 위해 위와 같이 명령어를 입력하는 것은 귀찮습니다. 이때, 심볼릭 링크를 이용하면 마치 WSL 내부의 디렉토리를 이용하듯 손쉽게 윈도우 폴더에 접근할 수 있게 됩니다.

# symbolic link 사용
ln -s "/mnt/d/workspace" /home/<my-wsl-username>/workspace

심볼릭 링크를 사용해서 워크스페이스를 편하게 접근케 함

		jekyll serve
		# => 개발서버가 실행됩니다. http://localhost:4000/
		# 자동 재생성: 활성화. 비활성화하려면 `--no-watch` 를 사용하세요.

		jekyll serve --livereload
		# 변경사항이 발생했을 때 LiveReload 기능이 브라우저를 새로고침합니다.

		jekyll serve --incremental
		# 재생성 소요시간을 줄이기 위해 증분 재생성 기능으로 부분 빌드를 합니다.

		jekyll serve --detach
		# => `jekyll serve` 와 동일하지만 현재 터미널에 독립적으로 실행됩니다.
		#    서버를 종료하려면, `kill -9 1234` 를 실행하세요. "1234" 는 PID 입니다.
		#    PID 를 모르겠다면, `ps aux | grep jekyll` 를 실행하고 해당 인스턴스를 종료하세요.