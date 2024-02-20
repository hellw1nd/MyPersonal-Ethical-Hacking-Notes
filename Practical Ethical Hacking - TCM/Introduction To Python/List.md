```python
#Lists - Have brackets []
movies = ["When Harry Met Sally", "The Hangover", "The Perks of Being a Wallflower", "The Exorcist"]

print(movies[1]) #returns the second item in the list - index / indices
print(movies[0]) #returns the first item in the list
print(movies[1:3]) #returns the first number given until right before last number given
print(movies[1:4]) #returns all 
print(movies[1:]) #returns everything from number to end of list
print(movies[:1]) #everything before 1
print(movies[:2])
print(movies[-1]) #grabs last item

print(len(movies)) #counts items in list
movies.append("JAWS")
print(movies) #appends to end of list

movies.insert(2, "Hustle")
print(movies)

movies.pop() #removes last item
print(movies)

movies.pop(0) #removes first item 
print(movies)

amber_movies = ['Just Go With It', '50 First Dates']
our_favorite_movies = movies + amber_movies
print(our_favorite_movies)

grades = [["Bob", 82], ["Alice", 90], ["Jeff", 73]]
bobs_grade = grades[0][1]
print(bobs_grade)
grades[0][1] = 83
print(bobs_grade)
```