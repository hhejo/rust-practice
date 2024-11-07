# Rust practice

## 0. Cargo

```bash
$ cargo new my-project --bin
$ cargo run
```

## 1. Hello, world!

```rust
fn main() {
    println!("Hello, world!");
}
```

## 2. Input

```rust
use std::io;

fn main() {
    println!("#1 _ 두 수를 띄워 입력하세요.");
    let mut user_input = String::new(); // 빈 문자열 생성
    io::stdin().read_line(&mut user_input).expect("입력 실패.");
    let mut numbers = user_input // 이터레이터 생성
        .trim() // 양 끝 공백 제거
        .split_whitespace() // 띄어쓰기로 문자열 분리
        .map(|s| s.parse::<i32>()); // 각 단어를 i32로 변환
                                    // println!("numbers: {:#?}", numbers); // {:?}에서 #을 붙인 {:#?}는 pretty print
    let x = match numbers.next() {
        Some(Ok(num)) => num,
        _ => {
            println!("첫 번째 숫자를 올바르게 입력하세요.");
            return;
        }
    };
    let y = match numbers.next() {
        Some(Ok(num)) => num,
        _ => {
            println!("두 번째 숫자를 올바르게 입력하세요.");
            return;
        }
    };
    println!("#1 _ x: {x}, y: {y}");
    println!("");

    println!("#2 _ 두 수를 띄워 입력하세요.");
    let mut user_input = String::new();
    io::stdin().read_line(&mut user_input).expect("입력 실패.");
    let numbers: Vec<i32> = user_input
        .trim()
        .split_whitespace()
        .map(|s| s.parse::<i32>().expect("숫자를 입력하세요."))
        .collect(); // 이터레이터의 요소를 벡터로 수집
    let [x, y]: [i32; 2] = [numbers[0], numbers[1]];
    println!("#2 _ x: {x}, y: {y}");
    println!("");

    println!("#3 _ 두 수를 띄워 입력하세요.");
    let mut user_input = String::new();
    io::stdin().read_line(&mut user_input).expect("입력 실패.");
    let (x, y): (i32, i32) = {
        let mut numbers = user_input
            .trim()
            .split_whitespace()
            .map(|s| s.parse::<i32>().expect("숫자를 입력하세요."));
        (numbers.next().unwrap(), numbers.next().unwrap())
    };
    println!("#3 _ x: {x}, y: {y}");
    println!("");
}
```
