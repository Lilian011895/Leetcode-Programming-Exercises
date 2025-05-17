# Leetcode-Programming-Exercises

## 6. ZigZag Conversion

### 解題思路
這題要求將字串按照Z字形模式重新排列，然後按行讀取。我使用了一個方向變量來控制字符添加的方向，當到達最上方或最下方時改變方向。

### Rust程式碼
```rust
impl Solution {
    pub fn convert(s: String, num_rows: i32) -> String {
        // 如果只有一行或字串為空，直接返回原字串
        if num_rows == 1 || s.len() <= 1 {
            return s;
        }
        
        // 為每一行創建一個字串
        let mut rows: Vec<String> = vec![String::new(); num_rows as usize];
        
        // 當前行和移動方向
        let mut current_row = 0;
        let mut direction = 1; // 1表示向下，-1表示向上
        
        // 遍歷每個字符並放到相應的行
        for c in s.chars() {
            rows[current_row as usize].push(c);
            
            // 檢查是否需要改變方向
            if current_row + direction < 0 || current_row + direction >= num_rows {
                direction = -direction; // 改變方向
            }
            
            // 更新當前行
            current_row += direction;
        }
        
        // 合併所有行並返回結果
        rows.concat()
    }
}
