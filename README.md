#ExpNo:10 Implementation of Classical Planning Algorithm 

NAME: YAZHINI 
REG NO: 2305002028
## Algorithm or Steps Involved:
Define the initial state
Define the goal state
Define the actions
Find a plan to reach the goal state
Print the plan

### Example - 1
```
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
Output:
['move_A_to_B']
```

### Example - 2
```
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
Output:
['move_A_to_B', 'move_B_to_C']
```

### PROGRAM
```
from collections import deque

# Check if goal is satisfied
def is_goal_state(current_state, goal_state):
    return all(current_state.get(k) == v for k, v in goal_state.items())

# Apply action effects
def apply_action(current_state, effect):
    new_state = current_state.copy()
    new_state.update(effect)
    return new_state

# Check if action is valid
def is_applicable(current_state, preconditions):
    return all(current_state.get(k) == v for k, v in preconditions.items())

# BFS Planner
def find_plan(initial_state, goal_state, actions):
    queue = deque([(initial_state, [])])
    visited = set()

    while queue:
        state, plan = queue.popleft()

        # Goal reached?
        if is_goal_state(state, goal_state):
            return plan

        state_tuple = tuple(sorted(state.items()))
        if state_tuple in visited:
            continue
        visited.add(state_tuple)

        # Try each action
        for action_name, action_rules in actions.items():
            if is_applicable(state, action_rules["precondition"]):
                next_state = apply_action(state, action_rules["effect"])
                queue.append((next_state, plan + [action_name]))

    return None


initial_state = {
    'Cargo1': 'Airport_A',
    'Cargo2': 'Airport_B',
    'Plane1': 'Airport_A',
    'Plane2': 'Airport_B'
}

goal_state = {
    'Cargo1': 'Airport_B',
    'Cargo2': 'Airport_A'
}

actions = {
    'Load_C1_P1': {
        'precondition': {'Cargo1': 'Airport_A', 'Plane1': 'Airport_A'},
        'effect': {'Cargo1': 'Plane1'}
    },

    'Unload_C1_P1': {
        'precondition': {'Cargo1': 'Plane1', 'Plane1': 'Airport_B'},
        'effect': {'Cargo1': 'Airport_B'}
    },

    'Fly_P1_A_to_B': {
        'precondition': {'Plane1': 'Airport_A'},
        'effect': {'Plane1': 'Airport_B'}
    },

    'Load_C2_P2': {
        'precondition': {'Cargo2': 'Airport_B', 'Plane2': 'Airport_B'},
        'effect': {'Cargo2': 'Plane2'}
    },

    'Unload_C2_P2': {
        'precondition': {'Cargo2': 'Plane2', 'Plane2': 'Airport_A'},
        'effect': {'Cargo2': 'Airport_A'}
    },

    'Fly_P2_B_to_A': {
        'precondition': {'Plane2': 'Airport_B'},
        'effect': {'Plane2': 'Airport_A'}
    }
}

# Run planner
plan = find_plan(initial_state, goal_state, actions)

print("Plan found:")
print(plan)

```

### OUTPUT
<img width="778" height="227" alt="image" src="https://github.com/user-attachments/assets/3411c18b-a2f1-4c8b-a8cf-52f7e7bc18da" />


RESULT
Thus the program to implement Classical Planning Algorithm has been executed successfully.

