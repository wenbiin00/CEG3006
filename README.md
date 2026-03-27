# CEG3006 - V2P Group Project

## Group 09 <br>
<ul>
<li>ERIC TAN JUN BOON</li>
<li>ALOYSIUS BAY JIA JING</li>
<li>LIN WEN BIN</li>
<li>DARRENCE LIM JUN AN</li>
<li>NEO YAN MING</li>
</ul>

## Brief Description of Solution <br>
<p>
Current Vehicle-to-Pedestrian (V2P) solutions fall into two broad categories, each with significant drawbacks. Onboard sensor-based systems (cameras, radar and LiDAR) are constrained by line-of-sight requirements 
and fail under occlusion or poor lighting. Smartphone-based V2X applications, while more accessible, suffer from high battery drain and low adoption rates among vulnerable populations such as young children and the elderly.

Our solution is a low-power, dedicated wearable safety tag that addresses these gaps. Using Bluetooth Low Energy (BLE) for vehicle discovery and Ultra-Wideband (UWB) for centimetre-level ranging, the tag continuously estimates
the relative position and trajectory between the pedestrian and approaching vehicles. When a high-risk collision trajectory is detected, it simultaneously triggers an acoustic alert on the wearable and broadcasts a warning to the
vehicle's dashboard unit, ensuring both parties are notified in real time with a combined detection-to-alert latency of under 200ms.

Unlike smartphone-based systems, the tag is a purpose-built device with minimal power draw, designed for all-day wearability without frequent recharging. Unlike sensor-only vehicle systems, it does not rely on line-of-sight and 
remains effective in obstructed or low-visibility environments.

The tag operates adaptively: it remains in a low-power BLE scanning state when no vehicles are nearby and escalates to active UWB ranging when a vehicle is detected. Alert thresholds are tiered: a MEDIUM alert 
(intermittent buzz + dashboard notification) is issued when Time-to-Collision drops below 4 seconds and a HIGH alert (continuous tone + dashboard alarm) when it drops below 2 seconds. This dual-sided alerting makes the system
robust even when one party is distracted, ensuring it serves as a practical and inclusive safety solution for all pedestrian demographics.
</p>
<br>

## Literature Review <br>
<p>Vehicle-to-Pedestrian (V2P) communication has emerged as a key solution for improving the safety of vulnerable road users (VRUs) by enabling real-time information exchange between vehicles and pedestrians. In Vulnerable 
Road User Safety Using Mobile Phones with Vehicle-to-VRU Communication, smartphone-based V2P systems are proposed as a practical approach, where pedestrians use mobile devices to transmit their position and receive safety 
alerts through V2X networks. These systems enhance situational awareness and allow early detection of potential collisions. However, the study highlights several limitations, including high energy consumption, reliance on 
user participation, and reduced positioning accuracy due to GPS constraints. (Rashid et al., 2024)

Similarly, V2P Collision Warnings for Distracted Pedestrians: A Comparative Study with Traditional Auditory Alerts evaluates the effectiveness of V2P warnings compared to conventional auditory signals such as vehicle horns. 
The results show that V2P alerts significantly improve response time, particularly for distracted pedestrians using smartphones, and are more effective in noisy urban environments . This demonstrates the potential of direct 
communication-based safety systems over traditional methods. (Certad et al., 2025)

Despite these advancements, current V2P implementations still face practical challenges. Sensor-based systems relying on cameras, radar, or LiDAR are limited by line-of-sight constraints and may fail in occluded environments,
while smartphone-based approaches suffer from high battery consumption and inconsistent user adoption. These limitations highlight the need for a more reliable and energy-efficient solution.

To address these gaps, this project proposes a low-power, dedicated wearable safety tag that leverages cellular LTE/5G communication to enable low-latency interaction between pedestrians and vehicles. By combining accurate 
trajectory tracking with dual alert mechanisms for both drivers and pedestrians, the proposed system aims to provide a more robust and accessible V2P solution for real-world deployment.

References:
(Certad et al., 2025) Certad, N., Del Re, E., Varughese, J., & Olaverri-Monreal, C. (2025). V2P collision warnings for distracted pedestrians: A comparative study with traditional auditory alerts. arXiv. 
https://arxiv.org/abs/2504.13906
(Rashid et al., 2024) Rashid, M., Al-Khateeb, H., Alazab, M., & Alazab, M. (2024). Vulnerable road user safety using mobile phones with vehicle-to-VRU communication. Electronics, 13(2), 331. 
https://www.mdpi.com/2079-9292/13/2/331
</p>
<br>

## Visuals and Diagrams <br>
<p>Architecture diagram and flow chart for system logic. 
<img width="1292" height="316" alt="image" src="https://github.com/user-attachments/assets/c845a27f-59f0-4e29-8816-103a6632a80e" />
<img width="2385" height="2005" alt="image" src="https://github.com/user-attachments/assets/a604fa07-7518-4ea5-8e87-9b76d8f5fe36" />
</p>
<br>

## Decision Log <br>
<p>
  <li>Drains battery: so we change to a low-footprint and low-power wearable</li>
  <li>May be hard to adopt: as certain demographics may not choose to install/keep updated, therefore we change to wearable</li>
  <li>Communication protocol/location tracking: Standard GNSS not accurate enough, therefore we change to UWB (Centimeter level)</li>
  <li>Broadcasting frequency: High battery drain detected at 10hz broadcasting. Modifying to lower suitable frequency or adaptive frequency based on nearby vehicles.</li>
  <li>False positive? Based on how the solution is designed, high degree of false positive for high risk may be detected (Accuracy? Finetuning of algorithm?)</li>
  <li>Addressing both sides of interaction: Wearable device will also emit a high volume tweet/beep in response to being marked as high-risk.</li>
  <li>Issues with Bluetooth 5.0 for peer to peer communication (Tag-to-Vehicle)</li>
  <li>UWB range is too narrow to detect long range vehicle approach or early collision warning at road scale, so change to GNSS (long range) + UWB (short range)</li>
  <li>User Type Classification: Manual vs. Automatic Gait Analysis</li>
  <li>Privacy vs. Functionality Trade-off in Beacon Payload</li>
</p>
<br>


## Hardware Parameters <br>
<p>Tables below are filled with possible hardware implementations and their respective parameters for our proposed solution.</p>
<br>

| Module | Hardware Component | Selected Device | Function | Specifications | Electrical Specifications |
| --- | --- | --- | --- | --- | --- |
| Processing Unit | Microcontroller | Nordic nRF5340 | Central controller for sensor fusion, communication handling, and alert logic |Dual-core Cortex-M33 (128 MHz), 1 MB Flash, 512 KB RAM, integrated BLE 5.4, ultra-low power modes | V: 1.7–3.6 V, Active: ~5–10 mA, Sleep: ~2–5 µA |
| Positioning Unit | GNSS | u-blox MIA-M10Q | Provides long range global positioning for pedestrian tracking and trajectory estimation | Multi-constellation (GPS, GLONASS, Galileo, BeiDou), ~1.5 m accuracy, up to 10 Hz update rate, ultra-low power | V: 1.8–3.6 V, Active: ~25–30 mW (~8–10 mA @3.3V) |
| Positioning Unit | UWB Module | Qorvo DW3110 | Enables high-precision positioning in close-range conflict zones | 6.0–8.5 GHz, ±10 cm accuracy, up to 6.8 Mbps, low power | V: 2.4–3.6 V, TX: ~60–90 mA, RX: ~50–80 mA |
| Data Processing | Sensor Fusion Module (Software) | Implemented on MCU | Combines GNSS, IMU, and UWB data for accurate positioning and trajectory estimation | Kalman filter / sensor fusion algorithm, real-time processing | Runs on MCU, no additional hardware |
| Decision Logic | Collision Risk Assessment Module (Software) | Implemented on MCU | Evaluates collision risk using trajectory prediction and Time-to-Collision (TTC) calculations | TTC computation, threshold-based risk detection, real-time response | Runs on MCU, minimal additional power |
| Motion Sensing | IMU | Bosch BMI270 | Improves tracking during GNSS signal degradation and supports motion estimation | 6-axis IMU, 50–100 Hz typical sampling, ultra-low power | V: 1.7–3.6 V, Active: ~0.6–1 mA, Low-power: ~100–200 µA |
| Communication Unit (Prototype) | BLE (integrated in MCU) | nRF5340 BLE | Used for vehicle discovery and low-latency beaconing in prototype setup | BLE 5.3/5.4, ~100–150 m range (open field), <20–50 ms latency (target), 100–200 ms advertising interval | TX: ~4–8 mA, RX: ~4–5 mA |
| Communication Unit (Deployment) | C-V2X Transceiver | Quectel AG15 | Direct vehicle-to-pedestrian communication via PC5 sidelink | Low latency (<100 ms), high reliability, ~50–300 m range | ~3.3–5 V, ~200–400 mA active (module dependent) |
| Alert System | Acoustic Buzzer | CUI CMT-8540S-SMT | Provides loud audible warning in urban environments | 4 kHz, up to 100 dBA @ 10 cm, 5 V, ~150 mA | V: 5 V, Current: ~150 mA |
| Alert System | Vibration Motor | Coin Vibration motor | Provides haptic feedback for redundancy and accessibility | 3 V operation, low power | V: 3 V, Current: ~60–100 mA |
| Power Management | PMIC/Charger | Nordic nPM1100 | Ensures stable power delivery and safe battery operation | Li-Po charging (20-400mA), voltage regulation, protection features | Input: 3.7 V battery, Charge: up to 400 mA, Quiescent: ~400 nA |
| Energy | Battery | Li-Po (500–1000 mAh) | Provides sufficient runtime for wearable operation (approx. 12–24 hours typical use) | 3.7 V nominal, rechargeable | Capacity: 500–1000 mAh, Peak current support: >500 mA |
| Antenna System | GNSS Antenna | Ceramic chip antenna | Enables reliable satellite signal reception | Multi-band GNSS support | Passive |
| Antenna System | UWB Antenna | UWB compact antenna | Supports precise ranging performance | 6–8.5 GHz compatible | Passive |
| Antenna System | BLE Antenna | PCB/chip antenna | Enables wireless communication with vehicle system | 2.4GHz | Passive |
| Casing | Wearable Casing | Werable Casing | Ensures portability, durability, and user comfort | <50 × 30 × 12 mm, <25 g, IP54 |
<br>

### Additional Protocols and Parameters:<br>
| Parameters | Value |
| --- | --- |
| GNSS Accuracy | ~1.5 m Circular Error Probability (CEP) |
| UWB Accuracy | +- 10 cm (line of sight) |
| IMU Sampling Rate | 50–100 Hz |
| GNSS Update Rate | 5–10 Hz |
| UWB Update Rate | 5–10 Hz |
| Communication (Prototype) | Bluetooth Low Energy (BLE) |
| BLE Range | ~100–150 m (open environment) |
| BLE Latency | <20–50 ms |
| Communication (Deployment) | Cellular V2X (C-V2X, PC5 sidelink) |
| C-V2X Range | ~50–300 m (urban conditions) |
| C-V2X Latency | <20–100 ms |
| Message Broadcast Rate | ~10 Hz (VRU beacon) |
| Alert Type | Acoustic (buzzer) + Haptic (vibration) |
| Alert Sound Level | ~100 dBA @ 10 cm |
| Power Source | 3.7 V Li-Po battery |
| Battery Capacity | 500–1000 mAh |
| Estimated Battery Life | ~12–24 hours |
| Operating Voltage | 3.3 V system rail (5 V for buzzer) |
| Peak Current Consumption | ~150–250 mA (alert + UWB active) |
| Operating Temperature | −20°C to 60°C |

## AI Usage <br>
<p>Insert AI prompts and responses from Gen AI.</p>
Demonstrate how responsible use of AI tools supported your project work and how you verified the
results. This section should include
• List of used AI tools and how (in which project phases) you have used them
• Examples of prompts and generated outputs [at least 3]
• Examples of identified weaknesses or hallucinations [at least 3]
• Individual reflection and own contributions [approx. 5-10 sentences per team member]

### <ins>**AI tools used:**</ins>
ChatGPT

### <ins>**Prompts and generated outputs:**</ins>
1. What are some ways to improve the safety and comfort of pedestrians, cyclists, or wheelchair users for a Vehicle-to-Pedestrian (V2P) application?<br><br>
<img width="707" height="647" alt="Screenshot 2026-03-27 at 00 22 15" src="https://github.com/user-attachments/assets/570ac5b5-13cf-4174-835b-a0b3f8788677" /> <br>
2. I am designing a Vehicle-to-Pedestrian (V2P) safety system using a wearable tag and V2X communication. The vehicle will perform risk assessment based on distance, blind spot detection, and Time-To-Collision (TTC). Can you guide me on how to structure a flowchart for the vehicle-side decision logic?Suggest the key steps and decision points I should include, such as validation, filtering, and risk evaluation. <br>
**Generated Response**
```
Start with system initialization, where the vehicle-side module sets up V2X communication and prepares to receive wearable tag messages. After that, the first main step should be message reception from the wearable tag.

From there, add a message validation decision point. This checks whether the received V2P message is complete, current, and from a recognized or valid source. If invalid, the logic should discard it and return to waiting for the next message.

If the message is valid, move into a basic filtering stage. This is where the vehicle determines whether the wearable tag is even relevant. Good filtering questions include:

Is the VRU within the vehicle’s detection range?
Is the signal recent enough to use?
Is the VRU in a road-related context rather than far outside the conflict area?

Only if it passes this filtering stage should the logic continue.

Next, include a spatial or geometric risk check. This can evaluate whether the pedestrian is inside the vehicle’s blind spot or projected conflict zone. If not, the system can continue monitoring without triggering an alert.

If the VRU is in a possible danger zone, the next block should be trajectory and motion analysis. Here the system estimates relative movement between the vehicle and the VRU. After that, add a Time-To-Collision (TTC) calculation step.

Then place a decision point such as:

Is TTC below the warning threshold?
Is the collision risk level high enough to justify an alert?

If yes, the flow should proceed to driver alert generation and then send an alert back to the wearable tag. If no, the system should continue monitoring and loop back for the next message.

A good overall order is:
Initialize → Receive Message → Validate → Filter by Range/Relevance → Check Blind Spot/Conflict Zone → Predict Motion → Calculate TTC → Compare Against Threshold → Trigger Alerts / Continue Monitoring

For the actual diagram, use:
- ovals for start/end
- rectangles for processes
- diamonds for yes/no decisions
- arrows for flow direction

A strong extra touch is to make the “no” branches return to a monitoring loop instead of ending, so the system clearly behaves continuously in real time.
```
<br>

3. Does the block diagram consists of all modules and components needed for the wearable to function normally?
<img width="562" height="620" alt="image" src="https://github.com/user-attachments/assets/f9eecfc7-0e57-4709-86cd-cd195bd15f15" />
<img width="500" height="690" alt="image" src="https://github.com/user-attachments/assets/eb26fb85-e1b0-4dd9-a939-aa1275d0481e" />
<img width="780" height="361" alt="image" src="https://github.com/user-attachments/assets/8b90b8f0-fe45-4bd8-a50b-e42ce81c324d" />
<br>



## **Identified weaknesses or hallucinations:**
1. The initial development of the block diagram consisted of incomplete/missing system components, critical to make the wearable function as a whole, hence repeated prompts had to be made to confirm functionality of system.
2. Some of the generated outputs are generic in details, and do not contain the full details unless further prompted.
3. Accuracy of component specifications such as latency, range, consumption may be inaccurate as the values are approximated from values found online, hence specifications are dependent on assumptions and not tied to readily available datasheets.
<br>

## **Reflection and Contribution:** 
<ins>Wenbin</ins> <br>
Working on this V2P wearable tag project significantly deepened my understanding of how automotive safety systems must balance technical performance, user privacy, and practical deployability. 
My primary contribution was conducting extensive research into real-world case studies—from industrial ZoneSafe tags to clinical elderly care systems—which transformed our initial abstract concept
into an evidence-based design grounded in proven technologies, as well as contributing to the development of the project idea and refinement. Through this project, I learned that real-world deployment constraints (cost, 
infrastructure availability, user adoption friction) must be considered as early as technical performance requirements—a lesson learned after initially proposing solutions that were technically sound but economically impractical. 
My key takeaway is that automotive safety systems require balancing multiple competing priorities (performance vs. privacy vs. cost vs. usability), and the most successful designs aren't necessarily 
the most technically advanced but rather those that make strategic trade-offs aligned with real-world constraints. 
<br>

<ins>Yan Ming</ins> <br>
Through working on this project, I learnt more about the V2X communication, how it helps in improving road safety and different types of V2X implementations, particularly V2P. Through literature research, I have also learned about limitations involving existing V2P wearable solution, which involves factors such as battery consumption, position accuracy and that personalized V2P alerts are more effective than traditional auditory warnings, especially for distracted pedestrians, as they provide direct and timely notifications. This project also helped me appreciate the importance of integrating multiple technologies, such as GNSS, IMU, and UWB, to improve positioning reliability, showed me the pros and cons of using C-V2X or BLE and direct or network based connection and how trade offs can archieve a better result for pedestrian safety. I contributed to researching existing V2P solutions for literature review and improvement of initial design.
<br>

<ins>Darrence</ins> <br>
During this project, I gained a deeper understanding of how Vehicle-to-Everything (V2X) communication can be applied to improve pedestrian safety particularly through Vehicle-to-Pedestrian (V2P) systems. I learned how different components such as GNSS, IMU and communication protocols work together to provide real-time positioning and risk detection. One key takeaway for me was how important it is to design systems that go beyond simple distance-based detection as this can lead to a high number of false positives. Instead, incorporating concepts such as blind spot detection, trajectory prediction and Time-To-Collision (TTC) allows for more accurate and reliable safety alerts.I also learned the importance of balancing technical performance with real-world constraints such as cost, power consumption and infrastructure requirements making it more obvious for proper balancing. For example, while technologies like Ultra-Wideband (UWB) offer higher accuracy, they may not always be practical without supporting infrastructure which led us to consider hybrid solutions. Additionally, this project helped me understand how system design is an iterative process where initial ideas are continuously refined based on identified limitations and trade-offs. Overall, this project improved my ability to think critically about system integration and how multiple technologies can be combined to create a more effective and practical solution.
<br>

<ins>Eric</ins> <br>
Working on this Vehicle-to-Pedestrian wearable tag project provided me with useful insights into iterative processes of designing safety-critical automotive systems. My primary contributions involved conducting research on existing V2P solutions to identify gaps and possible improvements, as well as researching specific hardware components to ensure our proposed wearable was feasible in terms of design and economy. I also translated our flowchart into pseudocode and maintained the project decision log to track our chronological records and improvements/changes. Through the hardware selection process and writing the pseudocode, I learned exactly how strict power and latency constraints dictate the system architecture, such as why we had to opt for a BLE and UWB hybrid model instead of a powerful cellular module. Documenting our improvements/changes in the decision log reinforced my understanding that effective engineering is rarely about choosing the most advanced technology possible, but rather making continuous, justifiable refinements to balance performance, cost, and user adoption.
<br>

<ins>Aloysius</ins> <br>
Working on this Vehicle-to-Pedestrian wearable safety tag project broadened my understanding of how embedded systems must be designed with both technical rigour and real-world usability in mind. My primary contributions involved (e.g. designing the BLE communication protocol / researching hardware components / developing the risk assessment algorithm), which gave me hands-on exposure to the trade-offs inherent in low-power wearable design. Through this process, I came to appreciate that decisions rarely exist in isolation, choosing UWB over GPS, for instance, had cascading effects on power budget, hardware cost and firmware complexity that all needed to be reconciled. I also learned how important it is to validate assumptions early; several of our initial design choices, such as fixed 10 Hz BLE broadcasting, had to be revised once their practical limitations became apparent. My key takeaway is that good engineering is less about selecting the most capable technology and more about understanding your constraints deeply enough to make principled, justifiable trade-offs that serve the end user.
<br>

## Real-World Case Study <br>
<p>
  
### USE CASE 1
V2p wearable: ZoneSafe 
A real-world use case of Vehicle-to-Pedestrian (V2P) implementation wearable can be observed in industrial safety systems such as ZoneSafe, where workers wear dedicated proximity tags that communicate with nearby vehicles. 
Forklifts are equipped with detection systems that create a 360-degree safety zone around the vehicle, and when a pedestrian carrying a wearable tag enters this zone, both the driver and the pedestrian receive immediate alerts 
through in-cab warnings and vibrating tags, allowing both parties to react and avoid potential collisions. Notably, the system is capable of detecting pedestrians even in non-line-of-sight conditions, such as behind walls 
or obstacles, improving safety in complex environments. (Forklift Proximity Warning System - ZoneSafe, 2026) However, these systems are typically limited to short-range communication and controlled industrial settings. 
Building upon this concept, the proposed concept extends the wearable V2P approach to urban environments by leveraging LTE/5G communication for low-latency, long-range interaction between pedestrians and vehicles. This 
enables more advanced features such as trajectory prediction and real-time alerts, enhancing safety in dynamic road scenarios.
  
References:
(Forklift Proximity Warning System - ZoneSafe, 2026) Forklift Proximity Warning System - ZoneSafe. (2026, March 19). Zonesafe. 
https://zonesafe.com/proximity-warning-systems/

### USE CASE 2
Scenario: Elementary School Morning Drop-Off (7:45 AM)
8-year-old Emma wears a clip-on safety tag attached to her backpack as she walks to school. The AirTag-sized device contains a BLE 5.0 radio, 9-axis IMU sensor, and LoRaWAN backup.
As Emma approaches the school crosswalk, BLE beacons mounted on lamp posts detect her tag. Her device immediately switches from low-power mode (1 Hz beacon rate) to high-frequency safety mode (10 Hz). The tag vibrates gently: "You're near a road."
A sedan approaching at 40 km/h has a vehicle OBU that receives Emma's BLE beacon. The tag's payload identifies her as: USER_TYPE: CHILD | MOTION: WALKING | BATTERY: 87%.
The driver's dashboard displays: "CHILD DETECTED AHEAD - SLOW TO 25 KM/H"
Emma's tag vibrates twice as the vehicle approaches within 30 meters. Both parties are now aware—dual-alert system active.
Meanwhile, the system uses rotating anonymous IDs (changing every 5 minutes) to prevent tracking, similar to the Seeed Studio school badge that successfully protects student privacy while enabling real-time safety.
If Emma were to fall, her IMU would detect the impact and broadcast an emergency LoRaWAN alert to school staff—just like the fall detection in the airbag belt case study.
Cost per tag: ~$40 | Infrastructure: Existing school zone beacons + BLE modules

References:
Seeed Studio, "Wearable BLE + LoRaWAN Trackers: The Ultimate Hybrid for Seamless Indoor Personal Safety," Seeed Studio Blog, Oct. 17, 2025. [Online]. 
https://www.seeedstudio.com/blog/2025/10/17/wearable-ble-lorawan-trackers-indoor-safety/
</p>
<br>

## Functions and Messages <br>
```<p>
# Pseudocode for Proposed System
# grab car stats once at startup
host_vehicle = get_vehicle_telemetry() # gets vehicle speed, heading, gps
warning_threshold_ttc = 3 # threshold for collision warning in seconds
critical_distance = 100.0 # max tracking range in meters

# keep running while the car is on
while system_is_active:
    
    # grab the incoming uwb beacon 
    vru_message = receive_uwb_beacon()
    
    if not is_valid(vru_message):
        continue # drop bad packets
        
    # figure out how far the tag is right now
    relative_distance = calculate_distance(host_vehicle.position, vru_message.position)
    
    if relative_distance > critical_distance:
        continue
        
    # figure out the tag's speed from its past few pings
    vru_speed = calculate_speed(vru_message.historical_positions)
    
    # edge case where tag is moving fast and matching our heading (maybe a passenger in a car ahead or the same car)
    if vru_speed > 30.0 and headings_match(host_vehicle.heading, vru_message.heading):
        flag_as_passenger(vru_message.id)
        continue
        
    # edge case where tag is basically standing still (like waiting at a bus stop)
    if vru_speed < 0.5:
        flag_as_stationary(vru_message.id)
        continue # just watch them for now, no immediate threat
        
    # project where both the car and the tag are going to be
    vru_path = predict_trajectory(vru_message.position, vru_message.heading, vru_speed)
    vehicle_path = predict_trajectory(host_vehicle.position, host_vehicle.heading, host_vehicle.speed)
    
    # check if these paths cross
    conflict_zone = find_intersection(vru_path, vehicle_path)
    
    if not conflict_zone:
        continue # walking parallel on the pavement, all good

    # danger
    # paths cross, figure out when both parties arrive at the crash point
    ttc_vehicle = calculate_time_to_point(host_vehicle, conflict_zone)
    ttc_vru = calculate_time_to_point(vru_message, conflict_zone)
    
    # find the difference in arrival time
    time_difference = abs(ttc_vehicle - ttc_vru)
    
    # if they arrive within 1 sec of each other and it is happening soon
    if time_difference < 1.0 and ttc_vehicle < warning_threshold_ttc:
        
        # trigger safety systems
        trigger_dashboard_warning("pedestrian collision imminent")
        engage_automated_braking()
        
        # ping the tag back to buzz the pedestrian
        send_alert_to_tag(vru_message.id, "activate_buzzer")
```
</p>
<br>
