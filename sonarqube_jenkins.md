## SonarQube와 Jenkins 연동


소나큐브는 Jacoco를 통해 만들어진 xml 리포트를 바탕으로 코드 커버리지를 분석한다. 그렇기 때문에 빌드시에 만들어진 jacoco 리포트가 없다면 소나큐브를 실행해도 코드커버리지는 0%로 나오게 된다.
따라서 빌드의 순서는 다음과 같이 진행되어야 한다.

1. test
2. jacocoTestReport
3. jacocoTestCoverageVerification
4. SoanrQube

따라서, jenkins 환경에서 pre step에서가 아닌, post step에서 작동을 해야 test 이후 test 결과가 정상적으로 반영됨.

<img width="1113" alt="image" src="https://github.com/nhnacademy-be5-no24/docs/assets/43560497/6d9ad2ec-364f-43f9-89b4-60b7d48c47ba">

ref. https://young-bin.tistory.com/94
