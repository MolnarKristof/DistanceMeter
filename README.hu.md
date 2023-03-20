# A feladat lépései

1. A távolságmérő programozása
    - Távolság -> `distance` változóba
    - Kiírás a képernyőre
2. Mintavételezés kapcsolóval
    - Distance -> 'distance'
    - Eseménykezelő készítése ami kattintásra hívja a függvényt
3.  7 szegmenses kijelzőre kiírni a distance értéket
    - Distance értékének kiküldése a 7 szegmenses kijelzőnek
    - Megjelenítés a kijelzőn

# 1. A távolságmérő programozása
Megvalósítás kódja
```py
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

```

# 2. Mintavételezés kapcsolóval

```py
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
```

# 3. 7 szegmenses kijelzőre kiírni a distance értéket

```py
display = segments.Seg7x4(i2c)
```