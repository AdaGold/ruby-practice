# Comprehension Practice 2: Advanced Methods
This practice worksheet covers more advanced methods than the first practice. In particular, code snippets in these practice problems have methods which may include:
* Multiple parameters
* Collection parameters (`Array` or `Hash`)
* Loop constructs (e.g. `each` and `times`)
* Enumerable methods (e.g. `map` and `reduce`)

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
1. Each problem is intended to be more challenging to read and comprehend than the previous ones.

## Practice Problems
### Problem 1
#### Code Snippet
```ruby
def problem1(values)
  best = values.first
  values.each do |val|
    if best < val
      best = val
    end
  end

  best
end
```

#### Input Values
* `3`
* `"hello"`
* `[3]`
* `[5, 2, 3, 6, -10, 0]`
* `"hello".chars`
* `{ a: 1, b: 2, c: 3 }`

### Problem 2
#### Code Snippet
```ruby
def problem2(values)
  best = values.first
  values.each { |val| best = val if best > val }
  best
end
```

#### Input Values
* `[3]`
* `[5, 2, 3, 6, -10, 0]`
* `"hello".chars`
* `{ a: 1, b: 2, c: 3 }`

#### Bonus questions
Consider the first two problems' code snippets. How are they similar, and how are they different? Are there any built-in Ruby methods that could do the same work for us?

### Problem 3
#### Code Snippet
```ruby
def problem3(values)
  other_values = []
  values.each.with_index { |val, i| other_values << val if i.even? }

  other_values.reduce(&:+)
end
```

#### Input Values
* `[3]`
* `[5, 2, 3, 6, -10, 0]`
* `"hello".chars`

### Problem 4
#### Code Snippet
```ruby
BIG_THRESHOLD = 5

def problem4(values)
  big_values = []
  small_values = []
  values.each do |val|
    array = val > BIG_THRESHOLD
              ? big_values
              : small_values

    array << val
  end

  differences = []
  big_values.zip(small_values).each do |big, small|
    differences << big - (small || 0)
  end

  differences
end
```

#### Input Values
* `[5, 2, 6, 3, 9, -10, 100, 11]`
* `[1, 3, 5, 7, 9, 11, 13]`
* `[0, 2, 4, 6]`

### Problem 5
**NOTE**: For this problem, the code snippet defines a method and calls it three times. The input values listed in the section beneath the snippet are what would replace the `INPUT` part of the code snippet. This means that the `some_array` variable is initialized with the value listed in the "Input Values" section and then passed to the method `problem5` three times.

Rather than the expected return value from this method, instead you should figure out what the expected value of `some_array` is after the last method call. To keep with the iterative process outlined in the instructions above, you should start by predicting the value of `some_array` after only the _first_ call to `problem5` then compare the actual results with your expectation. With that new information, write down your expectation of `some_array`'s value after the second call to `problem5`, and repeat the process for the third call as well.

#### Code Snippet
```ruby
KEY = "pie"

def problem5(values)
  if values.include? KEY
    values << (values.first + values.last)
    values.shift
  end
end

some_array = INPUT

problem5(some_array)
problem5(some_array)
problem5(some_array)
```

#### Input Values
* `["turkey", "yams", "pie", "cranberry sauce", "green beans", "stuffing"]`
* `["veggie burgers", "pie", "hot dogs", "potato chips", "potato salad"]`
* `["pie"]`

### Problem 6
#### Code Snippet
```ruby
SALES = [
  { provider: "Asha",     service: "Touchup and Cut",    price:  40.00 },
  { provider: "Asha",     service: "Shampoo",            price:  15.00 },
  { provider: "Rosalind", service: "Partial Highlight",  price: 110.00 },
  { provider: "Sunny",    service: "Pravana Smoothing",  price: 235.00 },
  { provider: "Rosalind", service: "Full Foil",          price: 140.00 },
  { provider: "Marzanna", service: "Blowout",            price:  50.00 },
  { provider: "Ndidi",    service: "Women's Haircut",    price:  70.00 },
  { provider: "Rosalind", service: "Balayage Highlight", price: 155.00 },
  { provider: "Sunny",    service: "Pravana Smoothing",  price: 235.00 },
  { provider: "Marzanna", service: "Blowout",            price:  50.00 },
]

def problem6(provider)
  provider_sales = SALES.select do |sale|
    sale[:provider] == provider
  end

  prices = provider_sales.map do |sale|
    sale[:price]
  end

  prices.sum
end
```

#### Input Values
* `"Asha"`
* `"Rosalind"`
* `"Debora"`

### Problem 7
#### Code Snippet
```ruby
VIDEO_PLAYS = [
  { user_id: 57579013, video_id: "H8n-Z41b1", play_time: 288.1 },
  { user_id: 38328560, video_id: "kO1v3BMDx", play_time: 202.0 },
  { user_id:  3961384, video_id: "H8n-Z41b1", play_time: 144.8 },
  { user_id: 22877914, video_id: "kO1v3BMDx", play_time: 202.0 },
  { user_id: 80081492, video_id: "_v99zAYUz", play_time:  71.7 },
  { user_id:   593326, video_id: "H8n-Z41b1", play_time:   4.4 },
  { user_id: 22877914, video_id: "H8n-Z41b1", play_time: 129.9 },
  { user_id: 80081492, video_id: "kO1v3BMDx", play_time: 202.0 },
  { user_id: 80081492, video_id: "H8n-Z41b1", play_time: 170.6 },
  { user_id:  3961384, video_id: "_v99zAYUz", play_time:  67.1 },
  { user_id: 22877914, video_id: "_v99zAYUz", play_time:  55.9 },
  { user_id: 57579013, video_id: "_v99zAYUz", play_time:  66.8 },
  { user_id: 22877914, video_id: "H8n-Z41b1", play_time: 109.3 },
]

PLAY_TIME_THRESHOLD = 0.3 # 30%

def problem7(video_id, video_length)
  min_play_time = video_length * PLAY_TIME_THRESHOLD
  VIDEO_PLAYS.select do |play|
    play[:video_id] == video_id &&
    play[:play_time] >= min_play_time
  end.count
end
```

#### Input Values
**NOTE**: For this and following problems we use a different convention for the input values. Instead of writing the value that should be provided as the sole parameter to the method, we write the full invocation of that method because there are multiple parameters.

* `problem7("H8n-Z41b1", 301.1)`
* `problem7("_v99zAYUz",  72.8)`
* `problem7("m_-6Y6df6", 474.0)`

### Problem 8
#### Code Snippet
```ruby
VEHICLE_INFO = {
  coupe: {
    seats: 2,
    fwd: false
  },
  sedan: {
    seats: 4,
    fwd: false
  },
  minivan: {
    seats: 6,
    fwd: false
  },
  truck: {
    seats: 2,
    fwd: true
  }
}

def problem8(cars_db, seats_required, fwd_required=false)
  cars_db.values.map do |inventory|
    inventory.select do |type, _|
      info = VEHICLE_INFO[type]
      info[:seats] >= seats_required && (!fwd_required || info[:fwd])
    end.values
  end.flatten.sum
end
```

#### Input Values
* 
  ```
  CARS_DB = {
    alamo: {
      coupe: 5, sedan: 6, minivan: 4, truck: 0
    },
    budget: {
      coupe: 0, sedan: 14, minivan: 1, truck: 1
    },
    enterprise: {
      coupe: 6, sedan: 8, minivan: 0, truck: 9
    },
    hertz: {
      coupe: 7, sedan: 10, minivan: 2, truck: 4
    },
  }

  problem8(CARS_DB, 4)
  ```
* 
  ```
  CARS_DB = {
    alamo: {
      coupe: 1, sedan: 3, minivan: 10, truck: 1
    },
    budget: {
      coupe: 1, sedan: 4, minivan: 1, truck: 3
    },
    enterprise: {
      coupe: 6, sedan: 6, minivan: 4, truck: 8
    },
  }

  problem8(CARS_DB, 2, true)
  ```
