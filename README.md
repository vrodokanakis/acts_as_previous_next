# ActsAsPreviousNext

## Description

This `acts_as` extension provides the capability for having previous & next methods for an object.
Previous & next are based on a specified column (default is id).

## Install

In your Gemfile

  `gem 'acts_as_previous_next'`

Currently is tested on rails3.2, ruby 1.9.3 and mysql

## Example
```
  class Post < ActiveRecord::Base
    acts_as_previous_next
    # acts_as_previous_next column: :id
    # or
    # acts_as_previous_next :id
  end

  post = Post.new
  post.next # => nil
  post.save
  post.next # => post
  post.previous # => post
  another_post = Post.new
  another_post.save
  another_post.next # => post
  another_post.previous # => post
```
Currently CanCan authorization is supported as option (`false` by default). If cancan authorization is
enabled then `current_ability` must be passed to next, previous methods. So the previous example
with cancan will be:
```
  class Post < ActiveRecord::Base
    acts_as_previous_next with_cancan: true

    belongs_to :user
  end
```
And in your view:
```
  link_to 'Next', @post.next(current_ability)
  link_to 'Previous', @post.previous(current_ability)
```
## License

MIT License

