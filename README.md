# CSE-366-4---2021-1-60-108
import random
import matplotlib.pyplot as plt

class Environment:
    def __init__(self):
        self.grid_size = 10
        self.grid = [[0] * self.grid_size for _ in range(self.grid_size)]
        self.start = (0, 0)
        self.end = (self.grid_size - 1, self.grid_size - 1)
        self.obstacles = [(random.randint(0, self.grid_size - 1), random.randint(0, self.grid_size - 1)) for _ in range(10)]

        for obstacle in self.obstacles:
            self.grid[obstacle[0]][obstacle[1]] = 1

    def display(self, agent_position=None):
        grid_copy = [row[:] for row in self.grid]  # Create a copy to avoid modifying the original grid
        if agent_position:
            x, y = agent_position
            grid_copy[x][y] = 2  # Mark agent's position on the grid
        plt.imshow(grid_copy, cmap='binary')
        plt.title('Grid Environment')
        plt.show()

class Agent:
    def __init__(self, environment):
        self.environment = environment
        self.position = environment.start
        self.battery = 100

    def move(self, direction):
        x, y = self.position
        dx, dy = direction
        new_x, new_y = x + dx, y + dy

        # Check if the new position is within the grid boundaries and not blocked by an obstacle
        if 0 <= new_x < self.environment.grid_size and 0 <= new_y < self.environment.grid_size \
                and not self.environment.grid[new_x][new_y]:
            self.position = (new_x, new_y)
            self.battery -= 10
            if self.battery <= 0:
                self.recharge()

    def recharge(self):
        self.battery = 100

    def check_battery(self):
        return self.battery

class Simulation:
    def __init__(self):
        self.environment = Environment()
        self.agent = Agent(self.environment)

    def run(self):
        # Implement simulation logic
        # For example, move the agent through the environment using pathfinding algorithms
        # Here we can call pathfinding algorithms to find the optimal path for the agent

        # For demonstration, let's make the agent move randomly until it reaches the goal
        while self.agent.position != self.environment.end:
            directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]  # Possible movement directions
            direction = random.choice(directions)
            self.agent.move(direction)
            self.environment.display(agent_position=self.agent.position)  # Display the environment with the agent's position

    def visualize(self):
        self.environment.display(agent_position=self.agent.position)  # Display the final environment after simulation

class PathfindingAlgorithms:
    def __init__(self, environment):
        self.environment = environment

    def uniform_cost_search(self, start, end):
        # Implement Uniform Cost Search algorithm
        pass

    def a_star(self, start, end):
        # Implement A* algorithm
        pass

if __name__ == "__main__":
    simulation = Simulation()
    simulation.run()
    simulation.visualize()
    
