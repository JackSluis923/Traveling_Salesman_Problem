# Traveling_Salesman_Problem
This is a python code segment I created to solve a csv version of the "traveling salesman problem": provided a list of distances between different cities, what is the optimal path a salesman could travel while reaching all cities and returning to the original city (In terms of mileage)?

Instead of taking the time to learn the statistical backbone of this problem and the actual optimized solution, my code goes for a "good enough solution": provided a starting point, go to the city with the least distance between your starting point and the city, and once it reaches that city, repeat the process until there are no more "paths" to take.

The code is contingent on the file you provide being a csv file formatted like so: 
 ![Capture](https://user-images.githubusercontent.com/78769272/111252904-c127b580-85d7-11eb-818d-d8ed1cd96979.PNG) (Where the letters are different cities, Ex. the distance from city E to I is 147 miles). 
 
The size of the file/list of distances can be any, however the code will not work if two distances are the same between different cities (Ex if J to I is 278 and K to O is 278). The best workaround I found is to simply offset the distances by a small amount and modify the code to support float values instead of integers.

The code operates on an IDLE Shell (for python 3.9.2 64-bit for Windows) in case you wanted to take a look at it, modify it, etc.

Code :: 

import csv

dict_list = []
condDict = {}
store = {}
def getFileInfo(filename):
    reader = csv.DictReader(open(filename))
    for line in reader:
        dict_list.append(line)
    print("Original CSV - " + str(dict_list))
getFileInfo("C:\Python Stuff\Mileage Problem Code and Data\Mileage - Sheet1.csv") ## Put file name here

for i in range(len(dict_list)):
    for key, value in dict_list[i].items():
        caseList = []
        if(value != "--" and key != ''):
            condDict.setdefault(value,{dict_list[i]['']:key})

print("Condensed version of CSV (duplicates removed and organized by distance) - " + str(condDict))
print("\n")
for d, f in condDict.items():
    store.setdefault(d,f)

startingLoc = input("What location would you like to start in? ")
temp = startingLoc

optimalPath = []
visitedCities = [startingLoc]
totalDistance = 0
for l in range(len(condDict.keys())):
    minimum = 1000000000
    locationDict = {}
    for g, f in condDict.items():
        if(startingLoc in f.keys() or startingLoc in f.values()):
            locationDict.setdefault(g,f)
    print(locationDict)
    for h in range(len(locationDict)):
        for x in range(len(locationDict)):
            if int(list(locationDict.keys())[x]) < minimum:
                minimum = int(list(locationDict.keys())[x])
        if(startingLoc == list(locationDict[str(minimum)].values())[0]) and (list(locationDict[str(minimum)].keys())[0] not in visitedCities):
            startingLoc = list(locationDict[str(minimum)].keys())[0]
        elif(list(locationDict[str(minimum)].values())[0] not in visitedCities):
            startingLoc = list(locationDict[str(minimum)].values())[0]
    optimalPath.append(minimum)
    visitedCities.append(startingLoc)
    for g in range(len(locationDict)):
        condDict.pop(list(locationDict.keys())[g])
    if(len(optimalPath) == len(dict_list)-1):
        break
print("\n")
        
final = visitedCities[-1]
print("Optimal Path :: (Starting from " + temp + ")")
print("\n")
for j in range(len(optimalPath)):
    print(store[str(optimalPath[j])])
    totalDistance += int(optimalPath[j])
for o, p in store.items():
    if (p == {temp:final}):
        totalDistance += int(o)
        print({temp:final})
        print("\n")
    elif (p == {final:temp}):
        totalDistance += int(o)
        print({final:temp})
        print("\n")
print("Which would have a total distance of " + str(totalDistance) + " miles.")
