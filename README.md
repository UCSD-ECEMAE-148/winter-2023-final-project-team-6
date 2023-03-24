# MAE/ECE 148 Winter 2023 at UCSD
## TEAM 6
Our project uses the OAK-D camera, a roboflow YOLO model, PyVESC module, and an Arduino-powered camera mount to get our car to scan its surroundings until it finds a basketball and drive until it is within about 0.5 m of the ball.
## Car Assembly
### Vehicle Body
![image](https://user-images.githubusercontent.com/58583277/227629739-8605ff8f-2651-47f2-8638-b58979c6237b.png) ![image](https://user-images.githubusercontent.com/58583277/227629805-54638b5a-0fda-4de6-a73b-0aee29c2c946.png)


## Tech Stack
### RoboflowOak Module
We used roboflow to train a ball detection model and host the model. We, then, made API calls to hosted model to retrieve predictions on frame captures from the OAK-D camera. Once a ball is found, we wrote a script to calculate the angle between the center of the bounding box drawn around the detected ball and the centerline of the camera (which by default is the center of the frame).
### PyVESC Module
We used the pyvesc module to set our servo's angle once a detection has been made. The steering angle is proportional to the calculated angle. Once the steering is set, we increase throttle for about half a second and then stop the motor to make another detection. We then loop over these steps until the ball is within 0.5 m of the frame. Our stopping condition was for the width of the bounding box of the ball to be a certain ratio of the total frame width. The ratio is hardcoded based on fine-tuning to get the car to stop at about 0.5 m.
### Arduino Board
We used an arduino nano to control the camera mount. The camera mount can rotate horizontally (yaw-equivalent) within a range of 180 degrees. And it can move up and down (pitch-equivalent) within a range of 90 degrees. This is used to move the camera around so it can scan the surroundings for a ball (in case the ball is not in frame). 
### Motorized Camera Mount
We designed a camera mount that is actuated by 2 servos, one controls the camera's pitch angle and the other controls the camera's yaw angle. The mount elevates the camera 5 inches amove the vehicle's mounting plate. It allows the camera to turn and scan for the target ball. 
## How To Run The Code
One can run python run.py from inside the Jetson Nano mounted on their car. This will load the model and also detect the motor and begin the purported task of finding a basketball. If no basketball is found, it will remain stationary. The 148remote/ folder contains a cool arduino program for proof of concept. It moves the camera mount through its full range of motion in a rhythmic fashion. 
# Team 6: Wall-E (used to be Cyclops)
- Saathvik Dirisala  
- Victor Chen  
- Yang Song  
