# AC-Project
**This is an arduino program that runs to display the output from a Pressure/Humidity/Temperature Sensor on a Serial LCD screen**

I was staying at my brother’s house recently and noticed something screwy. The house has 80’s-era air conditioning….a large unit and one small accessory A/C whirlygig to cool the laundry room and part of the living room. The smaller unit only pumps air to 4 outlet vents, all but one of which were blowing ~room temperature air (NOT cold)

How can we easily hunt down the leaks and save summer by fixing the A/C?

Since one of the 4 vents *is* cold, we know there’s freon and that *cold stuff is leaving the main duct*….so, we can deduce that something in-between the main ducting and the vents is allowing hot bits of air to intermingle and defeat the erstwhile cool intentions of the conditioned air. The attic where the ducts are housed is *HOT* (~120°F), so we can’t stay up there very long

1. Go up there and use your sweaty hand to find where the cold air might be leaking out 
2. Use a PHT sensor https://www.sparkfun.com/products/16298 to hunt down any areas of increased pressure and/or lower temperature
3. Get fancy and visualize the leaks in real-time with a FLIR sensor

Let’s explore the pros/cons of each. 




Pro
Con
#1
Free; requires nothing except some wherewithal and gumption
Attic heat may turn experimenter into a puddle
#2
Fairly simple; will most likely work
Requires a bit amount of know-how (know what to get, how to create code for your use-case)
#3
VERY simple, Most sensitive, nearly guaranteed to work
Expensive


#1 is self-explanatory, moving on the cover details of methods #2 & 3

#2: The PHT sensor I used https://www.sparkfun.com/products/16298 is fairly sensitive, low power, etc…combined it with:

1x MCU (keep in mind this needs to be portable; remember to get a way to power the setup!)
1x Lipo battery
1x Display

My setup was this board https://www.sparkfun.com/products/16829 
with this processor https://www.sparkfun.com/products/16402 
and used this display https://www.sparkfun.com/products/16396 
powered by https://www.sparkfun.com/products/13813  

*NOTE* this is overkill, a simpler setup would also work….you could also use a cheaper temp sensor (like this https://www.sparkfun.com/products/16304) and a cheaper all-in-one board (like this https://www.sparkfun.com/products/15123)

With either build be sure to grab enough qwiic cables https://www.sparkfun.com/products/14426 to connect the products along with any necessary power adapters…

Ambient Attic Temp+Pressure:
![LCD   PHT Ambient](https://user-images.githubusercontent.com/54976031/190316958-43477d89-3117-472c-8b41-8b5e450cf04a.jpg)

Leak Found (lower temp, slightly higher pressure):
![LCD   PHT Leak](https://user-images.githubusercontent.com/54976031/190316989-de1c6fb7-99ad-4ee3-861d-f2ad8478270d.jpg)


#3: All I did was use a FLIR module to “see” the temperature difference in the area, using: 

1x Flir Lepton 2.5 https://www.sparkfun.com/products/16465
1x OpenMV H7+ https://www.sparkfun.com/products/16989
1x  Adapter https://www.sparkfun.com/products/16779

And hooked the module up to a laptop over USB. Software used is the OpenMV IDE, selecting the Lepton example code, which I then modified slightly (the min/max temps determine the colors displayed on-screen for a given temp; I adjusted from the default values to “look” at the range from 50°F to 120°F)



This photo shows the main duct exiting the fan:
![Attic Main Duct Regular Photo](https://user-images.githubusercontent.com/54976031/190316997-b07199d3-bcbc-4ddc-bd8a-f4ba827fb0d3.jpg)

Same view using FLIR setup:


The dark area corresponds to an area of LOW TEMPERATURE.
![Attic Leak Circled](https://user-images.githubusercontent.com/54976031/190316994-7882d294-c178-43c9-bbf5-53075864c8d3.jpg)



Same area from another angle (notice the PHT setup in the foreground as well!):
![Attic Main Duct Cold Spot](https://user-images.githubusercontent.com/54976031/190316996-7e82f164-c5ee-4fb3-aea2-63147d0e9820.jpg)



And Finally this is a FLIR photo *AFTER SEALING THE LEAK* with Aluminum Duct Tape
![Attic Sealed Leak](https://user-images.githubusercontent.com/54976031/190316987-478719a9-980c-4a6d-9d98-52dbcce3d5aa.jpg)


The single cold vent before the repair was the one closest to the fan; it was still transmitting some of the cold air. 


The other 3 vents weren’t getting any cold air because most of it was leaking out right at the beginning of the duct where pressure is the highest and temperature difference is also @ max (worst-case scenario!). After sealing all 4 now blow cold.

So, we came up with 3 ways to solve the same problem at varying price points. The free method might be best if you are flat-broke or aren’t good at things. #2 is affordable but takes some effort…#3 costs a lot, but found the leak in seconds. Ultimately how you would like to create an AC leak detector is entirely up to you, this is just what I came up with.


