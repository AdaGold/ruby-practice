# Comprehension Practice 3: Multiple Methods
This practice worksheet covers the use of multiple methods together to compose a larger program. In addition to practicing comprehension, this worksheet should reinfoce that when writing code comprehension can be made easier by breaking large chunks of code into smaller methods, especially when they are aptly named.

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
Use the following data for all problems in this worksheet:

```ruby
VEHICLE_INFO = {
  coupe: {
    seats: 2,
    fwd: false,
    cargo: :small,
  },
  sedan: {
    seats: 4,
    fwd: false,
    cargo: :small,
  },
  minivan: {
    seats: 6,
    fwd: false,
    cargo: :medium,
  },
  truck: {
    seats: 2,
    fwd: true,
    cargo: :large,
  },
}

CARGO_SIZES = [:none, :small, :medium, :large, :xlarge]

VEHICLE_DB = {
  alamo: {
    coupe: 5, sedan:  6, minivan: 4, truck: 0
  },
  budget: {
    coupe: 0, sedan: 14, minivan: 1, truck: 1
  },
  enterprise: {
    coupe: 6, sedan:  8, minivan: 0, truck: 9
  },
  hertz: {
    coupe: 7, sedan: 10, minivan: 2, truck: 4
  },
}
```

### Problem 1
#### Code Snippet
```ruby
def enough_seats?(type, seats_required)
  VEHICLE_INFO[type][:seats] >= seats_required
end

def has_fwd?(type)
  VEHICLE_INFO[type][:fwd]
end

def matches_search?(type, seats_req, fwd_req)
  enough_seats?(type, seats_req) && (!fwd_req || has_fwd?(type))
end

def vehicles_available(seats_required, fwd_required=false)
  VEHICLE_DB.values.map do |inventory|
    inventory.select do |type, _|
      matches_search?(type, seats_required, fwd_required)
    end.values
  end.flatten.sum
end
```

#### Input Values
* `vehicles_available(3)`
* `vehicles_available(3, true)`

### Problem 2
#### Code Snippet
```ruby
def seats_matches?(type, search)
  VEHICLE_INFO[type][:seats] >= search[:seats_required]
end

def has_fwd?(type)
  VEHICLE_INFO[type][:fwd]
end

def fwd_matches?(type, search)
  !search[:fwd_required] || has_fwd?(type)
end

def cargo_large_enough?(left, right)
  CARGO_SIZES.index(left) >= CARGO_SIZES.index(right)
end

def cargo_matches?(type, search)
  cargo_large_enough?(VEHICLE_INFO[type][:cargo], search[:cargo_min])
end

def matches_search?(type, search)
  seats_matches?(type, search) &&
  fwd_matches?(type, search)   &&
  cargo_matches?(type, search)
end

def vehicles_available(search)
  VEHICLE_DB.values.map do |inventory|
    inventory.select do |type, _|
      matches_search?(type, search)
    end.values
  end.flatten.sum
end
```

#### Input Values
*
  ```ruby
    vehicles_available({
      seats_required: 3,
      fwd_required: false,
      cargo_min: :medium
    })
  ```
*
  ```ruby
    vehicles_available({
      seats_required: 3,
      fwd_required: true,
      cargo_min: :small
    })
  ```

### Problem 3
#### Code Snippet
```ruby
AGENCY_PREFERENCE = [
  :enterprise,
  :alamo,
  :hertz,
  :budget
]

def agency_type_qty(agency, type)
  VEHICLE_DB[agency][type].to_i
end

def agency_has_type?(agency, type)
  agency_type_qty(agency, type) > 0
end

def agencies_to_contact(type, quantity)
  results = {
    qty_left: quantity,
    agencies: []
  }

  results = AGENCY_PREFERENCE.reduce(results) do |results, agency|
    qty_left = results[:qty_left]

    if qty_left > 0 && agency_has_type?(agency, type)
      results[:qty_left] = [0, qty_left - agency_type_qty(agency, type)].max
      results[:agencies] << agency
    end

    results
  end

  if results[:qty_left] > 0
    raise StandardError.new("Could not find sufficient vehicles of type '#{type}'.")
  end

  results[:agencies]
end
```

#### Input Values
* `agencies_to_contact(:sedan, 22)`
* `agencies_to_contact(:truck, 10)`
* `agencies_to_contact(:minivan, 8)`

### Problem 4
#### Code Snippet
```ruby
AGENCY_PREFERENCE = [
  :enterprise,
  :alamo,
  :hertz,
  :budget
]

def agency_type_qty(agency, type)
  VEHICLE_DB[agency][type].to_i
end

def agency_has_type?(agency, type)
  agency_type_qty(agency, type) > 0
end

def agency_quantities(type, quantity)
  agencies = AGENCY_PREFERENCE.reduce({}) do |agencies, agency|
    qty_left = quantity - agencies.values.sum

    if qty_left > 0 && agency_has_type?(agency, type)
      agency_qty = agency_type_qty(agency, type)

      agencies[agency] = [agency_qty, qty_left].min
    end

    agencies
  end

  if agencies.values.sum < quantity
    raise StandardError.new("Could not find sufficient vehicles of type '#{type}'.")
  end

  agencies
end
```

#### Input Values
* `agency_quantities(:coupe, 12)`
* `agency_quantities(:truck, 20)`
* `agency_quantities(:minivan, 3)`
