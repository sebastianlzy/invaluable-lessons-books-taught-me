## Reducing cost with duck typing

Objective of OOP is to reduce the cost of change.

1. Defined public interfaces
2. Messages being the design center of application

### Understanding Duck Typing
Duck types are public interfaces that are not tied to any specific class. They provide flexibility to application by replacing costly dependencies on class with more forgiving dependencies. They are more defined by their behavior than by their class

#### Example without ducktype

```ruby
class Trip
  attr_reader: :bicycles, :customers, :vehicle
  
  def prepare(preparers)
    preparers.each {|preparer|
      case preparer
      when mechanics
        preparer.prepare_bicycle
      when driver
        preparer.gas_up
		  ...
	  end	
    }
  end
end	
```

#### Problems

1. The design is constrained by class, objects do not understand the message being sent
2. Every arguments is of a different class and implement different methods
3. The `prepare` method has too much context on its dependency. It needed to know the excat method for each classes
4. A second developer would add a new `when` branch for a new trip preparer
5. Adding of additional `case` statement to switch class will cause an explosion of dependencies 

#### Potential Solutions

1. Think of if from the `prepare` point of view, it wanted all preparer to prepare themselves
2. All `preparers` should have a `prepare_trip` method.
3. `prepare` can now accept any new `preparer` without making any change

``` ruby
class Driver
  def prepare_trip
    ...
  end
```

### Consequences of duck typing
