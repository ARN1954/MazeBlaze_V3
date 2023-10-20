# MazeBlaze-v3.1
## Left Follow Rule (LFR)
### Theory
The Left-Hand Rule (LFR), also known as the "left-follow-algorithm," is a maze solving technique used to navigate through 2D mazes. To use LFR, you start at the entrance of a maze with your left hand touching the wall to your left. As you navigate through the maze, you follow a set of rules:

1. **Always turn left:** Whenever you reach an intersection or have a choice of paths, you make a left turn if it's possible, keeping your left hand on the wall.

2. **Go straight if a left turn is blocked:** If you come to an intersection where turning left is not an option because it leads to a wall, you continue moving straight while still touching the left wall.

3. **Take a right turn as a last resort:** If you encounter an intersection where you cannot turn left or go straight (usually because of a wall or obstacle), you take a right turn.

4. **Reverse when there are no other options:** If you find yourself in a situation where you can't turn left, go straight, or turn right, it means you've likely reached a dead end. In this case, you need to turn around and backtrack.

### Implementation

The Left Follow algorithm is a method for navigating and tracking the movement of a bot as it encounters and traverses various paths. This algorithm records the bot's movements by assigning numeric values to different directions and then tracking these values in an array named `store_path`. The directions are indexed as follows:

- North: 1
- East: 2
- South: 3
- West: 4

It is important to note that the algorithm assumes that the bot initially faces the North direction. Subsequently, the other directions are determined based on the North direction. These directions are fixed with respect to the world frame, and the bot continually updates its direction as it takes turns.

#### Direction Index Tracking

The program is designed to keep track of the serial numbers (direction indices) based on the assumptions mentioned above. Whenever the bot encounters a node or takes a turn, it records the direction index into the `store_path` array. Four key conditions are defined to track the bot's movement:

1. **Condition for Right Turn**

   When the bot takes a right turn, it increments the `direction` by 1. This is achieved through the code:

   ```c
   direction = (direction + 1) % 4;
   if (direction == 0) direction = 4;
   ```

   This code ensures that the `direction` cycles between 1 and 4, representing North, East, South, and West, respectively.

2. **Condition for Left Turn**

   When the bot takes a left turn, it decrements the `direction` by 1. This is done using:

   ```c
   direction = (direction - 1) % 4;
   if (direction == 0) direction = 4;
   ```

   This code ensures that the `direction` cycles between 1 and 4, representing North, East, South, and West, respectively.

3. **Condition for U-Turn**

   When the bot performs a U-turn, the `direction` is decremented by 2:

   ```c
   direction = (direction - 2) % 4;
   if (direction == 0) direction = 4;
   if (direction == -1) direction = 3;
   ```

   This operation effectively represents a 180-degree turn.

4. **Condition for Moving Straight**

   When the bot continues to move straight, the `direction` remains unchanged:

   ```c
   direction = direction;
   ```

   In this case, the `direction` remains the same, signifying that the bot maintains its current orientation.

When the robot moves and follows these rules, it records its current direction in the store_path array. This helps us keep track of where the robot has been. The robot always knows which direction it's facing, even if it takes many turns.

### Description Of Functions Used
