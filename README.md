# Traveling_Salesman_Problem
This is a python code segment I created to solve a csv version of the "traveling salesman problem": provided a list of distances between different cities, what is the optimal path a salesman could travel while reaching all cities and returning to the original city (In terms of mileage)?

Instead of taking the time to learn the statistical backbone of this problem and the actual optimized solution, my code goes for a "good enough solution": provided a starting point, go to the city with the least distance between your starting point and the city, and once it reaches that city, repeat the process until there are no more "paths" to take.

The code is contingent on the file you provide being a csv file formatted like so: 
 ![Capture](https://user-images.githubusercontent.com/78769272/111252904-c127b580-85d7-11eb-818d-d8ed1cd96979.PNG) (Where the letters are different cities, Ex. the distance from city E to I is 147 miles). 
 
The size of the file/list of distances can be any, however the code will not work if two distances are the same between different cities (Ex if J to I is 278 and K to O is 278). The best workaround I found is to simply offset the distances by a small amount and modify the code to support float values instead of integers.

The code operates on an IDLE Shell (for python 3.9.2 64-bit for Windows) in case you wanted to take a look at it, modify it, etc.
