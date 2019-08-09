# Nested Data Structures

## Learning Goals

## Outline

+ We'll talk about how to navigate deeply nested data structures
+ Use data pulled from the Star Wars API
  + API stands for application programming interface - it's a way for code to interact with something in your program
  + Often means giving structured data via a web link instead of HTML
  + Show visiting reddit.com vs reddit.com/.json
  + Visit this link in the browser to show them what the data looks like: https://swapi.co/api/people/.json
  + Use a JSON viewer chrome extension to preview
+ We have a hash loaded into our app file - but it's kind of hard to read
+ The JSON viewer will help us to see how to access
  + Four top level keys
    + Results points to a number - how many total results there are
    + next points to a url - this would be if we needed to get more Data
    + previous points to null, or nothing in this case
    + and results - results points to an array
```ruby
star_wars_data[:results] #=> array
star_wars_data[:results].length #=> 10
```
+ Look at the first item
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
+ And then the second

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

+ So we can see that they are following a similar format here. Knowing this, let's write a few methods.
+ Feel free to pause the video to think about how you might do each of these.

```ruby
def print_names(data)
end
# This method should print all of the names of the characters

def characters_height(name, star_wars_data)
end
# This method should return the height of a character given their name
characters_height("C-3PO", star_wars_data) #=> 167

def hair_color_of_tallest_character(star_wars_data)
end
# this method should return the hair color of the tallest chracter
```

+ Demonstrate how to solve each of these using higher-level iterators 
+ At each step of the way, discuss what the data structure looks like
