# SelfDrivingCars_GeneticAlgorithm


## Overview
This project is a racing game developed in Python using the Pygame library. It features AI-controlled cars that learn and evolve through genetic algorithms, competing on procedurally generated tracks. The game combines elements of artificial intelligence, physics, and graphical rendering to create an engaging experience.

## Features
- **AI-Controlled Cars**: Cars utilize neural networks to make decisions based on their environment.
- **Genetic Algorithms**: The AI learns and evolves over generations through mutation and crossover of weights and biases.
- **Procedural Track Generation**: Tracks are generated randomly, providing unique racing experiences each time.
- **Dynamic Graphics**: Utilizes Pygame for rendering graphics and handling user input.
- **User Interface**: Users can interact with the game through various controls to enhance gameplay experience.

## User Controls
The game provides several interactive features for users, accessible through keyboard controls:

- **Press `B` to Breed**: Initiates the breeding process between selected cars. This will create new offspring cars that inherit traits from their parents, allowing for the evolution of better-performing AI.
  
- **Press `M` to Change Track**: Changes the current track to a new randomly generated layout. This feature allows for varied racing experiences each time you play.

- **Press `N` to Mutate**: Mutates the weights and biases of the selected AI cars. This introduces random changes that can lead to improved performance or entirely new behaviors.

- **Press `L` to Toggle Lines**: Toggles the display of player lines on the track. This can help users visualize car paths during races.

- **Press `P` to Toggle Player Display**: Toggles whether the player representation is shown on the screen.

- **Press `I` to Toggle Info Display**: Toggles additional information about the race, such as car speeds and positions.

## Requirements
To run this project, you need the following:
- Python 3.x
- Pygame library
- NumPy library
- Shapely library
- Pillow library

You can install the required libraries using pip:

```bash
pip install pygame numpy shapely pillow
```

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/AI-Racing-Game.git
   ```
2. Navigate to the project directory:
   ```bash
   cd AI-Racing-Game
   ```
3. Run the game:
   ```bash
   python main.py
   ```

## Code Structure

### Main Components
- **gameLogic.py**: Contains the core logic for the game, including AI behavior, track generation, and car movement.
- **Images/Sprites/**: Directory for car sprites used in the game.
- **Images/TracksMapGen/**: Directory for track images used in procedural generation.

### Key Functions

#### Initialization and Configuration
```python
pygame.init()  # Initializes Pygame for use in the game.
size = width, height = 1600, 900  # Sets the size of the game window.
```
- This section initializes Pygame and sets up the window dimensions for rendering.

#### Color Definitions
```python
white = (255, 255, 255)
green = (0, 255, 0)
blue = (0, 0, 128)
black = (0, 0, 0)
gray = pygame.Color('gray12')
Color_line = (255, 0, 0)
```
- Defines color constants used throughout the game for rendering various elements.

#### Image Loading
```python
white_small_car = pygame.image.load('Images/Sprites/white_small.png')
bg = pygame.image.load('bg7.png')
```
- Loads images for car sprites and backgrounds to be displayed during gameplay.

#### Utility Functions

1. **Distance Calculation**
   ```python
   def calculateDistance(x1, y1, x2, y2):
       """
    Calculates the Euclidean distance between two points (x1, y1) and (x2, y2).
    Useful for determining the distance between objects in the game.
    
    Parameters:
    - x1, y1: Coordinates of the first point.
    - x2, y2: Coordinates of the second point.
    
    Returns:
    - dist: The distance between the two points.
    """
       dist = math.sqrt((x2 - x1)**2 + (y2 - y1)**2)
       return dist
   ```
   - Calculates the Euclidean distance between two points on the screen. This is essential for determining proximity between cars or obstacles.

2. **Rotation Function**
   ```python
   def rotation(origin, point, angle):
       """
    Rotates a point around a given origin by a specified angle.
    
    Parameters:
    - origin: The (x, y) coordinates of the center of rotation.
    - point: The (x, y) coordinates of the point to rotate.
    - angle: The angle of rotation in degrees.
    
    Returns:
    - (qx, qy): The new coordinates of the point after rotation.
    """
       ox, oy = origin
       px, py = point
       qx = ox + math.cos(angle) * (px - ox) - math.sin(angle) * (py - oy)
       qy = oy + math.sin(angle) * (px - ox) + math.cos(angle) * (py - oy)
       return qx, qy
   ```
   - Rotates a point around a specified origin by a given angle. This is crucial for orienting cars based on their direction of movement.

3. **Movement Function**
   ```python
   def move(point, angle, unit):
       x = point[0]
       y = point[1]
       rad = math.radians(-angle % 360)
       x += unit * math.sin(rad)
       y += unit * math.cos(rad)
       return x, y
   ```
   - Moves a point in a specified direction based on an angle and distance. This function drives car movements in response to user input or AI decisions.

4. **Activation Function**
   ```python
   def sigmoid(z):
       """
    Sigmoid activation function, often used in neural networks to introduce non-linearity.
    
    Parameters:
    - z: The input value to the sigmoid function.
    
    Returns:
    - The output of the sigmoid function, a value between 0 and 1.
    """
       return 1.0 / (1.0 + np.exp(-z))
   ```
   - Implements the sigmoid activation function used in neural networks to introduce non-linearity in decision-making processes.

### Genetic Algorithm Functions

1. **Weight Mutation**
   ```python
   def mutateOneWeightGene(parent1, child1):
        """
    Copies weights from a parent neural network to a child and introduces a random mutation
    to one of the weights to create slight variations. This is useful for evolutionary algorithms,
    where small changes can lead to exploring different solutions.

    Parameters:
    - parent1: The parent neural network object from which weights are copied.
    - child1: The child neural network object that will inherit weights and be mutated.

    The child1 object should have the following attributes:
    - sizes: A list of integers representing the number of neurons in each layer.
    - weights: A nested list (or matrix) storing the weights of the neural network.
    - biases: A list of biases for each neuron.

    Returns:
    - None (the function directly modifies the weights of `child1`)
    """
       sizenn = len(child1.sizes)
       # Copy parent weights into child weights and modify one randomly.
       ...
       return
   ```
   - Mutates one weight gene from parent to child car by copying weights from `parent1` to `child1` and randomly modifying one weight to introduce variation.

2. **Bias Mutation**
   ```python
   def mutateOneBiasesGene(parent1, child1):
       """
    Copies weights and biases from a parent neural network to a child and introduces a random
    mutation to one of the biases. This helps in evolving different neural network behaviors.

    Parameters:
    - parent1: The parent neural network object from which biases and weights are copied.
    - child1: The child neural network object that will inherit biases and be mutated.

    The child1 object should have the following attributes:
    - sizes: A list of integers representing the number of neurons in each layer.
    - weights: A nested list (or matrix) storing the weights of the neural network.
    - biases: A list of biases for each neuron.

    Returns:
    - None (the function directly modifies the biases of `child1`)
    """
       sizenn = len(child1.sizes)
       # Similar logic for biases as with weights.
       ...
       return
   ```
   - Similar to weight mutation but focuses on biases within the neural network structure.

3. **Crossover Functions**
```python
def uniformCrossOverWeights(parent1, parent2, child1, child2):
    """
    Performs a uniform crossover of weights between two parent neural network objects,
    creating two children with mixed weights. This is useful in genetic algorithms for 
    combining features of two parent networks to create potentially better offspring.

    Parameters:
    - parent1: The first parent neural network object.
    - parent2: The second parent neural network object.
    - child1: The first child neural network object that will receive a mix of weights.
    - child2: The second child neural network object that will receive a mix of weights.

    The child objects should have the following attributes:
    - sizes: A list of integers representing the number of neurons in each layer.
    - weights: A nested list (or matrix) storing the weights of the neural network.
    - biases: A list of biases for each neuron.

    Returns:
    - None (the function directly modifies the weights and biases of `child1` and `child2`)
    """
    # Given two parent car objects, it modifies the children car objects weights.
    ...
    return

def uniformCrossOverBiases(parent1, parent2, child1, child2):
    """
    Performs a uniform crossover of biases between two parent neural network objects,
    creating two children with mixed biases. This is part of a genetic algorithm process
    where biases from two parents are combined to produce potentially better offspring.

    Parameters:
    - parent1: The first parent neural network object.
    - parent2: The second parent neural network object.
    - child1: The first child neural network object that will receive a mix of biases.
    - child2: The second child neural network object that will receive a mix of biases.

    The child objects should have the following attributes:
    - sizes: A list of integers representing the number of neurons in each layer.
    - weights: A nested list (or matrix) storing the weights of the neural network.
    - biases: A list of biases for each neuron.

    Returns:
    - None (the function directly modifies the biases and weights of `child1` and `child2`)
    """
    # Given two parent car objects, it modifies the children car objects biases.
    ...
    return
```
- These functions facilitate genetic crossover between two parent cars to create offspring with mixed traits by exchanging weights and biases.

### Track Generation Function

```python
def generateRandomMap(screen):
    # Generates a random maze/grid that serves as a race track.
    ...
    return 
```
- Uses maze generation algorithms to create a dynamic racetrack layout that varies with each game session. The function handles loading track images and placing them based on maze cell states.

## Contributing
Contributions are welcome! If you have suggestions for improvements or new features, please fork the repository and submit a pull request.

## Acknowledgments
Special thanks to the contributors of Pygame and other libraries that made this project possible.
