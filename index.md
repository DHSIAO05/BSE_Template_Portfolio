# Gesture Controlled Car with Accelerometer
I am working on a gesture controlled car using arduino with an esp32 chip

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| David Hsiao | Leland High School | Computer Engineer | Incoming Senior

![Gesture Controlled Car Image](https://bluestampengineering.com/wp-content/uploads/2020/05/edited_qR6z8Gq5H1-6-scaled.jpg)
  
# Final Milestone
My final milestone is the increased reliability and accuracy of my robot. I ameliorated the sagging and fixed the reliability of the finger. As discussed in my second milestone, the arm sags because of weight. I put in a block of wood at the base to hold up the upper arm; this has reverberating positive effects throughout the arm. I also realized that the forearm was getting disconnected from the elbow servo’s horn because of the weight stress on the joint. Now, I make sure to constantly tighten the screws at that joint. 

[![Final Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1612573869/video_to_markdown/images/youtube--F7M7imOVGug-c05b58ac6eb4c4700831b2b3070cd403.jpg )](https://www.youtube.com/watch?v=F7M7imOVGug&feature=emb_logo "Final Milestone"){:target="_blank" rel="noopener"}

# Second Milestone
My second milestone was understanding the accelerometer. I first had to learn how to solder, so I could connect my ESP32 to the accelerometer. Through arduino, I put in a code which shows the acceleration, roatation, and the temperature of the accelerometer. I ran many trials through the accelerometer by tilting it around, seeing which coordinates on the rotations would go up or down if I tilt it in a specific way. Once I figured that out, I wrote a code where when the accelerometer tilts a certain direction, it prints out that corresponding direction. After that, I put in a code through arduino which shows the angle of the accelerometer, which would give it a more specific read. I did the same thing where I ran many trials to see which numbers would go up or down, when the accelerometer is tilted. It printed out with more accurate reads and results compared to the rotations. This is to move the robot, so for example, if I tilt forward with my hand, the robot would move forward. The accelerometer would control the robots movements.

[![Third Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1612574014/video_to_markdown/images/youtube--y3VAmNlER5Y-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=y3VAmNlER5Y&feature=emb_logo "Second Milestone"){:target="_blank" rel="noopener"}
# First Milestone
  

My first milestone was building the car chassis and getting all of my motors to work. I first started off building the car chassis, so screwing in the DC motors in and putting the rubber wheels. I needed to understand all of the components that were used such as the ESP32, L298N Motor Driver, and where all of the wirings should go. I first started with trying to get the two left wheels to work by plugging all of the wires from the ESP32 to the motor driver. I then connected the wires from the motors to the motor drivers and plugged a battery pack to the driver to power it. The L298N Motor Driver is perfect for this because it can handle up to 3A at 35V and allows us to drive four DC motors simultaneously. After, I checked my arduino code, making sure all of the inputs were correct so that the wheels would spin. I then did the same thing for the two right wheels and at first they spun the opposite direction from the two left wheels. I noticed that I had plugged in the wires incorrectly, but I managed to fix it. Finally, I put in the code for the two right wheels, making sure that I had all of my inputs correct corresponding to its wheels, and they all spun in sync. 

[![First Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1626377722/video_to_markdown/images/youtube--TvEqnt8vFWk-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=TvEqnt8vFWk "David's First Milestone"){:target="_blank" rel="noopener"}

**ESP32 to L298N Motor Driver Schematics**
![ESP32 to L298N Motor Driver Schematics](https://i1.wp.com/randomnerdtutorials.com/wp-content/uploads/2018/05/ESP32_1_DC_Motor_bb.png?quality=100&strip=all&ssl=1)

**Motor Code**
```
// Motor A
int motor1Pin1 = 27; 
int motor1Pin2 = 26; 
int enable1Pin = 14;
int motor2Pin1 = 32;
int motor2Pin2 = 33;
int enable2Pin = 25;

// Setting PWM properties
const int freq = 30000;
const int pwmChannel = 0;
const int resolution = 8;
int dutyCycle = 200;

void setup() {
  // sets the pins as outputs:
  pinMode(motor1Pin1, OUTPUT);
  pinMode(motor1Pin2, OUTPUT);
  pinMode(enable1Pin, OUTPUT);
  pinMode(motor2Pin1, OUTPUT);
  pinMode(motor2Pin2, OUTPUT);
  pinMode(enable2Pin, OUTPUT);
  
  // configure LED PWM functionalitites
  ledcSetup(pwmChannel, freq, resolution);
  
  // attach the channel to the GPIO to be controlled
  ledcAttachPin(enable1Pin, pwmChannel);
  ledcAttachPin(enable2Pin, pwmChannel);

  Serial.begin(115200);

  // testing
  Serial.print("Testing DC Motor...");
}
```C++
void loop() {
  // Move the DC motor forward at maximum speed
  Serial.println("Moving Forward");
  digitalWrite(motor1Pin1, LOW);
  digitalWrite(motor1Pin2, HIGH); 
  digitalWrite(motor2Pin1, LOW);
  digitalWrite(motor2Pin2, HIGH); 
  delay(2000);

  // Stop the DC motor
  Serial.println("Motor stopped");
  digitalWrite(motor1Pin1, LOW);
  digitalWrite(motor1Pin2, LOW);
  digitalWrite(motor2Pin1, LOW);
  digitalWrite(motor2Pin2, LOW);
  delay(1000);

  // Move DC motor backwards at maximum speed
  Serial.println("Moving Backwards");
  digitalWrite(motor1Pin1, HIGH);
  digitalWrite(motor1Pin2, LOW); 
  digitalWrite(motor2Pin1, HIGH);
  digitalWrite(motor2Pin2, LOW); 
  delay(2000);

  // Stop the DC motor
  Serial.println("Motor stopped");
  digitalWrite(motor1Pin1, LOW);
  digitalWrite(motor1Pin2, LOW);
  digitalWrite(motor2Pin1, LOW);
  digitalWrite(motor2Pin2, LOW);
  delay(1000);

  // Move DC motor forward with increasing speed
  digitalWrite(motor1Pin1, HIGH);
  digitalWrite(motor1Pin2, LOW);
  digitalWrite(motor2Pin1, HIGH);
  digitalWrite(motor2Pin2, LOW);
  while (dutyCycle <= 255){
    ledcWrite(pwmChannel, dutyCycle);   
    Serial.print("Forward with duty cycle: ");
    Serial.println(dutyCycle);
    dutyCycle = dutyCycle + 5;
    delay(500);
  }
  dutyCycle = 200;
}
```
```
