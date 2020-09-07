# Hash Table (해시 테이블) 
`해시함수`를 사용하여 키(key) 값을 변환한 `인덱스(index) 값과 데이터 값(value)이 하나의 쌍`을 이루는 데이터 구조

#### 원래 데이터의 값(key) -> Hash Function -> Hash Code -> Index -> Index와 Value값 매핑

#### Hash(해시)  
데이터를 다루는 기법

#### Hash function (해시 함수) 
데이터를 효율적으로 관리하기 위하여 임의의 길이의 데이터를 고정된 길이의 데이터로 매핑하는 함수

### 장단점

> **장점**  
> 
> - 적은 리소스로 많은 데이터를 효율적으로 관리
> - Index 사용으로 검색, 삽입, 삭제가 빠름 
> - key, hash 값이연관성이 없어 보안에 많이 사용 
> 
> **단점**
>  
> - 충돌 순서가 있는 배열에는 어울리지 않음 
> - 해시 함수의 의존도가 높음

## 충돌
해시함수를 사용하여 이미 값이 매핑된 인덱스 값에 또 다른 데이터가 매핑 될 경우 충돌이 일어난다.

### 해결
1. **체인법(Chaining)**

	같은 해시 값을 갖는 데이터를 `연결 리스트`에 의해 사슬 모양으로 연결

> **장점** 
> 
> - 한정된 저장소를 효율적으로 사용 
> - 상대적으로 적은 메모리 사용 
> 
> **단점** 
> 
> - 한 hash에 자료들이 계속 연결된다면 검색효율이 떨어짐 
> - 외부 저장공간 사용

2. **오픈 해시법(open hashing)**

	빈 버킷을 찾을 때까지 해시를 반복
- 선형탐사(Linear Probing) : 충돌이 발생할 경우 해당 인덱스 뒤에 있는 버킷 중 빈 버킷을 찾아 데이터를 넣는다.

- 제곱 탐사(Quadratic probing) : 제곱수의 폭으로 빈 버킷을 찾아 데이터를 넣는다.
- 이중해싱(double hashing) : 다른 해시함수를 한 번 더 적용한 해시에 데이터를 넣는다.

> **장점** 
> 
> - 해시 테이블 내에서 데이터를 저장 및 처리 
> 
> **단점**
>  
> - 해시함수의 성능이 전체 해시테이블의 성능에 영향을 줌 
> - 데이터의 길이가 늘어나면 그만큼의 저장소가 더 필요함

#### [참고자료]
1. [enter link description here](https://velog.io/@cyranocoding/Hash-Hashing-Hash-Table%ED%95%B4%EC%8B%9C-%ED%95%B4%EC%8B%B1-%ED%95%B4%EC%8B%9C%ED%85%8C%EC%9D%B4%EB%B8%94-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EC%9D%98-%EC%9D%B4%ED%95%B4-6ijyonph6o)
2. [enter link description here](https://ratsgo.github.io/data%20structure&algorithm/2017/10/25/hash/)
