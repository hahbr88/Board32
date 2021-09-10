# 발견 문제점
## 1. 스프링 부트 앱 서버가 정상작동 하지 않음
> **원인** : 경로 잘못 기재 (이거 찾는데만 2시간 걸림 ㅠ)

```java
// WriteDAO.XML 33번 줄 수정
<select id="selectByUid" resultType="com.lec.spring.WriteDTO">  
==> <select id="selectByUid" resultType="com.lec.spring.domain.WriteDTO">

```

## 2. '수정' 시 수정완료 메시지가 떴지만 400 에러
> **원인** : UPDATE 할땐 post 방식으로 업데이트 해야한다.  
> (type=Bad Request, status=400) 라고 나옴
>> 이게 아닌가... ㅠㅠ 왜 안되지 ㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠㅠ
```java
// BoardController 66번 줄 수정
@RequestMapping("/updateOk.do")  ==> @PostMapping("/updateOk.do")

```



## 3. '삭제' 시 500 에러
> **원인** : 쿼리문 오류, uid가 아니라 wr_uid로 써야함 

```java
// WriteDAO.XML 60번 줄 수정
DELETE FROM test_write WHERE uid = #{uid} ==> DELETE FROM test_write WHERE wr_uid = #{uid}

```