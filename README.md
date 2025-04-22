# Tic Tac Toe Robot Controller

This repository contains a Python implementation for controlling a Niryo robot to play Tic Tac Toe. The controller handles the movement of game pieces on a physical game board using precise positioning.

## Overview

The `RobotController` class provides functionality to:
- Calibrate the robot workspace
- Pick game pieces from a designated yard area
- Place pieces at specific positions on a 3x3 grid
- Handle exception scenarios gracefully

## Requirements

- Niryo Robot with properly configured IP address
- Python 3.6+
- pyniryo package

## Installation

1. Install the required dependencies:
```bash
pip install pyniryo
```

2. Clone this repository:
```bash
git clone https://github.com/yourusername/tic-tac-toe-robot.git
cd tic-tac-toe-robot
```

## Configuration

Before using, configure the robot's IP address in the `RobotController` class:

```python
self.robot = NiryoRobot("10.10.10.10")  # Update this with your robot's IP
```

## Grid Layout

The code implements a 3x3 grid with 5cm spacing between cells. The positions are indexed as follows:

```
0 | 1 | 2
---------
3 | 4 | 5
---------
6 | 7 | 8
```

Where position 4 is the center of the grid.

## Usage

### Basic Example

```python
from robot_controller import RobotController

# Initialize the controller
controller = RobotController()

# Calibrate the workspace
controller.calibrate_workspace()

# Pick a game piece from the yard
controller.pick_from_yard()

# Place the piece at position 4 (center)
controller.place_at_position(4)

# Clean up when done
controller.close()
```

### Game Integration Example

```python
from robot_controller import RobotController

def play_game(moves):
    controller = RobotController()
    controller.calibrate_workspace()
    
    try:
        for position in moves:
            controller.pick_from_yard()
            controller.place_at_position(position)
    finally:
        controller.close()

# Example: Play the center and corners
play_game([4, 0, 8, 2, 6])
```

## Customization

### Adjusting Grid Size

The grid cell size can be modified by changing the `self.cell_size` value:

```python
self.cell_size = 0.05  # 5 cm spacing
```

### Modifying Heights

The base height of the grid and yard positions can be adjusted by modifying the `center_z` and `yard_position` values:

```python
center_z = 0.11  # Grid height
self.yard_position = [0.2, 0.0, 0.11]  # Yard position
```

## Safety Features

The controller includes several safety mechanisms:
- Collision detection and recovery
- Exception handling for robotic operations
- Automatic resource cleanup
