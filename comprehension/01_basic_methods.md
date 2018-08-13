# Comprehension Practice 1: Basic Methods
## Instructions
For each problem listed below, follow these steps to practice your code reading and comprehension skills:
1. Start by reading the code snippet presented. Try to work out everything that it's doing, on every line. **Write down a short (1-2 sentences) explanation of the code in your native language.**
1. After you feel that you understand the code (or are as close as you can get), look at the provided list of input values. For each value, try to work out what the return value of the method will be for that input. **Write down your expected return values.**
1. Finally, copy the code snippet into IRB and then try calling the method with each input:
    1. Was your expectation of the return value correct?
    1. If not, try to look at the code again and figure out what it's doing differently from how you originally understood it.
    1. If you figure out something knew about the code (i.e. you understand it better now), rewrite your expanation of the code from the first step. Also update any of the expected return values if you now believe they will be different.

### Tips
1. While you should push yourself to predict the correct return value for each of these problems, this is intentionally a challenging exercise. Don't be discouraged if you get something wrong! The instructions above involve re-reading and comprehending the code again after trying each input precisely for this reason. Look at this as an iterative process, each time hopefully getting closer to a full understanding of the code snippet.
1. You CAN use the Internet, any of our lecture resources, or any of your notes. Some of these problems might involve methods that you've not seen in class, so you will need to look them up in the Ruby docs.
1. Some of the input values for a given problem might result in an error rather than a return value. This is intentional.
1. Each problem is intended to be more challenging to read and comprehend than the previous ones. Even though the code isn't always longer, it may be using more sophisticated techniques.

## Practice Problems
### Problem 1
#### Code Snippet
```ruby
def problem1(n)
  n * 2
end
```

#### Input Values
* `3`
* `"hello"`
* `true`
* `:taco`

### Problem 2
#### Code Snippet
```ruby
def problem2(n)
  if n > 10
    -n + 4
  else
    n * 3
  end
end
```

#### Input Values
* `3`
* `10`
* `15`
* `"hello"`

### Problem 3
#### Code Snippet
```ruby
def problem3(n)
  !n
end
```

#### Input Values
* `3`
* `"hello"`
* `true`
* `:taco`

### Problem 4
#### Code Snippet
```ruby
def problem4(n)
  return nil unless n.round <= 5

  (n / 2) > 5
end
```

#### Input Values
* `3`
* `5.25`
* `"hello"`
* `20.6`
* `11` (this one is tricky)

### Problem 5
#### Code Snippet
```ruby
def problem5(n)
  case n
    when Integer
      500 / n
    when String
      n.downcase.sub('l', 'n').sub('o', 'a')
    when Numeric
      n.phase
    else
      !!n
  end
end
```

#### Input Values
* `3`
* `5.25`
* `"Hello"`
* `-0.6`
* `false`
* `[false]`
