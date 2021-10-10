# guess-the-number

a small game by rust

```rust
use rand::{thread_rng, Rng};
use std::io::stdin;

const ERROR_MESSAGE: &str = "Failed to read line, please try again!";

const TRY_MESSAGE: &str = "please try agian !";

fn main() {
    println!("📚  Welcome to the guessing number game 🎉 🎉 🎉 \n");
    println!("💬  Please choose the number range you want first:");

    let range_number = loop {
        let mut temp_number = String::new();
        stdin().read_line(&mut temp_number).expect(ERROR_MESSAGE);
        let temp_number: u32 = match temp_number.trim().parse() {
            Ok(num) => num,
            Err(_) => {
                println!("⚠️  The number range must be a number type, {}", TRY_MESSAGE);
                continue;
            }
        };
        break temp_number;
    };

    let key: u32 = thread_rng().gen_range(0..=range_number);

    println!("🔑  The answer is between 0 and {}\n", range_number);

    loop {
        println!("❓  Please enter the answer you guessed:");
        let mut input = String::new();
        stdin().read_line(&mut input).expect(ERROR_MESSAGE);
        let input: u32 = match input.trim().parse() {
            Ok(num) => num,
            Err(_) => {
                println!("⚠️  The answer must be a number type, {}\n", TRY_MESSAGE);
                continue;
            }
        };

        if input < key {
            println!("The guessed number is too small, {}", TRY_MESSAGE);
        } else if input > key {
            println!("The guessed number is too big, {}", TRY_MESSAGE);
        } else {
            println!("Congratulations ! You won the game 🎉 🎉 🎉");
            break;
        }
    }
}

```