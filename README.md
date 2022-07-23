# test_gluesql

### Installation
```sh
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

```sh
$ rustc --v
$ cargo new test_gluesql
$ cargo run
```

- cargo.toml
```
[dependencies]
gluesql = "0.11"
```

### Usage
```sh
$ notepad .\src\main.rs
```
```rs
use gluesql::prelude::*;
fn main() {
    let storage = SledStorage::new("data/doc-db").unwrap();
    let mut glue = Glue::new(storage);
    let sqls = vec![
        "DROP TABLE IF EXISTS Glue;",
        "CREATE TABLE Glue (id INTEGER);",
        "INSERT INTO Glue VALUES (100);",
        "INSERT INTO Glue VALUES (200);",
        "SELECT * FROM Glue WHERE id > 100;",
    ];
    for sql in sqls {
        let output = glue.execute(sql).unwrap();
        println!("{:?}", output)
    }
}
```

### Build
```sh
$ cargo build
   Compiling test_gluesql v0.1.0 (C:\Users\ASUS\Desktop\test_gluesql)
    Finished dev [unoptimized + debuginfo] target(s) in 9.94s
```    
