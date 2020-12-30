# Z-WAVE 700 and 500 Series Test Case

syntax: sensor/device [Working/Not working][REASON]

1. Test Case 1: 700 Series Z-Stick with 700 Series device or sensor (US frequency)
    1. Door sensor [Working]
    2. Temperature and humidity sensor [Working][portal UI showing in fahrenheit]
    3. Smart switch [Not working][Able to connect/pair but showing 3 devices on the portal]
2. Test Case 2: 700 Series Z-Stick with 500 Series device or sensor (US frequency)
    1. Door sensor [Working]
    2. Temperature and humidity sensor [Not working][Z-wave portal UI display incorrect sensor type and not showing data]
    3. Smart switch [Not working][Able to connect/pair but showing 3 devices on the portal]
3. Test Case 3: 700 Series Z-Stick with 500 Series device or sensor (Korean frequency)
    1. Door sensor [Working]
    2. Tri sensor [Working]
    3. Smart switch 6 [Working]
    4. NanoMote [Not working][Able to connect/pair but on portal not get data]
    5. smoke detector [Working][Can be connect/pair]
4. Test Case 4: 700 Series Z-Stick with Smart switch 7 (US frequency) and Vesta Hub
    1. PC controller [Working][show 1 device added][binary switch]
    2. Vesta Hub [Not sure][show 3 devices added]
    3. Special test [After adding the smart switch via Vesta Hub, unplug from hub and connect the Z-stick to PC-controller show 3 virtual devices and 1 binary switch]
