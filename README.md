# CEG3006

## Group 09 <br>
<ul>
<li>ERIC TAN JUN BOON</li>
<li>ALOYSIUS BAY JIA JING</li>
<li>LIN WEN BIN</li>
<li>DARRENCE LIM JUN AN</li>
<li>NEO YAN MING</li>
</ul>

## Brief Description of Solution <br>
<p>Current Vehicle-to-Pedestrian solutions relying on onboard sensors are limited by physical obstructions, while smartphone applications suffer from high battery drain and low adoption rates among vulnerable demographics. Our solution is a low-power, dedicated wearable safety tag designed for the safety of pedestrians and drivers alike. Utilizing BLE protocols, the tag ensures efficient low power communication with approaching vehicles without the use of complicated and high power components. It provides high accuracy location and trajectory tracking and alerting of both driver and pedestrians, emitting a high volume acoustic warning to the pedestrian while simultaneously triggering an alert within the vehicle's dashboard when a high risk trajectory is detected.</p>
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
<p>Architecture diagram, flow chart for system logic, and some visual on how the final solution should look like. 
<img width="2595" height="653" alt="image" src="https://github.com/user-attachments/assets/ab674292-be11-4e8f-a7cb-f39e666c521c" />
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
</p>
<br>


## Hardware Parameters <br>
<p>Need research for this section as well. Create a table and fill it in with possible hardware implementations and their respective parameters.</p>
<br>

| Component | Selected Device | Key Specs | Purpose |
|---|---|---|---|
| MCU | Nordic nRF5340 | Dual-core Cortex-M33, 128 MHz, 1 MB Flash, BLE 5.4 | Main controller for processing and communication |
| GNSS Module | u-blox MIA-M10Q | Multi-GNSS, ~1.5 m accuracy, 5–10 Hz update | Provides global positioning |
| UWB Module | Qorvo DW3110 | ±10 cm accuracy, up to 6.8 Mbps | Enables short-range precision tracking |
| IMU | Bosch BMI270 | 6-axis, low power, 50–100 Hz sampling | Supports motion tracking |
| Communication (Prototype) | BLE (nRF5340) | ~100–150 m range, low latency | Used for vehicle discovery and messaging |
| Communication (Deployment) | C-V2X Transceiver (e.g., Quectel AG15) | PC5 sidelink, low latency (<100 ms), high reliability | Enables direct vehicle-to-pedestrian communication |
| Buzzer | CUI CMT-8540S-SMT | 100 dBA @ 10 cm, 4 kHz | Audible warning |
| Vibration Motor | Coin motor | 3 V operation | Provides haptic feedback |
| PMIC | Nordic nPM1100 | Li-Po charging, low power | Power management |
| Battery | Li-Po 500–1000 mAh | 3.7 V nominal | Portable power source |

## AI Usage <br>
<p>Insert AI prompts and responses from Gen AI.</p>
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
