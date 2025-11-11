
디지털 포렌식 수사 - SQL CTF (Magnet Axiom 2024 - android)



## 🔍 사건 개요

### 배경
2023년 12월, Chadwick Elms(Chad)가 온라인 게임 아이템 사기 피해를 신고했습니다.
피의자 Rocco Sachs의 Google Pixel 3a XL 기기를 압수하여 포렌식 분석을 진행합니다.

### 분석 목표
압수한 포렌식 데이터(16개 CSV 파일)를 SQL로 분석하여 사건의 타임라인을 정리하세요!


## 📋 수사 지침


### 허용되는 SQL 문법
```sql
SELECT / FROM / JOIN  ON / WHERE / GROUP BY / HAVING / ORDER BY / LIMIT
```

### 수사 방법
1. 각 질문에 대해 관련 테이블을 탐색하세요
2. 힌트의 탐색 쿼리를 참고하여 단계적으로 접근하세요
3. 데이터를 분석하여 답을 찾아내세요

---


## 수사 #1: 신원 확인
**난이도**: Easy


### ❓ 질문
**디바이스와 관련있는 이메일은 무엇인가?**


💡 **수사 힌트**:
1. 먼저 어떤 테이블들이 있는지 확인: `.tables` (SQLite 기준)
2. 사용자 계정 관련 테이블 탐색: `User_Accounts`, `Accounts_Information`
3. 이메일 형식(@가 포함된) 계정 찾기
4. 가장 많이 사용된 계정이 주 계정일 가능성이 높음

🔍 **탐색 쿼리 예시**:
```sql
-- 1단계: User_Accounts 테이블 확인
SELECT * FROM User_Accounts LIMIT 5;

-- 2단계: 이메일 형식 찾기
SELECT "User Name" FROM User_Accounts WHERE "User Name" LIKE '%@%';

-- 3단계: 가장 많이 사용된 계정 찾기
SELECT "User Name", COUNT(*) as usage_count
FROM Accounts_Information
GROUP BY "User Name"
ORDER BY usage_count DESC
LIMIT 5;
```


## 수사 #2: 게임 활동
**난이도**: Medium


### ❓ 질문
**Rocco의 Call of Duty Username은 무엇인가?**

💡 **수사 힌트**:
1. Call of Duty는 게임이므로 검색 기록을 확인
2. 게임 관련 앱 설치 여부 확인
3. `대화`를 하며 언급했을 수 있음
4. 여러 단계 SQL 가능

---

## 수사 #3: 소셜 미디어
**난이도**: Easy


### ❓ 질문
**Rocco의 Twitter account name은 무엇인가?**

💡 **수사 힌트**:
1. 없음
---

## 수사 #4: 통신 기록
**난이도**: Easy


### ❓ 질문
**Rocco가 Twitter Direct Message로 보낸 메시지는 총 몇 건인가?**


💡 **수사 힌트**:
1. 없음
---

## 수사 #5: 통신 기록
**난이도**: Medium


### ❓ 질문
**(문제 4에 이어) Rocco가 가장 많이 메시지를 보낸 수신자는 누구인가?**

💡 **수사 힌트**:
1. 없음

---


## 수사 #6: 활동 기록
**난이도**: Medium


### ❓ 질문
**Rocco가 가장 최근에 사용했던 서비스는?**


💡 **수사 힌트**:
1. 없음
---

## 수사 #7: 시간대 분석
**난이도**: Easy


### ❓ 질문
**가장 많은 메시지가 교환된 날짜는?**


💡 **수사 힌트**:
1. 없음
---

## 수사 #8: 관계 분석
**난이도**: Hard


### ❓ 질문
**Rocco에게 화가 난 (upset) 사람의 아이디는?**

💡 **수사 힌트**:
1. `전화`가 아니라 `메시지`


---


## 수사 #9: 행동 패턴
**난이도**: Easy


### ❓ 질문
**Rocco가 가장 많이 검색한 주제는?**

💡 **수사 힌트**:
1. 없음

---


## 수사 #10: 회피 계획
**난이도**: Expert


### ❓ 질문
**Rocco가 관심을 가진 컨퍼런스는? (이름 & 무엇을 위한 컨퍼런스인지)**

💡 **수사 힌트**:
1. 검색기록


---


## 수사 #11: 사건 타임라인
**난이도**: Expert

### ❓ 질문
**그 외 필요한 정보를 SQL을 사용하여 추출하고, 사건의 타임라인을 정라하세요!**

💡 **수사 힌트**:
1. 위에서 알아낸 정보를 조합하여 타임라인을 만들어보세요.
