## Redis란?
메모리에 올려서 사용할 수 있는 key-value 형태의 DB 서버, NoSQL

<br>

## 왜 session이 아니고 redis?
<p align="center">
  <img src="https://github.com/nhnacademy-be5-no24/docs/assets/95386182/7144e02b-3c38-4019-9f05-bb8c1daf206c">
  출처 : https://ksh-coding.tistory.com/128#google_vignette
</p>

- session은 scale-out 시, 공유되지 않는다.

이러한 문제를 해결하는 방법 Sticky Session과 Session Clustering이 존재한다.

1. Sticky Session : 로드 밸런서의 설정을 통해 사용자의 요청이 처음 세션을 저장한 서버로만 가도록 설정
    - 실시간 트래픽과 상관 없이 세션이 저장된 서버에 요청이 가기 때문에 한 서버에 트래픽이 몰릴 수 있음 → 로드밸런싱 의미 X
    - 특정 서버에 장애가 발생하면 해당 서버에 존재하는 세션이 모두 사라질 수 있음

2. Session Clustering : 여러 WAS의 Session이 모두 공유되도록 하는 방법
   - 하나의 서버에 세션 생성 → 나머지 모든 서버의 세션 저장소에 같은 세션 생성
   - 서버 多 → 하나의 세션이 생성될 때 모든 서버에 세션을 생성해야 하기 때문에 서버의 메모리 부하가 커짐
   
<p align="center">
  <img src="https://github.com/nhnacademy-be5-no24/docs/assets/95386182/9a4444e7-fc40-4016-9876-90637e20a62b">
  출처 : https://ksh-coding.tistory.com/128#google_vignette
</p>

<br>

### 따라서 Redis Session Clustering 사용!
- 모든 서버가 같은 Redis Session 저장소를 바라보게 하는 방법
- 하나의 서버에서 세션이 생성될 때 한 번만 저장소에 저장됨 → 메모리 부하가 줄어듦
<p align="center">
  <img src="https://github.com/nhnacademy-be5-no24/docs/assets/95386182/65179213-28c6-4735-bc7e-cf4598a862c6">
  출처 : https://ksh-coding.tistory.com/128#google_vignette
</p>

<br>

## session 저장소로 RDB가 아니고 redis를 사용하는 이유는?
- 장바구니의 경우, 모든 사용자가 이용하기 때문에 저장소에 접근이 잦음
- 이때, 저장소가 RDB라면 디스크 I/O 작업이 많아지기 때문에 메모리 부하가 커짐<br>

### Redis
- In-memory 기반이기 때문에 디스크 I/O 작업 X → 메모리 낭비를 줄일 수 있음
- 빠른 성능
  - 평균 작업속도 < 1ms
  - 초당 수백만 건의 작업 가능
- TTL(Time-To-Live) 기능 제공
  - 데이터 만료 시간 설정 가능

<br>

## 그렇다면 redis 휘발성 문제는?
- 모든 데이터가 메모리에 저장되어 있기 때문에 서버 재시작 시 모든 데이터 유실
- 복제 기능을 사용해도 사람의 실수 발생 시, 데이터 복원 불가
- Redis를 캐시 이외의 용도로 사용한다면 적절한 데이터 백업 필요

### 따라서 AOF, RDB 방식 사용하여 강력한 내구성을 보장함!

1. AOF
2. RDB

# TODO
- redis 백업 방식 설명 추가
- redis를 사용했을 때의 장점을 지표로 보여줄 수 있는 자료 찾아보기
- 전반적인 내용 정리
