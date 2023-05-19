# HashMap

HashDoS 공격으로부터 보호되는 표준 해시 맵입니다:

```rust
use std::collections::HashMap;

fn main() {
    let mut page_counts = HashMap::new();
    page_counts.insert("Adventures of Huckleberry Finn".to_string(), 207);
    page_counts.insert("Grimms' Fairy Tales".to_string(), 751);
    page_counts.insert("Pride and Prejudice".to_string(), 303);

    if !page_counts.contains_key("Les Misérables") {
        println!("We know about {} books, but not Les Misérables.",
                 page_counts.len());
    }

    for book in ["Pride and Prejudice", "Alice's Adventure in Wonderland"] {
        match page_counts.get(book) {
            Some(count) => println!("{book}: {count} pages"),
            None => println!("{book} is unknown.")
        }
    }

    // Use the .entry() method to insert a value if nothing is found.
    for book in ["Pride and Prejudice", "Alice's Adventure in Wonderland"] {
        let page_count: &mut i32 = page_counts.entry(book.to_string()).or_insert(0);
        *page_count += 1;
    }

    println!("{page_counts:#?}");
}
```

<details>

<summary>발표자 노트</summary>

* `HashMap`은 prelude에 정의되어 있지 않기 때문에 명시적으로 추가해줘야 합니다.
*   아래 코드를 테스트해보세요. 첫 문장에서는 해시맵에 책이 있는지 검사하여, 없으면 디폴트 값을 반환합니다. 두번 째 문장에서는 해시맵에 해당 책이 없는 경우, 지정한 값을 해시맵에 추가한 뒤 그 값을 반환합니다.

    ```rust
      let pc1 = page_counts
          .get("Harry Potter and the Sorcerer's Stone ")
          .unwrap_or(&336);
      let pc2 = page_counts
          .entry("The Hunger Games".to_string())
          .or_insert(374);
    ```
* 안타깝지만 `hashmap!`같은 매크로가 없습니다.
  *   러스트 1.56부터는 `HashMap`이 [`From<[(K, V); N]>`](https://doc.rust-lang.org/std/collections/hash\_map/struct.HashMap.html#impl-From%3C%5B\(K%2C%20V\)%3B%20N%5D%3E-for-HashMap%3CK%2C%20V%2C%20RandomState%3E)을 구현하기 때문에 배열 리터럴을 이용하여 쉽게 해시맵을 초기화할 수 있습니다:

      ```rust
        let page_counts = HashMap::from([
          ("Harry Potter and the Sorcerer's Stone".to_string(), 336),
          ("The Hunger Games".to_string(), 374),
        ]);
      ```
* 키-값 쌍에 대한 `Iterator`로 해시맵을 만들 수도 있습니다.
* 예제 코드에서는 편의상 해시맵의 키로 `&str`를 사용하지 않았습니다. 물론 컬렉션에 참조를 사용할 수도 있습니다. 다만 참조를 사용하게 되면 빌림 검사기 때문에 복잡해 질 수 있습니다.
  * 예제 코드에서 `to_string()`을 없애도 컴파일에 문제가 없는지 확인해보세요. 어떤 문제에 부딪힐까요?

</details>

