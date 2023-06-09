# 안전하지 않은 러스트 (Unsafe Rust)

unsafe rust 원문도 그렇지만 안전하지 않은 러스트는 용어 선택이 적절하지 않아 보입니다. 안전하지 않다기 보다는 잘 살펴서 구현해야 하는 강력한 도구 블록이라고 봐야 합니다.

러스트로 작성된 프로그램은 크게 두 부분으로 나뉩니다:

* **안전한 러스트:** 메모리 관련 오류 발생 불가능, 정의되지 않은 동작 없음.
* **안전하지 않은 러스트:** 특별한 조건을 만족하지 않은채로 사용되면 정의되지 않은 동작을 유발할 수 있음.

이 강의는 대부분 안전한 러스트에 대해 다루지만 안전하지 않은 러스트가 무엇인지는 알아 두어야 합니다.

보통, 안전하지 않은 러스트 코드는 크기가 작으며, 독립적으로 존재합니다. 그리고 코드가 왜 잘 작동하는지에 대해 세밀하게 문서화가 되어 있습니다. 그리고, 많은 경우 안전한 러스트 코드를 통해서 추상화를 시킨 후 사용하게 됩니다.

안전하지 않은 러스트를 이용하면 다음과 같은 다섯 가지 것들이 가능해 집니다:

* 원시 포인터 역참조(따라가기)
* 정적 가변변수 접근 및 수정
* `union` 필드 접근
* `extern` 함수를 포함한 `unsafe` 함수 호출
* `unsafe` 트레잇 구현.

위 기능들에 대해 간략히 살펴보겠습니다. 자세한 내용은 [러스트 프로그래밍 언어, 19.1절](https://doc.rust-lang.org/book/ch19-01-unsafe-rust.html)과 [Rustonomicon](https://doc.rust-lang.org/nomicon/)를 참조하세요.

<details>

<summary>발표자 노트</summary>

안전하지 않은 러스트라고 해서 코드가 부정확 하다는 뜻은 아닙니다. 여기서 안전하지 않다의 의미는 컴파일러가 제공해주는 안전 장치들이 꺼진 상태이며, 개발자가 스스로 정확하고 안전한 코드를 작성해야 함을 의미합니다. 이는 컴파일러가 더 이상 러스트의 메모리 안전과 관련된 규칙들을 적용하지 않는다는 것입니다.

</details>

