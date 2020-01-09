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
motor2 = Motor(Port.C)

# Initialize thr ColorSensor
sensor = ColorSensor(Port.S2)

robot = DriveBase(motor, motor2, 56, 114)

n = 1

def scan(n):
    while (sensor.reflection() > 17):
        robot.drive_time(0, 5*n, 5000)
        n += 1
        wait(250)
        if (sensor.reflection() <= 17):
            break
        robot.drive_time(0, -5*n, 5000)
        n += 1
        wait(250)
        if (sensor.reflection() <= 17):
            break

while True: 
    if (sensor.reflection() <= 17):
        motor.run(200)
        motor2.run(200)
    else:
        motor.stop(Stop.BRAKE)
        motor2.stop(Stop.BRAKE)
        scan(n)

