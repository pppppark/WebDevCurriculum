# Quest 00. 형상관리 시스템

## Introduction

- git은 2021년 현재 개발 생태계에서 가장 각광받고 있는 버전 관리 시스템입니다. 이번 퀘스트를 통해 git의 기초적인 사용법을 알아볼 예정입니다.

## Topics

- git
  - `git clone`, `git add`, `git commit`, `git push`, `git pull`, `git branch`, `git stash` 명령
  - `.git` 폴더
- GitHub

## Resources

- [Resources to learn Git](https://try.github.io)
- [Learn Git Branching](https://learngitbranching.js.org/?locale=ko)
- [Inside Git: .Git directory](https://githowto.com/git_internals_git_directory)

## Checklist

- 형상관리 시스템은 왜 나오게 되었을까요?
  형상관리 시스템은 소프트웨어가 수정되고 업데이트를 함에 있어 효율적이고 체계적으로 관리하기 위함이다.

- git은 어떤 형상관리 시스템이고 어떤 특징을 가지고 있을까요? 분산형 형상관리 시스템이란 무엇일까요?
  git은 버전관리가 가능한 형상관리 시스템
  분산형 형상관리는 중앙집중형 시스템과는 다르게 클라이언트의 마지막 snapshot을 받아오지 않고 저장소를 전부 다 복제한다. 서버에 문제가 생기게 될 경우 접근한 클라이언트의 복제물로 서버를 복구할 수 있다. 모든 클라이언트가 서버에 접속하지 않아도 혼자서 commit과 작업이 가능한게 특징이다.

  - git은 어떻게 개발되게 되었을까요? git이 분산형 시스템을 채택한 이유는 무엇일까요?
    git은 기존의 형상관리 시스템이자 버전 관리 도구였던 CVS와 Subversion에서 업그레이드되어 시스템을 구축하고 네트워크 문제와 용량의 문제 등 여러 결함에서 고쳐진 툴이다. git이 분산형 시스템을 채택한 이유는 위에 언급한대로 제약없이 혼자서 언제든 어디서든 commit이 가능하고 작업할 수 있기 때문이다. 로컬에 서버복사본을 구축하여 메인 서버나 프록시 서버를 굳이 구축하지 않아도 네트워크나 용량의 문제도 해결이 가능하여 기존 시스템의 문제를 해결할 수 있기 때문이다.

- git과 GitHub은 어떻게 다를까요?
  git과 github의 차이점은 간단하다. git은 로컬서버를 통해 repository를 관리함이지만 github는 git을 이용해 로컬서버에 있던 내용을 업로드 함으로써 개발자간의 협업이나 소스코드 등 작업물들을 공유할 수 있다.

- git의 clone/add/commit/push/pull/branch/stash 명령은 무엇이며 어떨 때 이용하나요? 그리고 어떻게 사용하나요?

  1. git clone https://github.com/(사용자이름)/(repository).git 을 통해 repository를 복제하고
  2. git add 명령어를 통해 commit을 하기 전에 복제한 repository 공간에 파일을 추가한다. 수정사항을 업데이트할 때 사용한다.
  3. git commit -m "(text)" 명령어를 통해 add한 파일에 대한 설명이나 업데이트한 수정사항을 적고 기록을 남긴다.
  4. git push (repository or branch) 명령어로 로컬에 저장된 원격저장소에 업로드한다.
  5. git pull 명령어는 repository의 변경사항들을 로컬로 가져와 기존의 repository와 합친다.
  6. git branch 명령어는 -r, (새로만든branch)(원격branch)로 -r 옵션은 원격에서 로컬로 전역이 아닌 지역 branch를 생성한다. (새로만든branch)(원격branch) 옵션은 원격에서 지역 branch를 생성한다.
  7. git stash (sava) 명령어는 스택에 임시저장하여 다른 작업 공간(new branch)로 이동가능하다. list옵션을 통해 기존의 stash 명령어로 저장한 목록을 불러올 수 있다. apply 옵션을 사용하면 전에 작업하던 임시저장물을 가져와 다시 작업할 수 있다.

- git의 Object, Commit, Head, Branch, Tag는 어떤 개념일까요? git 시스템은 프로젝트의 히스토리를 어떻게 저장할까요?

  1. git object는 파일내용(blob), Dir과 blob의 정보들이 담겨져 있고, commit이 존재한다. object는 git에서 파일을 add하고 commit했을 때 내부에서 만들어지는 객체이다. 하여 git은 blob, tree, commit, tag의 4가지 객체로 이루어져있다. 그리고 SHA-1 해시값을 사용해 고유한 식별자를 만든다.
  2. commit은 git에서 가장 중요한 개념으로 소스코드의 작업 내용을 저장하고 변경 내용을 했다는 메시지와 함께 SHA1으로 고유한 식별자를 생성한다. 그로 인해 해시의 특징으로 이력을 추적할 수 있다.
  3. Headsms git에서 작업중인 commit을 가리키는 포인터로 현재 작업중인 commit을 추적 가능하고 변경 내용을 업데이트한다.
  4. Branch는 git을 통해 협업하는 중에 가장 중요한 요소이다. 소스코드를 작업할 때 변경내용을 나누어 작업할 수 있다. 협업중인 다른 개발자들의 영향을 받지 않고 독립적으로 작업이 가능하다.
  5. Tag는 gitdptj commit에 부여하는 이름이다. tag는 일반적으로 프로젝트에서 중요한 이벤트를 나타내는 commit에 부여됨으로 tag를 이용해 특정 commit을 찾아내 추적할 수 있다.

- 리모트 git 저장소에 원하지 않는 파일이 올라갔을 때 이를 되돌리려면 어떻게 해야 할까요?
  push를 하기 전에 git reset (commit tag) 명령어를 이용해 이전으로 돌아갈 수 있다. ~n 옵션을 이용하면 n만큼 이동하여 그 전 commit으로 돌아간다.

## Quest

- GitHub에 가입한 뒤, [이 커리큘럼의 GitHub 저장소](https://github.com/KnowRe-Dev/WebDevCurriculum)의 우상단의 Fork 버튼을 눌러 자신의 저장소에 복사해 둡니다.
- Windows의 경우 같이 설치된 git shell을, MacOSX의 경우 터미널을 실행시켜 커맨드라인에 들어간 뒤, 명령어를 이용하여 복사한 저장소를 clone합니다.
  - 앞으로의 git 작업은 되도록 커맨드라인을 통해 하는 것을 권장합니다.
- 이 문서가 있는 폴더 바로 밑에 있는 sandbox 폴더에 파일을 추가한 후 커밋해 보기도 하고, 파일을 삭제해 보기도 하고, 수정해 보기도 하면서 각각의 단계에서 커밋했을 때 어떤 것들이 저장되는지를 확인합니다.
- `clone`/`add`/`commit`/`push`/`pull`/`branch`/`stash` 명령을 충분히 익혔다고 생각되면, 자신의 저장소에 이력을 push합니다.

## Advanced

- Mercurial은 어떤 형상관리 시스템일까요? 어떤 장점이 있을까요?
- 실리콘밸리의 테크 대기업들은 어떤 형상관리 시스템을 쓰고 있을까요?
