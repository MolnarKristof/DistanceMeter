# A feladat lépései
1. A távolságmérő programozása
    - Távolság -> `distance` változóba
    - Kiírás a képernyőre
2. Mintavételezés kapcsolóval
    - distance -> measuredDistance
3. measuredDistance -> 7 szegmenses kijelzőre

# 1. A távolságmérő programozása

A megvalósítás kódja: 
```py
import RPi.GPIO as GPIO                    #GPIO library importálása
import time                                #time library importálása
GPIO.setmode(GPIO.BCM)                     #GPIO számozás kiválasztása 
TRIG = 23                                  #23-as tüske hozzárendelése a TRIG kimenethez
ECHO = 24                                  #24-es tüske hozzárendelése az ECHO bemenethez
print ("Mérés folyamatban")
GPIO.setup(TRIG,GPIO.OUT)                  #Trigger tüske beállítása kimenetnek
GPIO.setup(ECHO,GPIO.IN)                   #Echo tüske beállítása bemenetnek
while True:
  GPIO.output(TRIG, False)                
  print ("Várakozás a szenzorértékre")
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
  if distance > 2 and distance < 400:      
    print ("Távolság:",distance - 0.5,"cm")  
  else:
    print ("Túl nagy érték!!")

                   
```