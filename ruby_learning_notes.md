# Ruby Learning notes

## Convention

  - snake case for variable
  - Most of time when a method end with `!`, it means the Object which calls the method will be changed<br/>

	`h1.merge(h2)` -> Create new object in the heap<br/>
	`h1.merge!(h2)` -> Update h1

  - `module` represents the file-hierarchy `ContactInfo::Email`, can fine `email.rb` in `contact_info` directory
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
