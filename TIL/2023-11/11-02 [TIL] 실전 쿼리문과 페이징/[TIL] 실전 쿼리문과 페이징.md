# [TIL] 실전 쿼리문과 페이징

### 목차
- [\[TIL\] 실전 쿼리문과 페이징](#til-실전-쿼리문과-페이징)
    - [목차](#목차)
  - [😃 잡담](#-잡담)
  - [📄 배운 내용](#-배운-내용)
    - [좋아요 집계](#좋아요-집계)
    - [해시태그를 통한 검색](#해시태그를-통한-검색)
    - [Paging](#paging)

##  😃 잡담
오늘은 서버 스터디를 위해 실제로 프로젝트에서 쿼리문을 어떤 방식으로 작성해야 하는가에 대해 공부하게 되었다.<br>
몇가지의 요구 사항에 대해 어떻게 쿼리를 짜고 만들어야하는지에 대해 생각해볼 수 있었다. 해당 내용을 추후 서버 파트로 프로젝트를 진행할 때 중요하다고 판단되어 이렇게 TIL로 정리 하고자 한다.


## 📄 배운 내용
### 좋아요 집계
> 차단한 사용자의 좋아요는 집계하지 않는다면?

***해당 경우를 위해 책 테이블에 좋아요 컬럼을 만들기 보다는 좋아요 테이블을 따로 만들어, DML 연산으로 좋아요 집계를 하는 것이 좋다***

*예시*
```sql
SELECT count(*) 
from book_like 
where book_id=3;
```
```sql
-- 차단한 사용자의 좋아요는 포함하지 않는 경우

SELECT count(*) 
from book_like 
where book_id=3
AND user_id NOT IN (
    SELECT targert_id 
    FROM block 
    WHERE Owner_id = 2);
```

### 해시태그를 통한 검색
> M:N의 관계에서의 쿼리문을 어떻게 작성해야할까?

- ***조인 or 서브 쿼리 이용***

```sql
SELECT *
FROM book
WHERE book_id IN(
    SELECT book_id
    FROM book_hashtag
    WHERE hashtag_id =(
        SELECT hashtag_id
        From hashtag
        WHERE hashtag_name='hana'
    )
);

```

### Paging

**Offset Paging**
> Offset으로 몇개를 건너뛸지를 정함
```sql
-- 최신 순으로 정렬된 책 목록
-- n번의 페이지에 대해 한번에 10개씩 보여주는 경우

SELECT*
FROM book
ORDER BY created_at desc
limit 10 offset (n - 1) * 10;
```

**Cusor Paging**
> 커서로 가르켜 페이징을 함

- 커서는 마지막으로 조회한 콘텐츠
- Offset Paging의 경우, 페이지를 넘어가는 순간 게시글이 추가된다면, 전 페이지에서 봤던 게시글이 또 보일 수 있음
  - 따라서, 이런 단점 보완을 위해 Cusor Paging을 사용할 수 있음

```sql

SELECT * 
FROM book 
WHERE book.likes < 
		(SELECT likes 
        FROM book 
        WHERE id = 4)
			ORDER BY likes desc limit 15;
```