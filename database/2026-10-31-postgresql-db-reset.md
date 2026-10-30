# PostgreSQL DB 삭제 후 다시 만들기

`netflix` DB를 지우고 처음부터 다시 만드는 절차.
**psql**(터미널에서 PostgreSQL을 조작하는 프로그램)에서 실행한다.

> `DROP DATABASE`는 되돌릴 수 없다. 안의 데이터가 전부 사라진다.

## 절차

```sql
-- 1. 다른 DB로 이동 (접속 중인 DB는 지울 수 없다)
\c postgres

-- 2. 삭제 (WITH (FORCE): 접속 중인 사람이 있어도 강제로 끊고 삭제)
DROP DATABASE netflix WITH (FORCE);

-- 3. 다시 만들기 (OWNER: DB의 주인 계정, sd4 유저에게 권한 주기)
CREATE DATABASE netflix OWNER sd4;

-- 4. 새 DB로 이동한 뒤 setup.sql 실행
\c netflix
\i setup.sql
```

5. DBeaver(DB를 그래픽 화면으로 보여주는 프로그램)에서 `fixes.sql`을 열고 **Alt+X**로 전체 실행한다.

## psql 명령어

| 명령 | 설명 |
|---|---|
| `\l` | DB 목록 |
| `\d` | 현재 DB 안의 테이블 목록 |
| `\conninfo` | 현재 접속 정보 |
| `\c DB명` | 다른 DB로 이동 |
| `\i 파일명` | SQL 파일 실행 |

## 주의할 점

- `\!`는 운영체제 명령을 실행하는 기호라 SQL 파일이 실행되지 않는다. 파일 실행은 `\i`를 쓴다.
- 4번에서 `\c netflix`를 빼면 엉뚱한 DB(`postgres`)에 setup.sql이 실행될 수 있다.

## 인코딩 문제 해결

한글이 깨질 때:

```sql
SET client_encoding TO 'UTF8';
```
