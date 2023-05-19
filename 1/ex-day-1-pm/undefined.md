# 반복자와 소유권

러스트의 소유권 모델은 많은 API에 반영이 되어 있습니다. 예를들어 [`Iterator`](https://doc.rust-lang.org/std/iter/trait.Iterator.html) 와 [`IntoIterator`](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html) 같은 트레잇이 있습니다.

## [`Iterator`](https://google.github.io/comprehensive-rust/ko/exercises/day-1/iterators-and-ownership.html#iterator) <a href="#iterator" id="iterator"></a>

트레잇은 타입에 대한 행동(메서드)를 설명한다는 점에서 인터페이스와 유사합니다. `Iterator`는 단순히 `None`이 나올때까지 `next`를 호출하는 것이 가능하다는 것을 나타내는 트레잇입니다:

```rust
pub trait Iterator {
    type Item;
    fn next(&mut self) -> Option<Self::Item>;
}
```

`Iterator` 트레잇은 이렇게 사용합니다:

```rust
fn main() {
    let v: Vec<i8> = vec![10, 20, 30];
    let mut iter = v.iter();

    println!("v[0]: {:?}", iter.next());
    println!("v[1]: {:?}", iter.next());
    println!("v[2]: {:?}", iter.next());
    println!("No more items: {:?}", iter.next());
}
```

반복자가 반환하는 값들은 타입이 뭘까요? 여기서 답을 테스트 해 보세요:

```rust
fn main() {
    let v: Vec<i8> = vec![10, 20, 30];
    let mut iter = v.iter();

    let v0: Option<..> = iter.next();
    println!("v0: {v0:?}");
}
```

왜 이런 타입이 사용되는 것일까요?

## [`IntoIterator`](https://google.github.io/comprehensive-rust/ko/exercises/day-1/iterators-and-ownership.html#intoiterator) <a href="#intoiterator" id="intoiterator"></a>

`Iterator` 트레잇은 생성된 반복자를 _사용_하는 방법을 알려줍니다. 반면 `IntoIterator` 트레잇은 반복자를 _생성_하는 방법을 알려줍니다:

```rust
pub trait IntoIterator {
    type Item;
    type IntoIter: Iterator<Item = Self::Item>;

    fn into_iter(self) -> Self::IntoIter;
}
```

`IntoIterator`의 모든 구현은 반드시 다음의 두 타입을 선언해야합니다:

* `Item`: `i8`과 같이 반복되는 값의 타입
* `IntoIter`: `into_iter` 메서드에서 반환되는 `Iterator`타입.

`IntoIter`에는 `Item`이 연결되어 있음을 주목하세요. `IntoIter` 반복자는 `Item` 타입의 데이터를 가리켜야 합니다. 즉, 반복자는 `Option<Item>`을 리턴합니다.

이전과 마찬가지로, 반복자가 반환하는 타입은 무엇입니까?

```rust
fn main() {
    let v: Vec<String> = vec![String::from("foo"), String::from("bar")];
    let mut iter = v.into_iter();

    let v0: Option<..> = iter.next();
    println!("v0: {v0:?}");
}
```

## [배열과 `for` 반복문](https://google.github.io/comprehensive-rust/ko/exercises/day-1/iterators-and-ownership.html#%EB%B0%B0%EC%97%B4%EA%B3%BC-for-%EB%B0%98%EB%B3%B5%EB%AC%B8) <a href="#for" id="for"></a>

자, 이제 우리는 `Iterator`와 `IntoIterator`를 알았으므로 `for` 루프를 만들 수 있습니다. `for` 루프는 `into_iter()`를 호출하여 반복자를 만든 다음 그 반복자를 이용하여 요소들을 반복해서 접근합니다:

```rust
fn main() {
    let v: Vec<String> = vec![String::from("foo"), String::from("bar")];

    for word in &v {
        println!("word: {word}");
    }

    for word in v {
        println!("word: {word}");
    }
}
```

매 루프에서 `word`의 타입은 무엇입니까?

위 코드에서 실험 해 본 후 다음 문서를 참조해서 답변을 확인하시기 바랍니다: [`impl IntoIterator for &Vec<T>`](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-IntoIterator-for-%26%27a%20Vec%3CT%2C%20A%3E), [`impl IntoIterator for Vec<T>`](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-IntoIterator-for-Vec%3CT%2C%20A%3E)
