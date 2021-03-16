# Traveling_Salesman_Problem

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
