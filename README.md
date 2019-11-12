# Nested Data Structures

## Learning Goals
+ Explain why nested data structures are useful
+ Use bracket notation to access data in a nested structure
+ Use some basic Ruby methods to answer questions about a given list of data

## Lesson

<iframe width="100%" height="720" src="https://www.youtube.com/embed/VdJqevchJQs?rel=0&showinfo=0" frameborder="0" allowfullscreen></iframe>

+ Hi folks, it's Ian from Flatiron School. In this video, we're going to look at navigated nested data structures. By the end of this video, you should be able to:
  + Explain why nested data structures are useful.
  + Use bracket notation to access data in a nested structure.
  + Use some basic ruby methods to answer questions about a given list of data.
+ So let's get started. As I mentioned, in this video we're going to explore a deeply nested data structure. To do this, we're going to use some data that I pulled from an API. API stands for Application Programming Interface.
+ This basically just means that if I have an application, say Twitter for example, I might build a way for users to interact with the data of my app, but I might also have a way for other programs to interact with my app.
+ Usually, that means that, hey, if you visit a certain URL, we'll give you a nested data structure back of the data that you want.
+ So, for example, if we visit twitter.com/api/tweets, that might give us essentially a big hash of information back. There's a bit more to it than that, but we don't need to go over that for right now. For right now, it's enough to just know that APIs can give us back data that we might want.
+ So in this `app.rb` file, I have some data that I pulled from an API called the Star Wars API. I've already translated it into a hash so that we can look at it, but as you can see, it's pretty tough to read as a human.
+ Luckily, we're programmers, so we can use code to kind of navigate our way through this structure.
+ I'm going to use a gem called `pry`. Pry let's us pause our program mid-run, and gives us access to all the local variables or methods currently in scope.
+ To use it, I'll `gem install pry`, and then at the top of my file here, I can `require 'pry'`
+ Now, I can pause my program by using `binding.pry` anywhere in the code, and we'll stop there.
+ When I run this now, I can look at `star_wars_data` and see that it's this giant hash.
+ So let's start exploring. The first thing I want to is see - what are the top level keys of this hash? I can do that using a method called `keys`.
```ruby
star_wars_data.keys #=> ["count", "next", "previous", "results"]
```
+ Great - I can see that there are actually only four top level keys to this data structure - let's check each one out.
```ruby
star_wars_data["count"] #=> 87
```
+ This must represent the total count of characters. Let's check out next and previous:
```ruby
star_wars_data["next"] #=> "https://swapi.co/api/people/?page=2"
star_wars_data["previous"] #=> nil
```
+ This returns to a string of a URL - so this API was setup in such a way that, all the data was split over several URLs worth. That way, you know how many total to expect and how to get the next piece of data.
+ We won't worry too much about that right now, but this is just so you know the types of things you might see at the top level of a data. structure like this, sometimes it's just metadata, or data about the data.
+ So finally, let's look at results.
```ruby
star_wars_data["results"]
```
+ So this we can see is a big old data structure of some sort, and it's kind of hard to look at it to know what it is.
+ I'm just going to ask it by using the `class` method.
```ruby
star_wars_data["results"].class #=> Array
```
+ Awesome, so this thing is an array. Let's check how many items are in it.
```ruby
star_wars_data["results"].length #=> 10
```
+ And now let's look at the first item.
```ruby
star_wars_data[:results].first #=>
{"name"=>"Luke Skywalker",
 "height"=>"172",
 "mass"=>"77",
 "hair_color"=>"blond",
 "skin_color"=>"fair",
 "eye_color"=>"blue",
 "birth_year"=>"19BBY",
 "gender"=>"male",
 "homeworld"=>"https://swapi.co/api/planets/1/",
 "films"=>
  ["https://swapi.co/api/films/2/",
   "https://swapi.co/api/films/6/",
   "https://swapi.co/api/films/3/",
   "https://swapi.co/api/films/1/",
   "https://swapi.co/api/films/7/"],
 "species"=>["https://swapi.co/api/species/1/"],
 "vehicles"=>["https://swapi.co/api/vehicles/14/", "https://swapi.co/api/vehicles/30/"],
 "starships"=>["https://swapi.co/api/starships/12/", "https://swapi.co/api/starships/22/"],
 "created"=>"2014-12-09T13:50:51.644000Z",
 "edited"=>"2014-12-20T21:17:56.891000Z",
 "url"=>"https://swapi.co/api/people/1/"} -->
 ```
+ And then the second item.

```ruby
star_wars_data["results"][1]
=> {"name"=>"C-3PO",
 "height"=>"167",
 "mass"=>"75",
 "hair_color"=>"n/a",
 "skin_color"=>"gold",
 "eye_color"=>"yellow",
 "birth_year"=>"112BBY",
 "gender"=>"n/a",
 "homeworld"=>"https://swapi.co/api/planets/1/",
 "films"=>
  ["https://swapi.co/api/films/2/",
   "https://swapi.co/api/films/5/",
   "https://swapi.co/api/films/4/",
   "https://swapi.co/api/films/6/",
   "https://swapi.co/api/films/3/",
   "https://swapi.co/api/films/1/"],
 "species"=>["https://swapi.co/api/species/2/"],
 "vehicles"=>[],
 "starships"=>[],
 "created"=>"2014-12-10T15:10:51.357000Z",
 "edited"=>"2014-12-20T21:17:50.309000Z",
 "url"=>"https://swapi.co/api/people/2/"}
 ```
 + Looking at it - I can tell that each of these is a hash. Using `.class` confirms it.
+ Cool, so we can see that we're following a similar format here. How would you describe each of these?
+ Looking at this, I'd say that each one of these represents a single character. Each character has a name, height, hair_color, and so on.
+ Knowing this, we can write a few methods.
+ Feel free to pause the video to think about how you might do this.
+ First, let's make a method called `print_names` that takes in our data prints out all of the characters name.

```ruby
def print_names(data)
end
# This method should print all of the names of the characters
```
+ Given our initial hash, we can break this down into a couple of steps:
  + Get the array of characters.
  + Iterate over each character.
  + Print the name of that character.
```ruby
def print_names(data)
  # Get the array of characters
  # Iterate over each character
  # print the name of that character
end
# This method should print all of the names of the characters
```
+ First, throw a pry in this method so we can kind of play around with it when it's called.
```ruby
def print_names(data)
  binding.pry
  # Get the array of characters
  # Iterate over each character
  # print the name of that character
end

print_names(star_wars_data)
# This method should print all of the names of the characters
```
+ Great - so the first thing we need is that array of characters. Let's grab that out of the hash from the "results" key.
```ruby
characters = data["results"]
```
+ That seems to work, so I'll copy and paste that line into my method.
```ruby
def print_names(data)
  binding.pry
  # Get the array of characters
  characters = data["results"]
  # Iterate over each character
  # print the name of that character
end

print_names(star_wars_data)
# This method should print all of the names of the characters
```
+ Next, let's iterate over our list of characters using the .each method. So characters.each do and then between the pipes, we'll call this "character".
+ I'm also going to move my pry into the loop so we can see what the character looks like.
```ruby
def print_names(data)
  # Get the array of characters
  characters = data["results"]
  # Iterate over each character
  characters.each do |character|
    binding.pry
  end
  # print the name of that character
end

print_names(star_wars_data)
# This method should print all of the names of the characters
```
+ If I look at the character on the first pass through - I see it's Luke Skywalker. I can go to the next pass of my loop by typing `exit`.
+ Cool, second pass through is C-3PO. Now, I can access the name by doing `character["name"]` So let's do a `puts character["name"]`.
+ And that works well.
+ Now, to get out of my pry, I can type `exit!` and that will stop my loop completely since I feel confident about what we have now.
```ruby
def print_names(data)
  # Get the array of characters
  characters = data["results"]
  # Iterate over each character
  characters.each do |character|
    # print the name of that character
    puts character["name"]
  end
end

print_names(star_wars_data)
# This method should print all of the names of the characters
```
+ And that works really well! So there are a bunch of other methods that we could write using higher lever iterators.
+ Say we wanted to find out how tall a character is, let's write a method to do that.
+ This method should take in the character's name and the data structure, and return thier height.
+ For example, if we call this will "C-3PO", we should get bak 167.
+ One way to do this is to loop over all the character, and find the character whose name matches the name of our character.
+ Once we have the match, return the height for that character.
```ruby
def character_height(name, star_wars_data)
  # get the array of characters
  # iterate over each character
  # if the character name matches the given name
  # return the height for that character
end
# This method should return the height of a character given their name
character_height("C-3PO", star_wars_data) #=> 167
```
+ To start out, let's get the characters out of the data structure and then iterate over it using `.each`.
```ruby
def character_height(name, star_wars_data)
  # get the array of characters
  characters = data["results"]
  # iterate over each character
  characters.each do |character|
  # if the character name matches the given name
  # return the height for that character
  end
end
```
+ Now, if the character name matches the name provided, we'll look up the height. We can then use the `return` keyword to end our loop early.
```ruby
def character_height(name, star_wars_data)
  # get the array of characters
  characters = data["results"]
  # iterate over each character
  characters.each do |character|
  # if the character name matches the given name
  if character["name"] == name
    # return the height for that character
    return character["height"]
  end
  end
end
```
+ And now we see that this works great. Now, we're sort of doing these two steps in one loop here - that is, we're finding the character and then immediately returning the height. We can use a higher level iterator for this to separate that out. I'm going to go back to my original psuedo code and re-word it slightly.
+ I'm going to be a bit more abstract and just say we should "find the character with the given name".
```ruby
def character_height(name, star_wars_data)
  # get the array of characters
  # find the character with the given name
  # return the height for that character
end
# This method should return the height of a character given their name
character_height("C-3PO", star_wars_data) #=> 167
```
+ For this, we can use the Ruby iterator "find". When we call find on an array and give it a block, it will return the first item that makes the block true. So I can pass it a true/false statement like `character["name"] == "C-3PO" or character["birth_year"] == 1901` or something.
+ In this case, the true/false statement is - does the character's name equal the given name from the method?
```ruby
def character_height(name, star_wars_data)
  # get the array of characters
  characters = data["results"]
  # find the character with the given name
  character = characters.find do |character|
    character["name"] == name
  end
  # return the height for that character
  character["height"]
end
# This method should return the height of a character given their name
character_height("C-3PO", star_wars_data) #=> 167
```
+ This way, we can just return the height for the character we found.
+ So there's a bunch of other stuff we can do like this, you can find characters by value, or sort them to find the tallest character or anything like that.
+ We're just at the tip of the iceberg here, but this is a good introduction to using nested data, so I think we'll go ahead and stop here. So just to recap:
  + We talked about why nested data is useful - it lets us write complex interactions with robust, real-life data sources and to process more data than we as humans could.
  + We used bracket notation to access data in our nested structure here with the star wars example, such as the top level keys, plus results on each individual character.
  + And we used some basic ruby methods to answer questions about a given list of data - like each and find. We could do way more complex stuff as well.
+ Thanks so much for watching - happy coding!
