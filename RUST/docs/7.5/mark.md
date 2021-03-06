


### 格式化输出

format!：将格式化文本写到字符串（String）。（译注：字符串是返 回值不是参数。）
print!：与 format! 类似，但将文本输出到控制台（io::stdout）。
println!: 与 print! 类似，但输出结果追加一个换行符。
eprint!：与 format! 类似，但将文本输出到标准错误（io::stderr）。
eprintln!：与 eprint! 类似，但输出结果追加一个换行符。

通常情况下，`{}` 会被任意变量内容所替换。
> 所有 std 库类型都天生可以使用 {:?} 来打印：  

e.g.  index
```rust
println!("{0}, this is {1}. {1}, this is {0}", "Alice", "Bob");
```

e.g. fmt::Display
```rust
use std::fmt::{self, Formatter, Display};

struct City {
    name: &'static str,
    // 纬度
    lat: f32,
    // 经度
    lon: f32,
}

impl Display for City {
    // `f` 是一个缓冲区（buffer），此方法必须将格式化后的字符串写入其中
    fn fmt(&self, f: &mut Formatter) -> fmt::Result {
        let lat_c = if self.lat >= 0.0 { 'N' } else { 'S' };
        let lon_c = if self.lon >= 0.0 { 'E' } else { 'W' };

        // `write!` 和 `format!` 类似，但它会将格式化后的字符串写入
        // 一个缓冲区（即第一个参数f）中。
        write!(f, "{}: {:.3}°{} {:.3}°{}",
               self.name, self.lat.abs(), lat_c, self.lon.abs(), lon_c)
    }
}

```

### 原生类型

1. char（字符）：单个 Unicode 字符，如 'a'，'α' 和 '∞'（每个都是 4 字节）
2. mut 可变变量的类型不能改变
3. 类型声明
```rust
6 |     println!("1 - 2 = {}", 1u32 - 2);
  |                            ^^^^^^^^ attempt to subtract with overflow
```
4. 数组与切片

### 自定义类型
1. 结构体
2. 枚举+use的用法
3. 学习rust 链表写法([基于enum](RUST/Toy_Srcs/List.rs))
### 类型转换
    可以显式转换
    let integer = decimal as u8;
    let character = integer as char;
### 函数
1.  闭包(closure)和捕获（capture）  
    ```rust
    let mut count = 0;
    let mut inc = || {
        count += 1;
        println!("`count`: {}", count);
    };
    // 调用闭包。
    inc();
    inc();
    ```
    得到:  

    ```shell
    `count`: 1
    `count`: 2  
    ```

Fn：表示捕获方式为通过引用（&T）的闭包
FnMut：表示捕获方式为通过可变引用（&mut T）的闭包
FnOnce：表示捕获方式为通过值（T）的闭包

