# nvm node 버전 관리

https://github.com/nvm-sh/nvm#long-term-support
https://tutorialpost.apptilus.com/posts/nodejs/nvm-for-node-version-manager/

Node.js의 패키지 생태계인 npm(Node Packaged Manager)은 세계에서 가장 큰 오픈 소스 라이브러리 생태계이기도 합니다.
Node.js를 설치하면 npm이 같이 설치되어 사용할 수 있습니다.

1. 제일 먼저 협업시 해야할 작업은 현재 프로젝트의 node버전을 확인합니다.

`nvm(Node Version Manager)` : node 버전을 관리하는 매니저

2. nvm 설치

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
```

1. 맥에서는 Xcode command line tools이 미리 설치되어 있어야 합니다. 만약 맥에 Xcode가 설치되어 있다면 이미 설치되어 있을겁니다.

```
xcode-select --install # Xcode Command line tools 설치
```

1. nvm 설치가 잘 되어 있는 확인

```
command -v nvm
```

3. nvm이 이미 깔려 있다면 터미널에서 node 버전을 확인합니다.
   현재 설치 되어있는 node가 목록 출력

```
nvm ls
```

4. node가 낮아서 업데이트를 해야된다면 아래와 같은 명령어 작성
   --lts 옵션을 사용해서, NVM이 인식하고 있는 최신 LTS 버전을 설치

설치후 node 버전은 업데이트가 되었을 것이다. 하지만 **컴퓨터를 껐다가키면 다시 원점이 될것** 이유는 **default가 가르치는것이 이전 하위버전이기 떄문!!!**

```
nvm install --lts
```

1. node 버전 확인

```
node -v
```

1. 모든 node.js의 버전을 조회 할수 있습니다.

```
nvm ls-remote
```

5. node확인하고 default를 lis 최신 버전으로 변경

```
nvm alias default --lts/*
```

6. global 확인 ~~~ 왜냐면 하위버전에서 global로 설치한것들이 있나 해서

```
npm list -g --depth=0
npm list -g --depth=1
```

7. 현재 사용중인 버전 확인

```
nvm current
```
