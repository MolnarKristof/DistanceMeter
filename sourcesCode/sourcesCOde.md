# 1. A távolságmérő programozása

A megvalósítás kódja: 
```py
import RPi.GPIO as GPIO                    #GPIO library importálása
import time



# Importálja az összes board pint
import board
import busio

# Importálja a HT16K33 LED segments modult
from adafruit_ht16k33 import segments

# Megcsinálja az I2C felületet
i2c = busio.I2C(board.SCL, board.SDA)
# Megcsinálja a kijelző változóját
display = segments.Seg7x4(i2c)

GPIO.setmode(GPIO.BCM)


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

# A megmért távolságot lekéri a gombnyomás után és kiírja a képernyőre

def Save(channel):
    distance - 0.5
    if distance > 2 and distance < 400:      
        print ("Távolság:",distance - 0.5,"cm")
        
        distanceString = str(distance - 0.5)[:5].ljust(5,"0")                             
        display.print(distanceString) 
        
    else:
        print ("Túl nagy érték!!")

GPIO.add_event_detect(pinS, GPIO.FALLING, callback=Save, bouncetime=500)


# Távolság mérése

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


# Program leállítása 

except KeyboardInterrupt:
    print("Távolság mérő kikapcsolva")
    display.fill(0)
    GPIO.cleanup()


```