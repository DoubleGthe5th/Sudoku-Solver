#introduces player to sudoku/startup commands
lbiqwclb = input("Welcome to the Sudoku Solver. This solver only takes in classic sudokus (ie standard sudoku rules[1-9 in every row,column, and box]). Press enter to contiune")
print(chr(27) + "[2J")
lbiqwclb = input(" To start, enter in your unsolved sudoku row-by-row. Use dashes - to siginify blank spaces, and numbers to show given digits.\n An exmple of an imputtedd row would be \"1-3-5-7-9\", where 1,3,5,7, and 9 are given digits and the 4 blanks are unknown digits. Press enter to contiune")
print(chr(27) + "[2J")
print("---------     Use these 9 dashes to measure out your row")
grid = []
from curses.ascii import isdigit
changes = 15000

#functions to solve sudokus

#checks if sudoku has been solved yet
def testforsolve(grid):
    for row in grid:
        for spot in row:
            if len(spot) > 1:
                return False
    return True

#finds index of item(a) in a list(f)
def findindex(f,a):
    try:
        return f.index(a)
    except ValueError:
        return -1
#fills row by checking for already existing digits
def fillrows(row):
    for space in row:
        if len(space) == 1:
            given = int(space[0])
            for x in range(9):
                if len(row[x]) > 1:
                    if findindex(row[x],given) != -1:
                        row[x].remove(given)                       
                    
    return row

#fills row by checking for number being in unique position
def findnumber(row):
    for x in range(1,10):
        amounttimesfound = 0
        for space in row:
            if findindex(space,x) != -1:
                amounttimesfound += 1
        if amounttimesfound == 1:
            for y in range(9):
                if findindex(row[y],x) != -1:
                    if len(row[y]) > 1:
                        row[y] = [x]
    return row
#looks for pairs of numbers
def findpair(row):
    for x in range(1,10):
        for y in range((x+1),10):
            containseither = []
            for z in range(9):
                if findindex(row[z],x) == -1 or findindex(row[z],y) == -1:
                    containseither.append(z)
            if len(containseither) == 2:
                for z in range(9):
                    if findindex(containseither,z) == -1:
                        if findindex(row[z],y) != -1:
                            row[z].remove(y)
                        if findindex(row[z],x) != -1:
                            row[z].remove(x)
                    else:
                        row[z] == [x,y]
    return row

#Finds out column/row stuff in small grids

def rowingrid(sgrid,number):
        howmanyrows = []
        for x in range(3):
            rowcontain = False
            for y in range(3):
                if findindex(sgrid[3*x+y],number) != -1:
                    rowcontain = True
            if rowcontain == True:
                howmanyrows.append(x)
        if len(howmanyrows) == 1:
            return howmanyrows[0]
        return 10

#Fills up row/column/grid until it can't anymore using various stargities

def solverow(row):
    z = row
    row = fillrows(row)
    row = findnumber(row)
    if row != z:
        return(solverow(row))
    return(row)
    

#function to step up sudoku

for y in range(9):
    row = input("")
    row = list(row)
    for x in range(9):
        if isdigit(row[x]) == False:
            row[x] = [1,2,3,4,5,6,7,8,9]
        else:
            row[x] = [int(row[(x)])]
    grid.append(row)
print("solving is currently in process")

#Main place where sudoku is solved

while testforsolve(grid) == False:
        #rows
        for x in range(9):
            grid[x] = solverow(grid[x])
        #columns
        for x in range(9):
            column = []
            for row in grid:
                column.append(row[x])
            column = solverow(column)
            y = 0
            for row in grid:
                row[x] = column[y]
                y += 1
        #grids
        for x in range(9):
            smallgrid = []
            for y in range(3):
                for z in range(3):
                    smallgrid.append(grid[(x - x%3) + y][(x%3)*3+z])
            smallgrid = solverow(smallgrid)             
            for y in range(3):
                for z in range(3):
                    grid[(x - x%3) + y][(x%3)*3+z] = smallgrid[y*3 + z]
        #ends code if sudoku is too advanced to solve
        changes -= 1
        if changes < -1:
            print(chr(27) + "[2J")
            print("Sorry, but the sudoku you have inputted is either unsolveable or is too advanced for the program. Here is what the computer was able to compute.")
            for row in grid:
                x = ""
                for space in row:
                    if len(space) > 1:
                        x += "-"
                    else:
                        x += str(space[0])
                print(x)
            exit()

#Prints out final output AKA solved sudoku if sudoku is solved

print(chr(27) + "[2J")
for row in grid:
    x = ""
    for space in row:
        x += str(space[0])
    print(x)