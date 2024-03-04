# Assignment 1: Dynamic Robot Movement Simulation 
Using Informed Search Strategies(A* Search)-----
------------------------------------------------

import numpy as np: Imports the numpy library and aliases it as np.

import matplotlib.pyplot as plt: Imports the pyplot module from the matplotlib library and aliases it as plt.

import heapq: Imports the heapq module, which provides an implementation of the heap queue algorithm (priority queue).

import random: Imports the random module, which provides functions for generating random numbers.



class Environment:: Defines a class named Environment to represent the grid-based environment.
----------------------------------------------------------------------------------------------
def __init__(self, width=10, height=10, obstacle_density=0.2):: Defines the constructor method for the Environment class, which initializes the environment with default values for width, height, and obstacle density.

self.width = width: Initializes the width of the environment.

self.height = height: Initializes the height of the environment.

self.grid = np.zeros((height, width), dtype=int): Initializes a grid representing the environment, filled with zeros (empty cells).

self.start = (0, 0): Initializes the start position of the agent in the environment to the top-left corner.

self.end = (width - 1, height - 1): Initializes the end position of the agent in the environment to the bottom-right corner.

self.generate_obstacles(obstacle_density): Calls the generate_obstacles method to randomly generate obstacles in the environment based on the specified obstacle density.


def generate_obstacles(self, density):: Defines a method to generate obstacles in the environment.
-------------------------------------------------------------------------------------------------
num_obstacles = int(self.width * self.height * density): Calculates the number of obstacles based on the obstacle density.

for _ in range(num_obstacles):: Iterates to generate obstacles.

x, y = random.randint(0, self.width - 1), random.randint(0, self.height - 1): Randomly selects coordinates for the obstacle.

self.grid[y, x] = 1: Marks the cell in the grid as an obstacle.

def get_neighbors(self, x, y):: Defines a method to get neighboring cells for a given cell in the environment.

neighbors = []: Initializes an empty list to store neighboring cells.

for dx in [-1, 0, 1]:: Iterates over the x-offsets of neighboring cells (-1, 0, 1).

for dy in [-1, 0, 1]:: Iterates over the y-offsets of neighboring cells (-1, 0, 1).

if dx == 0 and dy == 0:: Skips the current iteration if both dx and dy are zero (current cell).

nx, ny = x + dx, y + dy: Calculates the coordinates of the neighboring cell.

if 0 <= nx < self.width and 0 <= ny < self.height:: Checks if the neighboring cell is within the bounds of the environment.

neighbors.append((nx, ny)): Adds the neighboring cell to the list of neighbors.

return neighbors: Returns the list of neighboring cells.  


def a_star_search(env, start, goal):: Defines a function named a_star_search to perform A* search algorithm to find the shortest path from start to goal in the environment env.
-------------------------------------------------------------------------------------------------------------------------

frontier = PriorityQueue(): Creates an instance of the PriorityQueue class to store frontier nodes during A* search.

frontier.put((0, start, 0)): Initializes the frontier with the start node, where the cost is 0 and the heuristic is 0.

visited = set(): Initializes an empty set to keep track of visited nodes.

came_from = {}: Initializes an empty dictionary to store the parent node for each visited node.

cost_so_far = {start: 0}: Initializes a dictionary to keep track of the cost of reaching each node from the start node.

while frontier:: Executes a loop until the frontier is empty.

current_cost, current, heuristic = frontier.get(): Retrieves the node with the lowest cost from the frontier.

if current == goal:: Checks if the current node is the goal node.

return reconstruct_path(came_from, current): If the goal is reached, reconstructs and returns the path from the start to the goal node.

if current in visited:: Checks if the current node has already been visited.

continue: Skips the current iteration if the node has already been visited.

visited.add(current): Adds the current node to the set of visited nodes.



The Agent class represents the robot agent that navigates through the environment:
-----------------------------------------------------------------------------------
__init__: Initializes the agent with the environment, start and end positions, and energy capacity.

move: Moves the agent in the environment using the A* search algorithm, updating the position, energy, and path.

recharge: Recharges the agent's energy when it runs out.



The visualize_environment function visualizes the grid environment, including the agent's position, start and end positions, and obstacles using matplotlib.
--------------------------------------------------------------------------------------------------------------------------------

The simulate function runs the simulation, where the agent navigates the environment until it reaches the goal position.







Using Informed Search Strategies(A* Search)-----
------------------------------------------------
All function are almost same

uniform_cost_search function implements the Uniform Cost Search algorithm to find the shortest path from a start node to a goal node in a grid-based environment.
---------------------------------------------------------------------------------------------------------------------------------------

visited: A set to keep track of visited nodes.
queue: A priority queue (heap) to store nodes prioritized by their path cost. Each element in the queue is a tuple (cost, current_node, path), where cost is the total cost to reach the current_node from the start node, and path is the path taken to reach the current_node.
The initial element in the queue is (0, start, []), indicating that the cost to reach the start node is 0, and the path taken so far is empty.
The loop continues until the queue is empty, meaning there are no more nodes to explore.
In each iteration, the node with the lowest cost is dequeued from the queue. This node represents the current node being explored.
If the current node is the goal node, the function returns the path to reach the goal node (path + [current]), indicating that a path from the start to the goal has been found.
If the current node has already been visited, it's skipped to avoid revisiting nodes unnecessarily.
If the current node has not been visited:
It's added to the set of visited nodes.
For each neighboring node of the current node, a new cost is calculated by adding 1 to the current cost (assuming uniform cost for each move).
A tuple (new_cost, neighbor, path + [current]) is pushed onto the queue, representing the updated cost, the neighboring node, and the path taken to reach it.


