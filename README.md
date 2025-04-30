#define ML_Ctrl 4     
//define direction control pin of B motor 
#define ML_PWM 5   //define PWM control pin of B motor 
#define MR_Ctrl 2    
//define direction control pin of A motor 
#define MR_PWM 9   //define PWM control pin of A motor 
const int sensor_l = 8;//define the pin of left line tracking sensor 
const int sensor_c = 7;//define the pin of middle line tracking sensor 
const int sensor_r = 11;//define the pin of right line tracking sensor 
int l_val,c_val,r_val;//define these variables 
void setup() { 
Serial.begin(9600);//start serial monitor and set baud rate to 9600 
pinMode(ML_Ctrl, OUTPUT);//set direction control pin of B motor  
pinMode(ML_PWM, OUTPUT);//set PWM control pin of B motor to OUTPUT 
pinMode(MR_Ctrl, OUTPUT);//set direction control pin of A motor to OUTPUT 
pinMode(MR_PWM, OUTPUT);//set PWM control pin of A motor to OUTPUT 
pinMode(sensor_l,INPUT);//set the pins of left line tracking sensor to INPUT 
pinMode(sensor_c,INPUT);//set the pins of middle line tracking sensor to INPUT 
pinMode(sensor_r,INPUT);//set the pins of right line tracking sensor to INPUT 
} 
void loop()  
{ 
tracking(); //run main program 
} 
void tracking() 
{ 
l_val = digitalRead(sensor_l);//read the value of left line tracking sensor 
c_val = digitalRead(sensor_c);//read the value of middle line tracking sensor 
r_val = digitalRead(sensor_r);//read the value of right line tracking sensor 
if(c_val == 1)//if the state of middle one is 1, which means detecting black line 
{ 
front();//car goes forward 
} 
else 
{ 
if((l_val == 1)&&(r_val == 0))//if only left line tracking sensor detects black 
trace 
{ 
} 
left();//car turns left 
else if((l_val == 0)&&(r_val == 1))//if only right line tracking sensor detects black 
trace 
{ 
} 
right();//car turns right 
Page 7 of 10 
else// if left and right line tracking sensors detect black trace or they don’t 
read 
} 
} 
{ 
} 
Stop();//car stops 
void front()//define the status of going forward 
{ 
digitalWrite(ML_Ctrl,HIGH);//set direction control pin of B motor to HIGH 
analogWrite(ML_PWM,60);//set PWM control speed of B motor to 70 
digitalWrite(MR_Ctrl,HIGH);//set direction control pin of A motor to HIGH  
analogWrite(MR_PWM,60);//set PWM control speed of A motor to 70 
} 
void back()//define the state of going back 
{ 
digitalWrite(ML_Ctrl,LOW);//set direction control pin of B motor to LOW 
analogWrite(ML_PWM,60);//set PWM control speed of B motor to 200 
digitalWrite(MR_Ctrl,LOW);//set direction control pin of A motor to LOW 
analogWrite(MR_PWM,60);//set PWM control speed of A motor to 200 
} 
void left()//car turns left 
{ 
digitalWrite(ML_Ctrl,LOW);//set direction control pin of B motor to LOW 
analogWrite(ML_PWM,60);//set PWM control speed of B motor to 200 
digitalWrite(MR_Ctrl,HIGH);//set direction control pin of A motor to HIGH level 
analogWrite(MR_PWM,60);//set PWM control speed of A motor to 200 
} 
void right()//define the right-turning state 
{ 
digitalWrite(ML_Ctrl,HIGH);//set direction control pin of B motor to HIGH level 
analogWrite(ML_PWM,60);//set PWM control speed of B motor to 200 
digitalWrite(MR_Ctrl,LOW);//set direction control pin of A motor to LOW 
analogWrite(MR_PWM,60);//set PWM control speed of A motor to 200 
} 
void Stop()//define the state of stop 
{ 
analogWrite(ML_PWM,0);//set PWM control speed of B motor to 0 
analogWrite(MR_PWM,0);//set PWM control speed of A motor to 0 
}//********************************************************* 
Second Code: 
#define Rpwm_pin 10//enable B 
Page 8 of 10 
#define Lpwm_pin 5//enable A 
int M1_Speed = 80; // speed of motor 1 
int M2_Speed = 80; // speed of motor 2 
int LeftSpeed = 250;  // Left  Speed 
int RightSpeed = 250; // Right Speed 
#define IN1 9 
#define IN2 8 
#define IN3 7 
#define IN4 6 
void setup() {//input output setup 
pinMode(IN1,OUTPUT);//set motors as outputs 
pinMode(IN2,OUTPUT); 
pinMode(IN3,OUTPUT); 
pinMode(IN4,OUTPUT); 
pinMode(Rpwm_pin,OUTPUT);//set enables as outputs 
pinMode(Lpwm_pin,OUTPUT); 
pinMode(A0, INPUT); // initialize Left sensor setup as input 
pinMode(A1, INPUT); // initialize Right sensor setup as input 
} 
void loop() { 
int LS = digitalRead(A0);//reading the value of the left IR sensor 
int RS = digitalRead(A1);//reading the value of the right IR sensor 
if(RS==0 && LS==0) {// if both sensors detect black, the car moves forward 
forward();  
} 
else if(RS==0 && LS==1) {// if only the right sensor detects black, the car moves left 
left(); 
} 
else if(RS==1 && LS==0) {// if only the left sensor detects black, the car moves right 
right(); 
} 
else if(RS==1 && LS==1) {// if both sensors detect white, the car stops 
Stop();  
} 
} 
Page 9 of 10 
// motion controling functions 
void forward() 
{ 
digitalWrite(IN1, HIGH); 
digitalWrite(IN2, LOW); 
digitalWrite(IN3, HIGH); 
digitalWrite(IN4, LOW); 
analogWrite(Rpwm_pin, M1_Speed); 
analogWrite(Lpwm_pin, M2_Speed); 
} 
void backward() 
{ 
digitalWrite(IN1, LOW); 
digitalWrite(IN2, HIGH); 
digitalWrite(IN3, LOW); 
digitalWrite(IN4, HIGH); 
analogWrite(Rpwm_pin, M1_Speed); 
analogWrite(Lpwm_pin, M2_Speed); 
} 
void Stop() 
{ 
digitalWrite(IN1, LOW); 
digitalWrite(IN2, LOW); 
digitalWrite(IN3, LOW); 
digitalWrite(IN4, LOW); 
} 
void right() 
{ 
digitalWrite(IN1, LOW); 
digitalWrite(IN2, HIGH); 
digitalWrite(IN3, HIGH); 
digitalWrite(IN4, LOW); 
analogWrite(Rpwm_pin, LeftSpeed); 
analogWrite(Lpwm_pin, RightSpeed); 
} 
void left() 
{ 
digitalWrite(IN1, HIGH); 
digitalWrite(IN2, LOW); 
digitalWrite(IN3, LOW); 
digitalWrite(IN4, HIGH); 
analogWrite(Rpwm_pin, LeftSpeed); 
analogWrite(Lpwm_pin, RightSpeed); 
}
