# Active Record Learning Notes

## includes
  - [Read](https://engineering.gusto.com/a-visual-guide-to-using-includes-in-rails/)
### How to use includes
  - Join

    ```ruby
    Users.includes(:contanct_info)`
    ```

  - Apply where condition to associated models. The `references` is required to access associated models

    ```ruby
    Users.includes(:contanct_info)
    .where("contact_infos.city = 'San Diego'")
    .references(:contanct_info)
    ```

  - Nested Join

    ```ruby
    User.includes(contact_info: [:email])
    ```

### preload v.s eager_load

- Default using `preload`, which will load leading model and associated model based on the foreign key

  `Users.includes(:contanct_info)` will load **all users** and **contanct_infos which has foreign key in users**

  ```ruby
  SELECT users.* FROM users
  SELECT contact_infos.* FROM contact_infos WHERE contact_infos.id IN (1, 2, 3)
  ```

- When using `includes` with `where` or `references`, it will use `eager_load` and load both **whole users and contanct_infos** instead. `eager_load` use **Left Join**

  ```ruby
  Users.includes(:contanct_info)
  .where("contact_infos.city = 'San Diego'")
  .references(:contanct_info)
  ```

- The data shows that using `:includes` will improve the performance significantly when a `:preload` is invoked, but has the opposite effect for `:eager_load` in most cases

***
## Query Optimization

### Why using `size` instead of `count`

- `count` on an ActiveRecord relation will always try to execute a SQL query
- `size` checks the length of ActiveRecord without making any SQL query

  **Only call COUNT when ActiveRecord is not loaded.**<br/>
  Change the order and replace count with size to make sure ActiveRecord is loaded beforehand

- Use `load` to load directly (no lazy loading)<br/>
  `ActiveRecord::QueryCache` only happen when a query is called twice

### When to use `where` and when not??**

- Don’t call `scopes` on associations when you’re rendering collections

- Don’t put query methods, like `where`, in instance methods of an `ActiveRecord::Base` class.

- `includes` + `scopes` (and other preloading + association) is a way to reduce the cost of `where`

- `includes` use a concept called "Eager loading", Eager loading works by preloading every comment for every article beforehand in a temporary cache stored in memory

- When an Active Record associated is called, the association method will first try to pull the requested association data out of the `@association_cache` instance variable assuming it has already been loaded into memory.

  [Three Active Record Mistake](https://www.speedshop.co/2019/01/10/three-activerecord-mistakes.html)

  [What’s N+1 query](https://medium.com/@bretdoucette/n-1-queries-and-how-to-avoid-them-a12f02345be5)

  [Preload scope to avoid make N+1 queries](https://www.justinweiss.com/articles/how-to-preload-rails-scopes/)

### When to use present, when not??

- `present?` actually call `!blank?`<br/>
  Emptiness like `[] {} “”` then present is useful

  ```ruby
  [27] pry(main)> !![]
  => true
  [28] pry(main)> [].present?
  => false

  Otherwise,

  [33] pry(main)> !!0
  => true
  [34] pry(main)> 0.present?
  => true
  [35] pry(main)> !!nil
  => false
  [36] pry(main)> nil.present?
  => false
  ```

**Practice**
How many query do these two actually call??

- if `@comments.any?`
  h2 Comments on this Post
  - @comments.each do |comment|

- unless @comments.load.empty?
  h2 Comments on this Post
  - @comments.each do |comment|

***

## find_each v.s all.each
- `find_each` use batch load which is good for memory while dealing with great amounts of data
