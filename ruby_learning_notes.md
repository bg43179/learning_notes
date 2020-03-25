# Ruby Learning notes

## Convention

  - snake case for variable
  - Most of time when a method end with `!`, it means the Object which calls the method will be changed<br/>

	`h1.merge(h2)` -> Create new object in the heap<br/>
	`h1.merge!(h2)` -> Update h1

  - `module` represents the file-hierarchy `ContactInfo::Email`, can fine `email.rb` in `contact_info` directory

## Proc
## Block

```ruby
  # multi-line block
  [1,2,3].map do |num|
    puts num
  end

  # one-line block
  [1,2,3].map { |num| puts number }
```

### `yield`

```ruby
def map(array)
  temp_array = []

  for item in array # step 1: item(1)

    # step 2: yield send item(1) to block as number && step 4: get number*2(1*2 = 2), assign to element
    element = yield(item)
    temp_array.push element
  end

  temp_array # [2]
end

map([1, 2, 3]) do |number|
  number * 2 #step 3: execute and return the last line
end

# output
2
4
6
```
`yield` returns the last evaluated expression.<br/>
In order to use value returned, need to assign it to varable, such as `value = yield(...)`

## Methods
### `map`
```ruby
  [1,2,3].map { |num| num.to_s }

  [1,2,3].map(&:to_s)
```

## Class

### variable
- **instance_var** == **instance method in Java**<br/>
Oject needs to be created to call the method<br/>
Use `@` sign

- **class_var** == static method in Java<br/>
Use `self`.

```ruby
class Person
  def instance_var
    @instance_var = "instance variable"
  end

  def self.class_var
    @@class_var = "class varialbe"
  end

  def say_hi
    "Hi I am #{@instance_var}"
  end

  def self.say_hi
    "Hi I am #{@class_var}"
  end
end

bob = Person.new
bob.say_hi # => Hi I am instance variable
Person.say_hi # => Hi I am class variable
```
## class_eval vs module_eval
