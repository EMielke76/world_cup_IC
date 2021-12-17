
# Boat Rental

## Setup

* Fork this Repository
* Clone YOUR fork
* Compete the activity below
* Push your solution to your fork
* Submit a pull request from your repository to the turingschool-examples repository
  * Make sure to put your name in your PR!

# Activity

## Iteration 1

Use TDD to create a `Boat` and a `Renter` class that respond to the following interaction pattern:

```ruby
pry(main)> require './lib/boat'
# => true

pry(main)> require './lib/renter'
# => true

pry(main)> kayak = Boat.new(:kayak, 20)    
# => #<Boat:0x00007fceac8f0480...>

pry(main)> kayak.type
# => :kayak

pry(main)> kayak.price_per_hour
# => 20

pry(main)> kayak.hours_rented
# => 0

pry(main)> kayak.add_hour

pry(main)> kayak.add_hour

pry(main)> kayak.add_hour

pry(main)> kayak.hours_rented
# => 3

pry(main)> renter = Renter.new("Patrick Star", "4242424242424242")    
# => #<Renter:0x00007fb5ef98b118...>

pry(main)> renter.name
# => "Patrick Star"

pry(main)> renter.credit_card_number
# => "4242424242424242"
```

## Iteration 2

Use TDD to create a `Dock` class. It should have the following methods:

* `rent` - this method takes a `Boat` and a `Renter` as arguments. Calling this method signifies that the `Boat` has been rented by the `Renter`.
* `rental_log` - this method returns a hash that associates a `Boat` with the `Renter` that rented it.

```ruby
pry(main)> require './lib/dock'
# => true

pry(main)> require './lib/renter'
# => true

pry(main)> require './lib/boat'
# => true

pry(main)> dock = Dock.new("The Rowing Dock", 3)    
# => #<Dock:0x00007fdeedb0a788...>

pry(main)> dock.name
# => "The Rowing Dock"

pry(main)> dock.max_rental_time
# => 3

pry(main)> kayak_1 = Boat.new(:kayak, 20)
# => #<Boat:0x00007fdeedb3a528...>

pry(main)> kayak_2 = Boat.new(:kayak, 20)    
# => #<Boat:0x00007fdeedae1860...>

pry(main)> sup_1 = Boat.new(:standup_paddle_board, 15)
# => #<Boat:0x00007fdeedaa8bc8...>

pry(main)> patrick = Renter.new("Patrick Star", "4242424242424242")    
# => #<Renter:0x00007fdeed0ab828...>

pry(main)> eugene = Renter.new("Eugene Crabs", "1313131313131313")    
# => #<Renter:0x00007fdeed8ce5c8...>

pry(main)> dock.rent(kayak_1, patrick)    

pry(main)> dock.rent(kayak_2, patrick)    

pry(main)> dock.rent(sup_1, eugene)    

pry(main)> dock.rental_log
# =>
# {
#   #<Boat:0x00007fdeedb3a528...> => #<Renter:0x00007fdeed0ab828...>,
#   #<Boat:0x00007fdeedae1860...> => #<Renter:0x00007fdeed0ab828...>,
#   #<Boat:0x00007fdeedaa8bc8...> => #<Renter:0x00007fdeed8ce5c8...>
# }
```

## Iteration 3

Use TDD to implement a `Dock#charge` method:

* This method takes a `Boat` as an argument
* This method returns a hash with two key/value pairs:
  * The key `:card_number` points to the credit card number of the `Renter` that rented the boat
  * The key `:amount` points to the amount that should be charged. The amount is calculated by multiplying the Boat's price_per_hour by the number of hours it was rented. However, any hours past the Dock's max_rental_time should not be counted. So if a Boat is rented for 4 hours, and the max_rental_time is 3, the charge should only be for 3 hours.

The `Dock` class should respond to the following interaction pattern:

```ruby
pry(main)> require './lib/dock'
# => true

pry(main)> require './lib/renter'
# => true

pry(main)> require './lib/boat'
# => true

pry(main)> dock = Dock.new("The Rowing Dock", 3)    
# => #<Dock:0x00007fe2f71f4730...>

pry(main)> kayak_1 = Boat.new(:kayak, 20)
# => #<Boat:0x00007fe2f8074c38...>

pry(main)> kayak_2 = Boat.new(:kayak, 20)    
# => #<Boat:0x00007fe2f70e3e68...>

pry(main)> sup_1 = Boat.new(:standup_paddle_board, 15)    
# => #<Boat:0x00007fe2f80a6ee0...>

pry(main)> patrick = Renter.new("Patrick Star", "4242424242424242")    
# => #<Renter:0x00007fe2f787d700...>

pry(main)> eugene = Renter.new("Eugene Crabs", "1313131313131313")    
# => #<Renter:0x00007fe2f7829c68...>

pry(main)> dock.rent(kayak_1, patrick)

pry(main)> dock.rent(kayak_2, patrick)    

pry(main)> dock.rent(sup_1, eugene)    

pry(main)> kayak_1.add_hour

pry(main)> kayak_1.add_hour

pry(main)> dock.charge(kayak_1)
# =>
# {
#   :card_number => "4242424242424242",
#   :amount => 40
# }

pry(main)> sup_1.add_hour

pry(main)> sup_1.add_hour

pry(main)> sup_1.add_hour

# Any hours past the max rental time should not count
pry(main)> sup_1.add_hour

pry(main)> sup_1.add_hour

pry(main)> dock.charge(sup_1)
# =>
# {
#   :card_number => "1313131313131313",
#   :amount => 45
# }
```

## Iteration 4

Use TDD to update your `Dock` class with the following methods:

* `return` - This method takes a `Boat` object as an argument. When this method is called, it signifies that a boat has been returned and is no longer being rented.
* `log_hour` - This method takes no arguments. When it is called, all boats that are currently rented have been rented an additional hour.
* `revenue` - This method takes no arguments. It returns the total revenue generated by charging all boats that have been rented and returned. A charge for a boat follows the same rules as iteration 3.

The `Dock` class should now respond to the following interaction pattern:

```ruby
pry(main)> require './lib/renter'

pry(main)> require './lib/boat'

pry(main)> require './lib/dock'

pry(main)> dock = Dock.new("The Rowing Dock", 3)

pry(main)> kayak_1 = Boat.new(:kayak, 20)

pry(main)> kayak_2 = Boat.new(:kayak, 20)    

pry(main)> canoe = Boat.new(:canoe, 25)    

pry(main)> sup_1 = Boat.new(:standup_paddle_board, 15)    

pry(main)> sup_2 = Boat.new(:standup_paddle_board, 15)    

pry(main)> patrick = Renter.new("Patrick Star", "4242424242424242")

pry(main)> eugene = Renter.new("Eugene Crabs", "1313131313131313")    

# Rent Boats out to first Renter
pry(main)> dock.rent(kayak_1, patrick)

pry(main)> dock.rent(kayak_2, patrick)

# kayak_1 and kayak_2 are rented an additional hour
pry(main)> dock.log_hour

pry(main)> dock.rent(canoe, patrick)

# kayak_1, kayak_2, and canoe are rented an additional hour
pry(main)> dock.log_hour

# Revenue should not be generated until boats are returned
pry(main)> dock.revenue
# => 0

pry(main)> dock.return(kayak_1)

pry(main)> dock.return(kayak_2)

pry(main)> dock.return(canoe)

# Revenue thus far
pry(main)> dock.revenue
# => 105

# Rent Boats out to a second Renter
pry(main)> dock.rent(sup_1, eugene)

pry(main)> dock.rent(sup_2, eugene)

pry(main)> dock.log_hour

pry(main)> dock.log_hour

pry(main)> dock.log_hour

# Any hours rented past the max rental time don't factor into revenue
pry(main)> dock.log_hour

pry(main)> dock.log_hour

pry(main)> dock.return(sup_1)

pry(main)> dock.return(sup_2)

# Total revenue
pry(main)> dock.revenue
# => 195
```
