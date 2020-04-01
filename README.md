# Rails Review

For each of the following topics, please answer each of the questions. You can use links and images to support your answer. Once done please make a pull request.

## Has many Through

- [Rails Active Record Intro](https://github.com/sei-entropy/lesson-w11d02-rails-active-record#active-record-associations) -[Hospital App](https://github.com/sei-entropy/hw-w11d02-rails-hospital)

### Questions

1. What is the role of a join table in a many-to-many relationship?

   Its purpose is to store a record for each of the combinations of these other two tables. It might seem like a bit of work to create, but it’s simple to do and provides a much better data structure.

2. What two columns must be present in a join table?

   It stores two columns:one for each of the primary keys from the other table.

3) Given the example below, edit the code to define a has many :through relationship.

   ```ruby
   class Customer < ActiveRecord::Base
   has_many :Product
   has_many :Product, :through => :Purchase
   end

   class Product < ActiveRecord::Base

   has_many :Customer
   has_many :Purchase, :through => :Customer

   end

   class Purchase < ActiveRecord::Base
   belongs_to :Product
   belongs_to :Customer
   end
   ```

4. Based on #3, give an example of associating two instances via the join model.
   Purchases.create(customer: Rawan , product: T-shirt)

## Devise

- [Devise Lesson](https://github.com/sei-entropy/lesson-w11d03-rails-devise)

### Questions

1. What does the `current_user` method that the Devise gem provides?

   is a helper method that is used to return objects that are specific to that user

2) What does the `authenticate_user!` method that the Devise gem provides?

   is a helper method that restricts users from specified controller actions.

3. Write a signout link using the `link_to` rails helper and a devise path.

   <%= link_to "Sign Out", destroy_user_session(current_user)%>

4. How do I generate a devise model in the terminal?

   rails g devise user

5) What are the trade offs for using a gem for authentication over a handrolled solution? (no real right answer)

   It is faster than writing your own code

## Validations

- [Validations Lesson](https://github.com/sei-entropy/lesson-w11d03-rails-model-validations)

### Questions

1. Which component, of Rails MVC, is responsible for the business logic?

   Model

2. Assume the user's age is an optional field. Write the validation to verify that a User's age is between 13 and 125 (inclusive).

   validates :age, inclusion: {in: %w(13..125) }

3) What would `user.errors.messages` return (for the above User), if you assigned `user.age = 12`?

"is not included in the list".

4. Assume you visit "/customers/new" and enter some invalid information. Given this controller code, what url would your browser be on after pressing "Create Customer"?

   new_customer_path

```ruby
class CustomersController < ApplicationController
  def new
    @customer = Customer.new
  end

  def create
    @customer = Customer.new(customer_params)
    if @customer.save
      redirect_to customer_path(@customer)
    else
      render :new
    end
  end
  ...
  private
  def customer_params
    params.require(:customer).permit(:first_name, :last_name, :age)
  end
end
```

5. Give one reason why we might have the similar validations in the browser, model, and database layer of our application.

   I think it great for security and similar validations are for the ease of the programmer , Maybe
