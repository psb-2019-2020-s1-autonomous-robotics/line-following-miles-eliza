#!/usr/bin/env pybricks-micropython

from pybricks import ev3brick as brick
from pybricks.ev3devices import (Motor, TouchSensor, ColorSensor,
                                 InfraredSensor, UltrasonicSensor, GyroSensor)
from pybricks.parameters import (Port, Stop, Direction, Button, Color,
                                 SoundFile, ImageFile, Align)
from pybricks.tools import print, wait, StopWatch
from pybricks.robotics import DriveBase

# Initialize a motor
motor = Motor(Port.A)

# Initialize the second motor
motor2 = Motor(Port.D)

# Initialize thr ColorSensor
sensor = ColorSensor(Port.S2)

robot = DriveBase(motor, motor2, 56, 114)

def scan():
    while (sensor.reflection() <= 5):
        robot.drive_time(0, 120, 1000)

while True: 
    if (sensor.reflection() <= 5):
        motor.run(300)
        motor2.run(300)
    else:
        motor.stop(Stop.BRAKE)
        motor2.stop(Stop.BRAKE)
        scan()
