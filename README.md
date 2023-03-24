# MAE/ECE 148 Winter 2023 at UCSD
## TEAM 6
Our project uses the OAK-D camera, a roboflow YOLO model, PyVESC module, and an Arduino-powered camera mount to get our car to scan its surroundings until it finds a basketball and drive until it is within about 0.5 m of the ball.
## Car Assembly
### Vehicle Body
<img src="https://user-images.githubusercontent.com/58583277/227629805-54638b5a-0fda-4de6-a73b-0aee29c2c946.png" width=40% height=40%> <img src="https://user-images.githubusercontent.com/58583277/227641325-697c8cda-a3ac-4d78-9a13-53a1cc52b471.png" width=40% height=40%> <img src="https://user-images.githubusercontent.com/58583277/227629739-8605ff8f-2651-47f2-8638-b58979c6237b.png" width=40% height=40%>
### Camera Mount
<img src="https://user-images.githubusercontent.com/58583277/227642485-4f448fb1-47b8-4ab7-b0f7-6edf5321f54c.jpg" width=75% height=75%>

![BaseGears](https://user-images.githubusercontent.com/58583277/227658524-233e6c31-cc78-495c-8032-ac0c4f8be5b9.png)

![BasePlate](https://user-images.githubusercontent.com/58583277/227657014-3986f34d-d2b6-40fd-9a19-5dfb6a4f50e6.png)

![CameraPlate](https://user-images.githubusercontent.com/58583277/227657015-886ac40c-0cff-44a8-929c-ef0a823e8ca1.png)

![TallMount](https://user-images.githubusercontent.com/58583277/227657016-4c8e9f72-1d04-466c-a677-dd73e047253d.PNG)

![CameraGear](https://user-images.githubusercontent.com/58583277/227657018-ac78ed20-f576-4419-8053-c66dbd9cf855.png)


## Tech Stack
### RoboflowOak Module
We used roboflow to train a ball detection model and host the model. We, then, made API calls to hosted model to retrieve predictions on frame captures from the OAK-D camera. Once a ball is found, we wrote a script to calculate the angle between the center of the bounding box drawn around the detected ball and the centerline of the camera (which by default is the center of the frame).
### PyVESC Module
We used the pyvesc module to set our servo's angle once a detection has been made. The steering angle is proportional to the calculated angle. Once the steering is set, we increase throttle for about half a second and then stop the motor to make another detection. We then loop over these steps until the ball is within 0.5 m of the frame. Our stopping condition was for the width of the bounding box of the ball to be a certain ratio of the total frame width. The ratio is hardcoded based on fine-tuning to get the car to stop at about 0.5 m.
### Arduino Board
We used an arduino nano to control the camera mount. The camera mount can rotate horizontally (yaw-equivalent) within a range of 180 degrees. And it can move up and down (pitch-equivalent) within a range of 90 degrees. This is used to move the camera around so it can scan the surroundings for a ball (in case the ball is not in frame). 
### Motorized Camera Mount
We designed a camera mount that is actuated by 2 servos, one controls the camera's pitch angle and the other controls the camera's yaw angle. The mount elevates the camera 5 inches amove the vehicle's mounting plate. It allows the camera to turn and scan for the target ball. 


https://user-images.githubusercontent.com/58583277/227646168-1071f237-de95-4f92-ad65-a90ee5fe2b01.mp4


## How To Run The Code
One can run python run.py from inside the Jetson Nano mounted on their car. This will load the model and also detect the motor and begin the purported task of finding a basketball. If no basketball is found, it will remain stationary. The 148remote/ folder contains a cool arduino program for proof of concept. It moves the camera mount through its full range of motion in a rhythmic fashion. 

## Vehicle In Action
[Click Here For Video](https://www.youtube.com/watch?v=0vU6c--l-R4)

## Future Improvements
We can use the Jetson to control the servo motors through the Arduino. We can account for the yaw angle of the camera mount and add that to the steering, so that the car can steer toward targets that is not in the field of view of the camera when the camera is pointing straight forward. We can also improve the precision of the ball-recognition model by using more pictures of the ball to train the model. 
# Team 6: Wall-E (used to be Cyclops)
- Saathvik Dirisala (Data Science)
- Victor Chen (Computer Engineering)
- Yang Song (Mechanical Engineering)
![image](https://user-images.githubusercontent.com/58583277/227645139-397ae17a-582f-4f71-9929-fd08ed245317.png)
