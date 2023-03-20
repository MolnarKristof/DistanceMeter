# A feladat lépései
1. A távolságmérő programozása
    - Távolság -> `distance` változóba
    - Kiírás a képernyőre
2. Mintavételezés kapcsolóval
    - distance -> measuredDistance
    - eseménykezelő készítése ami kattintásra hívja a függvényt
3. measuredDistance -> 7 szegmenses kijelzőre

# 1. A távolságmérő programozása

A megvalósítás kódja: 
```py
import RPi.GPIO as GPIO                    #GPIO library importálása
import time

from gpiozero import CPUTemperature

#Import all board pins.
import board
import busio

# Import the HT16K33 LED segment module.
from adafruit_ht16k33 import segments

# Create the I2C interface.
i2c = busio.I2C(board.SCL, board.SDA)
# Create the LED segment class.
# This creates a 7 segment 4 character display:
display = segments.Seg7x4(i2c)

GPIO.setmode(GPIO.BCM)
#display.marquee("CPU Temperature")
#time.sleep(2)

# Clear the display.
display.fill(0)



#time library importálása
                     #GPIO számozás kiválasztása
GPIO.cleanup()
TRIG = 23                                  #23-as tüske hozzárendelése a TRIG kimenethez
ECHO = 24                                  #24-es tüske hozzárendelése az ECHO bemenethez
print ("Mérés folyamatban")
GPIO.setup(TRIG,GPIO.OUT)                  #Trigger tüske beállítása kimenetnek
GPIO.setup(ECHO,GPIO.IN)                   #Echo tüske beállítása bemenetnek

# Kapcsoló
pinS = 12
GPIO.setup(pinS, GPIO.IN)

# Our function on what to do when the button is pressed
memory = 0


def Save(channel):
    global memory
    global memory
    distance - 0.5
    if distance > 2 and distance < 400:      
        print ("Távolság:",distance - 0.5,"cm")
        
        distanceString = str(distance - 0.5)[:5].ljust(5,"0")                             
        display.print(distanceString) 
        
    else:
        print ("Túl nagy érték!!")

GPIO.add_event_detect(pinS, GPIO.FALLING, callback=Save, bouncetime=500)


distance = 0

try:
    while True:
      GPIO.output(TRIG, False)                
      print ("Várakozás a gomb lenyomására")
      time.sleep(2)                            
      GPIO.output(TRIG, True)                  
      time.sleep(0.00001)                      
      GPIO.output(TRIG, False)                 
      while GPIO.input(ECHO)==0:               
        pulse_start = time.time()              
      while GPIO.input(ECHO)==1:               
        pulse_end = time.time()                 
      pulse_duration = pulse_end - pulse_start 
      distance = pulse_duration * 17150        
      distance = round(distance, 2)            
      #if distance > 2 and distance < 400:      
        #print ("Távolság:",distance - 0.5,"cm")
        
        #distanceString = str(distance - 0.5)[:5].ljust(5,"0")                             
        #display.print(distanceString) 
        
      #else:
        #print ("Túl nagy érték!!") 

except KeyboardInterrupt:
    print("Vége: Pinek lekapcsolva")
    display.fill(0)
    GPIO.cleanup()


```