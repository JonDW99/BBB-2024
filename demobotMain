#include <kipr/wombat.h>
#include <stdio.h>

#define clawArm 0
#define clawWrist 1
#define clawHand 2
#define leftM 0
#define rightM 3
#define leftS analog(4)
#define rightS analog(5)

void servo(float port, float position){
  set_servo_position(port, position);
}

void wait(float time){
  motor(leftM, 0);
  motor(rightM, 0);
  msleep(time * 1000);
}

void driveS(float speed, float distance){
  clear_motor_position_counter(0);
  while (get_motor_position_counter(0) < distance){
    motor(leftM, speed);
    motor(rightM, speed);
  }
}

void steer(float speedL, float speedR, float distance){
  clear_motor_position_counter(0);
  while (get_motor_position_counter(0) < distance){
    motor(leftM, speedL);
    motor(rightM, speedR);
  }
}

void turn(float degrees){
  clear_motor_position_counter(0);
  clear_motor_position_counter(3);
  if (degrees > 0){ 
    degrees = degrees * 11.6;
    while (get_motor_position_counter(3) < degrees){
      motor(leftM, -50);
      motor(rightM, 50);
    }
  }
  else if (degrees < 0){ 
    degrees = degrees * -11.6; 
    while (get_motor_position_counter(0) < degrees){
      motor(leftM, 50);
      motor(rightM, -50);
    }
  }
}

void slowServo(float port, float position){
  if (get_servo_position(port) < position){
    while (get_servo_position(port) < position){
      float newPos = get_servo_position(port) + 2;
      servo(port, newPos);
      msleep(4);
    }
  }
  else if (get_servo_position(port) > position){
    while (get_servo_position(port) > position){
      float newPos = get_servo_position(port) - 2;
      servo(port, newPos);
      msleep(4);
    }
  }
}

void lineFollow(float speed, float distance){
  clear_motor_position_counter(0);
  clear_motor_position_counter(3);
  int averagePos = 0;
  while (averagePos < distance){
     if ((leftS > 3628) && (rightS > 3628)){
      motor(leftM, speed * .9);
      motor(rightM, speed * .9);
     }
     else if (leftS > 3600){
      motor(leftM, speed*.35);
      motor(rightM, speed);
    }
    else if (rightS > 3600){
      motor(leftM, speed);
      motor(rightM, speed*.35);
    }
    else{
       motor(leftM, speed*.9);
       motor(rightM, speed*.35);
    }
     averagePos = (get_motor_position_counter(0) + get_motor_position_counter(3)) / 2;
  }
}

int main()
{
  //wait_for_light(0);
  //shut_down_in(119);
  	console_clear();
    
  return 0;
}
