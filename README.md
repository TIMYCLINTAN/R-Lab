from collections import deque
def water_jug_bfs(jug1_capacity, jug2_capacity, target):
    start = (0, 0)
    q = deque([(start, [])])  
    visited = set([start])
    while q:
        (x, y), path = q.popleft()
        if x == target or y == target:
            return path + [(x, y)]
        possible_states = [
            (jug1_capacity, y),  
            (x, jug2_capacity),  
            (0, y),              
            (x, 0),              
            (max(0, x - (jug2_capacity - y)), min(jug2_capacity, y + x)),
            (min(jug1_capacity, x + y), max(0, y - (jug1_capacity - x))),
        ]
        for state in possible_states:
            if state not in visited:
                visited.add(state)
                q.append((state, path + [(x, y)]))
    return None 
if __name__ == "__main__":
    jug1_capacity = 4
    jug2_capacity = 3
    target = 2
    result = water_jug_bfs(jug1_capacity, jug2_capacity, target)
    if result:
        print("Solution found:")
        for step in result:
            print(step)
    else:
        print("No solution exists.")


        .


        Procedure
1.  Start from the initial state (0,0) → both jugs empty.
2. Use a queue (FIFO) to store states and their paths.
3.  Maintain a visited set to avoid repeating states.
4.  At each step, generate all possible states by applying the operations:
•	Fill Jug1
•	Fill Jug2
•	Empty Jug1
•	Empty Jug2
•	Pour Jug1 → Jug2
•	Pour Jug2 → Jug1
5.  If at any state, the amount of water in Jug1 or Jug2 equals the target d, stop and return the path.
6.  If the queue becomes empty, it means no solution exists.



