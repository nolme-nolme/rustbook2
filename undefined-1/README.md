# 열거형

`enum` 키워드는 몇가지 유형(variant)으로 표현되는 타입을 생성합니다:

```rust
fn generate_random_number() -> i32 {
    4  // Chosen by fair dice roll. Guaranteed to be random.
}

#[derive(Debug)]
enum CoinFlip {
    Heads,
    Tails,
}

fn flip_coin() -> CoinFlip {
    let random_number = generate_random_number();
    if random_number % 2 == 0 {
        return CoinFlip::Heads;
    } else {
        return CoinFlip::Tails;
    }
}

fn main() {
    println!("You got: {:?}", flip_coin());
}
```

열거형은 다른 언어에서 볼 수 있는 분류를 위해서 사용할 수 있습니다.&#x20;

다른 언어와 달리 러스트의 열거형은 구현(impl) 블록에서 함수를 추가할 수 있습니다. 또 다른 타잎들을 분류로 포함할 수 있습니다. 이를 대수적 자료 구조라고 하는데 패턴 일치와 함께 러스트에서 매우 중요한 도구로 사용합니다.&#x20;



