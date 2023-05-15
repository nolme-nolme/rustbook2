# 패턴 일치(Pattern Matching)

패턴 일치 또는 패턴 맞추기는 매우 강력하고 편리한 러스트 기능입니다. 함수형 언어에서 많이 쓰이던 기능을 러스트가 여러 곳에서 활용 가능하도록 했습니다.&#x20;

`match`키워드는 값을 여러 형태의 패턴과 매치시킬 수 있습니다. 맨 위 패턴부터 하나씩 매치되는지 검사하며, 처음으로 매치되는 패턴이 선택됩니다.

C/C++의 `switch`와 비슷하게 값을 패턴으로 사용할 수도 있습니다:

```rust
fn main() {
    let input = 'x';

    match input {
        'q'                   => println!("Quitting"),
        'a' | 's' | 'w' | 'd' => println!("Moving around"),
        '0'..='9'             => println!("Number input"),
        _                     => println!("Something else"),
    }
}
```

`_`패턴은 어떤 값과도 매칭되는 와일드카드입니다.

발표자 노트의 설명입니다.&#x20;

* 패턴에서 사용되는 특수 문자들을 알려주세요.
  * `|`: or 기호입니다.
  * `..`: 필요한 만큼 확장합니다.
  * `1..=5`: 끝 값(여기서는 5)을 포함하는 범위를 나타냅니다.
  * `_`: 와일드카드입니다.
* **\[1]** 와일드카드 문자를 변수로 바꾸거나 `q`의 따옴표를 제거하는 식으로 수정하면서 바인딩이 어떻게 작동하는지 보여주는 것도 유용할 수 있습니다.
* **\[2]** 참조를 매칭하는 것도 시연할 수 있습니다.
* **\[3]** 에러 메시지에 “반박 불가능 패턴(irrefutable pattern)“이란 용어가 등장하기도 합니다. 지금 그 의미를 소개하는 것도 좋을 것 같습니다.

**\[1]** 직접 실행해 보면 알 수 있을 듯 합니다.&#x20;

**\[2]** 참조를 매칭한다는 뜻은 \&v 같이 변수에 대해 한다는 뜻입니다.&#x20;

```rust
let v = 'a';
let rv = &v;

match rv {
    &m => println!("{}", m),
    _ => println!("not a reference")
}
```

**\[3]**   반박 불가능 패턴(irrefutable pattern)은 항상 매칭되는 패턴이라는 뜻입니다. 여러 패턴 중 일부만 매칭되면 반박가능한 패턴(refutable pattern)이라고 합니다. 러스트 [언어 문서의 반박 항목](https://doc.rust-lang.org/book/ch18-02-refutability.html)에 자세히 나와 있습니다. 놀라운 점은 `let`도 패턴 매칭 구분이라는 점입니다. 따라서, `if let` 이나 `while let` 구문이 매우 자연스러운 문법이 됩니다.&#x20;
