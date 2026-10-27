# 단축평가 (Short-circuit evaluation)

## 단축평가란?

`and`, `or` 연산에서 **앞쪽만 보고 결과가 정해지면 뒤쪽은 실행하지 않는** 규칙이다.

```python
True or print("실행 안 됨")    # 앞이 True라서 뒤는 건너뜀
False and print("실행 안 됨")  # 앞이 False라서 뒤는 건너뜀
```

- `A or B` : A가 참이면 A, 아니면 B를 돌려줌
- `A and B`: A가 거짓이면 A, 아니면 B를 돌려줌

## 정리

1. 단축평가로 코드를 쓴다고 **실행 속도가 눈에 띄게 빨라지는 건 아니다.**
2. 그래서 짧게 쓰는 것보다 **다른 사람이 이해하기 쉬운 코드가 더 좋다.**
3. 웹개발에서는 화면 표시, 기본값 설정, URL 파라미터 처리 등에 단축평가를 자주 사용한다.

## 자주 쓰는 패턴

### 기본값 주기

```python
name = input_name or "손님"   # input_name이 비어 있으면 "손님"
```

### 값이 있을 때만 다음 단계 실행

```python
if user and user.is_admin:    # user가 None이면 뒤쪽은 실행하지 않아 오류가 안 남
    ...
```

### 웹개발 예시

- 파이썬 서버 코드: `page = request.args.get("page") or 1` (주소에 page 값이 없으면 1)
- 자바스크립트(React) 화면: `{isLoggedIn && <MyInfo />}` (로그인했을 때만 표시)

## 주의할 점

- `or`은 `0`, `""`(빈 문자열), `[]`(빈 리스트)도 "없는 값"으로 본다.
  `count = input_count or 10`에서 입력이 `0`이면 `10`이 되어버린다.
- `조건 and A or B`처럼 꼬아 쓰지 말고 `A if 조건 else B`를 쓴다.

## 참고

- 웹의 **URL 단축**(bit.ly 같은 짧은 주소)은 이름만 비슷하고 단축평가와 관계없다.
