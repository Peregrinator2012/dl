# The Maze Runner
author: [Yincen Xia](https://github.com/philipxyc)

# Get Started

To get started, please simply fork this GitLab repository and
follow the structure and submissions guidelines below. 
**Remember to change your repo to a private one before you commit to it.**


# Repository Structure

### README.md

Problem description and requirements.

### maze.py

A basic template for this homework.

### demoMap/\*.txt

Some test cases for you to test whether your program works properly.


# Submit

Submissions are done by simply running(push all your changes to GitLab first):

```git tag {tagname} && git push origin {tagname}``` from within the root folder of this repo.

You need to define your own submisson tag by changing `{tagname}`, 
e.g. ```git tag first_trial && git push origin first_trial```

**Please use a new tag for every new submission.**
Every submission will create a new GitLab issue, where you can track the progress.

# Regulations

- Due: 23:59:59, April 4, 2019, CST
- No late submission will be accepted
- You have 30 chances of grading (i.e. ```git tag```) in this homework. **Your assignment codes will not be graded if you do not set your repo into private (and will also not be counted into 30 chances of grading).** You are able to require grading at most 10 times every 24 hours. If you hand in more 30 times, **each extra submission will lead to 10% deduction**.
- We enforce academic integrity strictly. If you participate in any from of cheating, you will fail this course immediately. You can view full edition on [Piazza](https://piazza.com/class/jrykv8wi15m5dx?cid=7).
- If you have any question about this homework, please ask on Piazza first.

# Description

You woke up, but you found that you are currently trapped in a maze with moving walls. Since you don't want to die here, you have to get as more food as possible.

## Maze Map:

The map was given by a one dimensional python list whose number of rows and columns are given, this means that you have to do it yourself if you want to reshape the list into a matrix. All elements in the map list are integer, here is a specific explanation for each number:

- -1 represent the food, there could be a lot of food in the map.
- 0 stands for blank space which are safe to enter.
- ```runner_id``` is a positive integer, and ```2*runner_id``` is your position in the map. Since you will not consume the food at once, you have to string food together and put them behind you, ```2*runner_id - 1``` represent the food you got. Please notice that you are also **not allowed** to touch the food you gathered.
- ```i``` is each positive integer that not equal to ```runner_id```,  ```2*i``` is the moving part of a wall, and ```2*i - 1``` is the body part of each wall. Each wall will have only one moving part at one end (only one pixel), this end could move in any direction. And the body part of the wall is connected to its moving part, the length of the body part could be any fixed number. For a better understanding, you could compare the moving wall to a snake with head and body.

## Code

```python
def move_algo(maze: list, runner_id: int, size_m: int, size_n: int):
    """The algorithm to deside which direction will be taken, return which step to take"""
```

The `move_algo` function is the only part you should implement. A one dimensional list was given, `size_m` means the number of rows and `size_n` means the number of columns. The return value should be a integer that represent the runner's movement, here is the definition for it:

            x means the row index, y means the column index
            +------------------------------------------->(y)
            |
            |
            |
            |                   0
            |                   |
            |              3 ---*--- 1
            |                   |
            |                   2
            |
            |
            |
            |
            V
           (x)
## Algorithm

The final goal is to gather more food, but once the runner hit the wall, the game is over. So, your work is to replace ```# YOUR ALGORITHM``` with the required algorithm. Your algorithm should work **exactly** the same as the pseudocode below:
<pre>
Set MAP to be the 2D array of the field
Set (x,y) to be your head position in MAP (where MAP(x,y) == 2 * your ID)
if your head does not exist {
    return -1
}
for each point (i,j) in MAP {
    calculate heuristic_dist(i,j) to be the Manhattan distance from (i,j) to the nearest food
}
for each point in MAP {
    Initialize minimum_cost with zero
    Initialize is_visited with False
    Initialize prev_point
}
Set OPEN to be the set of points waiting to be check
Put only (x,y) in OPEN
while OPEN is not empty {
    Take the point P(i,j) from OPEN with the lowest minimum_cost(i,j)+heuristic_dist(i,j) (when there is more than one minimum, take the first point by ascending order with X primary index and Y secondary index )
    if P is food {
        Record P
        break
    }
    Set is_visited(P) = True
    Remove P from OPEN

    for each adjacent point Q of P {
        if Q is able to go and ( Q is not visited or minimum_cost(P) + 1 is smaller than minimum_cost(Q) ):
            Add Q to OPEN
            Set minimum_cost(Q) = be minimum_cost(P) + 1
            Set prev_point(Q) = P
    }
}
if food is not found {
    if there is no way to go {
        return -1
    }
    Take the first feasible direction ANS of (x,y) clockwise (the order 0,1,2,3)
    return ANS
}
if food is found {
    Trace prev_point with recorded P to find the first direction ANS of (x,y)
    return ANS
}
</pre>

