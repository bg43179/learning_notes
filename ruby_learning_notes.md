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

### `tap`

  How `tap` is implemented
  ```ruby
  class Object
    def tap
      yield self
      self
    end
  end
  ```

  Yield self to the block. The primary purpose of this method is to “tap into” a method chain. (Act as a temporary pipe)

  ```ruby
  (1..10).tap {|x| puts "original: #{x}" }
    .to_a.tap { |x| puts "array:#{x}" }
    .select {|x| x.even? }.tap {|x| puts "evens: #{x}" }
    .map {|x| x*x }.tap {|x| puts "squares: #{x}" }

  # output
  original: 1..10
  array:[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
  evens: [2, 4, 6, 8, 10]
  squares: [4, 16, 36, 64, 100]
  ```

  It can also be used for creation

  ```ruby
  user = User.new.tap do |u|
    u.firstname = "andrew"
    u.firstname = "chen"
    u.save!
  end
  ```

  Reference: [Ruby: Tap that method](https://medium.com/aviabird/ruby-tap-that-method-90c8a801fd6a), [API Doc](https://apidock.com/ruby/Object/tap)
## Class

### method
- **instance_method** == **instance method in Java**<br/>
Object needs to be created to call the method<br/>
`@instance_variable` is used by instance_method<br/>
Use `@` sign for instance variable<br/>

- **class_method** == static method in Java<br/>
Use `self` for class method<br/>
`@class_variable` is used by class_method<br/>
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

#### 3 ways to create class method  [Reference](http://www.railstips.org/blog/archives/2009/05/11/class-and-instance-methods-in-ruby/)
```ruby
# Way 1
class Foo
  def self.bar
    puts 'class method'
  end
end

# Way 2
class Foo
  class << self
    def bar
      puts 'class method'
    end
  end
end

# Way 3
class Foo; end
def Foo.bar
  puts 'class method'
end
```
Example: 
```ruby
module ActiveRecord
  class Base
    def self.validates_presence_of(...)
      # make sure present
    end
  end
end

class Foo < ActiveRecord::Base
  validates_presence_of :bar
end
```

### instacne_eval vs class_eval vs module_eval [Reference](https://web.stanford.edu/~ouster/cgi-bin/cs142-winter15/classEval.php)
```ruby
# class_eval
MyClass.class_eval do
  def num
    @num
  end
end

# is the same as 

class MyClass
  def num
    @num
  end
end
```


### Code outside of a method: [Reference](https://stackoverflow.com/questions/20414289/code-placed-outside-of-a-method)