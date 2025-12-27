# gesture-controlled-drone
This project explores controlling a commercial drone using hand gestures instead of a traditional remote controller. By translating human motion into real-time flight commands, the project investigates more intuitive and accessible methods of human-drone interaction.

Conventional drone controllers require extensive practice and fine motor control skills. Gesture-based control has the potential to:
- Make drones more intuitive for beginners
- Improve accessibility
- Make it more engaging and interactive

### Features
- Real-time gesture input
- Directional flight control via hand motion
- Modular structure for future gesture expansion

### Technologies and Tools
- Programming Language: Python
- Sensors: IMU
- Drone: DJI Tello
- Libraries / frameworks:


I began the project by coding keyboard-based flight controls to test whether the drone could reliably respond to software commands. I implemented basic actions such as takeoff, landing, and directional movement. This step was essential to confirm that communication between the computer and the drone was working correctly before adding more complex control systems.

I was also able to connect the drone’s camera to stream real-time video to my computer. This allowed me to observe the drone’s movement during flight. Both movement and live vision were laggy, but I had a functional baseline system.

![Keyboard](/Gifs/keyboard_rotate.gif)



Next, I attempted to integrate the IMU to enable hand-gesture control. Initially, the IMU would not connect to the computer, preventing me from accessing orientation and motion data needed for gesture recognition. I discovered that it would be easier to connect the IMU through bluetooth rather than through the USB port.



With the IMU connected, I began implementing gesture-based commands using loops and multiple if and if-else statements. I successfully programmed the drone to take off and land based on detected hand movements.

However, a major issue appeared: the drone would continue taking off even when I stopped moving my hand. This made the behavior unpredictable and unsafe. At first, it was unclear whether the issue was related to sensor noise or the logic of the control code.

After further testing, I realized that the drone was responding to previous IMU inputs rather than current ones. Gesture commands were being queued and executed with a delay, causing the drone to lag behind my actual hand movements.

I attempted to solve this by adding delays between commands, but this only increased latency and did not prevent repeated takeoff commands. This made it clear that the problem was not timing alone, but how commands were structured and triggered.

To fix the issue, I refactored the control logic by converting gesture commands into dedicated functions instead of repeatedly triggering them inside a loop. This change ensured that each gesture resulted in a single, intentional command rather than multiple repeated executions. This also made the code much more organized and efficient.


Another problem arised when the drone would not connect simultaneously with the IMU. This was a major problem because I needed both the IMU and the drone to connect to the computer to make the gesture controls work. The problem was that the two connections were operating on different parallels and could not operate asynchronously alongside each other.

After troubleshooting the issue, I discovered that the problem was related to how sensor data was being handled in the program. By using asyncio, I was able to run the IMU data stream asynchronously alongside the drone control code. This allowed the IMU to continuously send data without blocking other processes, successfully restoring sensor communication.



  <img src="/Gifs/Gesture_takeoffforward.gif" width="500" />
  <img src="/Gifs/Gesture_4direction.gif" width="500" />
  <img src="/Gifs/Gesture_land.gif" width="500" />

