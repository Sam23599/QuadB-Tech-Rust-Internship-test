## Solutions for QuadB Tech's Rust Interview

# 1. Palindrome Check

```rust
fn is_palindrome(s: &str) -> bool {
    let mut chars = s.chars().rev();
    for c in s.chars() {
        if c != chars.next().unwrap() {
            return false;
        }
    }
    true
}
```

# 2. First Occurrence of a Number in Sorted Array

```rust
fn first_occurrence(arr: &[i32], target: i32) -> Option<usize> {
    arr.iter().position(|&x| x == target)
}

```

# 3. Shortest Word in a String

```rust
fn shortest_word(s: &str) -> &str {
    let mut words = s.split_whitespace();
    let mut shortest = words.next().unwrap_or("");
    for word in words {
        if word.len() < shortest.len() {
            shortest = word;
        }
    }
    shortest
}
```

# 4. Prime check

```rust
fn is_prime(n: u64) -> bool {
    if n < 2 {
        return false;
    }
    for i in 2..=(n as f64).sqrt() as u64 {
        if n % i == 0 {
            return false;
        }
    }
    true
}
```

# 5. Median of Sorted Array

```rust
fn median(arr: &[i32]) -> f64 {
    let len = arr.len();
    if len % 2 == 0 {
        let mid = len / 2;
        (arr[mid - 1] + arr[mid]) as f64 / 2.0
    } else {
        arr[len / 2] as f64
    }
}

```

# 6. Longest Common Prefix

```rust
fn longest_common_prefix(strs: Vec<String>) -> String {
    if strs.is_empty() {
        return String::new();
    }
    let mut prefix = strs[0].clone();
    for s in strs.iter().skip(1) {
        while !s.starts_with(&prefix) {
            prefix.pop();
        }
    }
    prefix
}

```

# 7.  kth smallest element in an array 

```rust
fn kth_smallest(arr: &[i32], k: usize) -> Option<i32> {
    let mut sorted = arr.to_vec();
    sorted.sort();
    sorted.get(k - 1).cloned()
}

```

# 8. maximum depth of a BT 

```rust
#[derive(Debug)]
struct TreeNode {
    val: i32,
    left: Option<Box<TreeNode>>,
    right: Option<Box<TreeNode>>,
}

fn max_depth(root: Option<&Box<TreeNode>>) -> i32 {
    match root {
        Some(node) => 1 + max(max_depth(node.left.as_ref()), max_depth(node.right.as_ref())),
        None => 0,
    }
}

fn max(a: i32, b: i32) -> i32 {
    if a > b { a } else { b }
}

```

# 9. String Reversal

```rust
fn reverse_string(s: &str) -> String {
    s.chars().rev().collect::<String>()
}

```

# 11. Merge Two Sorted Arrays

```rust
fn merge_sorted_arrays(arr1: &[i32], arr2: &[i32]) -> Vec<i32> {
    let mut merged = Vec::with_capacity(arr1.len() + arr2.len());
    let mut i = 0;
    let mut j = 0;
    while i < arr1.len() && j < arr2.len() {
        if arr1[i] < arr2[j] {
            merged.push(arr1[i]);
            i += 1;
        } else {
            merged.push(arr2[j]);
            j += 1;
        }
    }
    merged.extend_from_slice(&arr1[i..]);
    merged.extend_from_slice(&arr2[j..]);
    merged
}

```

# 12. Maximum Subarray Sum 

```rust
fn max_subarray_sum(arr: &[i32]) -> i32 {
    let mut max_sum = 0;
    let mut current_sum = 0;
    for &num in arr {
        current_sum = num.max(current_sum + num);
        max_sum = max_sum.max(current_sum);
    }
    max_sum
}

```