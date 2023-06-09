# 비교

메모리 관리 기술의 대략적인 비교입니다.

## 메모리 관리 방법 별 장점

* C와 같은 수동 관리:
  * 런타임 오버헤드가 없음.
* JAVA와 같은 자동화 관리:
  * 완전한 자동화.
  * 안전하고 정확함.
* C++ 와 같은 범위 기반 관리:
  * 부분 자동화
  * 런타임 오버헤드가 없음.
* 러스트와 같은 컴파일러 수행 범위 기반 관리:
  * 컴파일러에 의해 수행됩니다.
  * 런타임 오버헤드가 없습니다.
  * 안전하고 정확합니다.

메모리 관리 방법 별 단점

* C와 같은 수동 관리:
  * 사용 후 해 제 문제.
  * 이중 해제 문제.
  * 메모리 누출 문제.
* JAVA와 같은 자동화 관리:
  * GC동작으로 인한 멈춤.
  * 소멸자 지연 (역주: 특정 메모리를 더이상 사용하지 않더라도 곧바로 해제 되지 않고 GC가 동작할 때 까지 기다려야 한다는 점)
* C++ 와 같은 범위 기반 관리:
  * 복잡하며, 개발자의 선택사항임.
  * 사용 후 해제 문제 가능성 있음.
* 러스트와 같은 컴파일러가 강제하는 수행 범위 기반 관리:
  * 약간의 초기 복잡성.
  * 올바른 프로그램이지만 컴파일러가 거부할 수 있음.
