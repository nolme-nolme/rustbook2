# 범위(Scope)와 쉐도잉(Shadowing)

현재 범위에 있는 변수와, 바깥 범위에 있는 변수 모두 가릴(쉐도잉)수 있습니다:

```rust
fn main() {
    let a = 10;
    println!("before: {a}");

    {
        let a = "hello";
        println!("inner scope: {a}");

        let a = true;
        println!("shadowed in inner scope: {a}");
    }

    println!("after: {a}");
}
```

<details>

<summary>발표자 노트</summary>

* 쉐도잉은 기존 변수에 새로운 값을 할당하는 것이 아닙니다. 쉐도잉을 하면 새로운 변수가 생기며, 이전 변수와 새 변수는 메모리의 서로 다른 위치에 존재합니다. 그 두 변수는 단지 이름이 같은 뿐이며, 코드 중 어디에서 그 이름이 사용되었느냐에 따라 어떤 변수를 지칭하는 지가 결정됩니다.
* 쉐도잉 시 타입을 바꿀 수 있습니다.
* 처음에 쉐도잉을 보면 코드를 더 모호하게 만든다고 생각할 수 도 있습니다. 그러나 실제로 쉐도잉을 이용하면, 어떤 변수에서 `.unwrap()` 된 값을 새로운 변수에 담을 경우 새로운 이름을 지을 필요 없이 기존 이름을 유지할 수 있어서 편리합니다.
* 아래 코드는 불변 변수를 쉐도잉할 때 타입이 동일하더라도 새 변수가 원래 변수의 메모리 위치를 재사용 할 수 없는지 그 이유를 보여줍니다.

```rust
fn main() {
    let a = 1;
    let b = &a;
    let a = a + 1;
    println!("{a} {b}");
}
```

</details>

<details>

<summary>놀미 노트</summary>

* 쉐도잉은 동일 이름을 다른 타잎으로 쓸 수도 있기 때문에 좋은 방법은 아닐 듯 합니다. 매우 편리하여 꼭 쓰면 좋은 곳 외에는 안 쓰는 것이 나아 보입니다.
* 러스트는 블록(함수 블럭, 모듈 블록)이 범위(Scope)를 대부분 결정합니다.

</details>

<details>

<summary>연습</summary>

* 발표자 노트의 코드가 컴파일 되는가요? 된다면 b와 a 값은 무엇인가요?

</details>
