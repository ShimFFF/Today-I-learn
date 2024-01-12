# [TIL] 각종 컨벤션 정리

##  😃 잡담
일단, 그동안 TIL을 안 쓴 동안 한 일은..

- 트위터 클론 코딩
  - spring 
  - android
- 시간표 앱
  - android
- 서버 스터디
  - api
  - swagger
  - 커스텀 annotation
  - paging
  - 무중단 ci/cd
  - github action
  - aws elastic beanstalk
- 개인 공부
  - DB
    - transaction
    - hashing
    - indexing
    - xml
  - network
    - socket programing
    - network layer
    - transport layer
    - link layer
- 묘집사 리뉴얼 (플젝)

일단 대충 이정도..

그래서 이제는 새로운 프로젝트를 시작하게 되었는데, 우리는 daily scrum을 진행한다. 간단하게 오늘 한 일을 정리해서 올리는 것인데, 
올리는 김에 다시... TIL도 시작하자! 라는 생각으로 드디어 다시 쓰게 되었다.

오늘은 프로젝트를 진행할 때 필요한 git convention 관련해서 정리 해야겠다..<br>
나중에는 레포 하나 파서 프로젝트 초기 세팅 템플릿 같이 만들어 놔야겠다..!

## 📄 배운 내용

## commmit message

`깃모지, 태그 : 제목의 형태`

- `:sparkles: Feat : 새로운 기능 추가`
- `:bug: Fix : 버그 수정`
- `:memo: Docs : 문서 수정`
- `:white_check_mark: Test : 테스트 코드 추가`
- `:recycle: Refactor : 코드 리팩토링`
- `:art: Style : 코드 의미에 영향을 주지 않는 변경사항(코드 포맷팅, 세미콜론 누락 등..)`
- `:wrench: Chore : 빌드 부분 혹은 패키지 매니저 수정사항`
- `:truck: Rename : 파일, 경로, route를 옮기거나 이름 변경`
- `:fire: Remove : 삭제(파일, 코드)`

개인적으로는 그냥 태그만 있는 것 보다는 깃모지가 있는게 알아보기 편한 것 같다.

## Issue PR 제목 형식

- `:sparkles: [FEAT] 기능구현 (eg. 회원가입 구현, UI 구현)`
- `:ambulance: [HOTFIX] 당장 0순위로 고쳐야 하는 상황`
- `:bug: [FIX] 버그 수정`
- `:white_check_mark: [TEST] 디버깅, 테스트 코드 추가`
- `:lipstick: [STYLE] 폰트 변경 등 코드에 영향을 주지 않는 변경 사항`
- `:recycle: [REFACTOR] 코드 리펙토링`
- `:wrench: [CHORE] 빌드 테스트, 패키지 매니저 설정 등 코드 수정이 없을 때`

## Issue templete

```md
## 구현할 기능
> 기능을 자세히 설명

## 체크리스트
- [ ] TODO

### ref) (선택)
```

버그 리포트 
```md
## 어떤 버그인지
> 기능을 자세히 설명

## 버그가 발생한 상황
> (~을 했는데, ~을 할 때, ~한 버그가 발생)

## 예상 결과 
> 예상했던 결과가 무엇인지

### ref) (선택)
```

## PR templete
```md
## 연관된 이슈

> ex) #이슈번호, #이슈번호

## 작업 내용

> 이번 PR에서 작업한 내용을 간략히 설명 (이미지 첨부)

### 스크린샷 (선택)

## 리뷰 요구사항(선택)
> 리뷰어가 특별히 봐주었으면 하는 사항
> ex) 메서드 XXX의 이름을 더 잘 짓고 싶은데 혹시 좋은 명칭이 있을까요?
```

## Branch name
`태그/이슈번호/기능명`

ex) `feature/#2/member`

**태그**
- `master` : 항상 실행 가능한 상태 유지 (최종 버전 올라가는 곳)
  - Team Leader가 release에서 pull request 후, merge
- `develop` : 항상 최신 버전이 유지된 브랜치
- `release` : master로 옮기기 전 검수용
- `hotfix` : 급하게 고쳐야 하는 코드 디버깅용


- `업무 종류` : 
    - 해당 업무 완료 후 develop 브랜치에 머지
    - ex) feature, refator, fix.....등등

## naming
**Class**
- PascalCase로 표기
- 클래스의 이름은 명사 또는 명사구문 _ex) Member_

**function**
- lowerCamelCase
- 함수의 이름은 동사 또는 동사구문
- 함수 이름만 보고도 어떤 기능을 하는지 힌트를 얻을 수 있어야 한다.
  - show... : 무언가를 보여주는 함수.  _ex) showMessage()_
  - get... : 값을 반환하는 함수.  _ex) getAge()_
  - calc... : 값을 반환하는 함수. _ex) calcSum()_
  - create... : 무언가를 생성하는 함수. _ex) createForm()_
  - check... : 무언가를 확인하고 불린값을 반환하는 함수. _ex) checkPermission()_
  - convert... : 무언가를 전환해주는 함수. _ex) convertToString()_
- 함수는 동작 하나만 담당해야된다.


**export되는 파일 내의 모든 상수는 모두 대문자로 표기**


ref) <br>
https://amaran-th.github.io/Github/[Github]%20Issue%20&%20PR%20Template%20%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0/