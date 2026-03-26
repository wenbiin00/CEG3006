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
<p>~200-300 words, require research and reference. </p>
<p>Vehicle-to-Pedestrian (V2P) communication has emerged as an important component of intelligent transportation systems aimed at improving the safety of vulnerable road users (VRUs), including pedestrians and cyclists. V2P systems enable vehicles and pedestrians to exchange real-time information such as location, speed, and trajectory to predict potential collisions and provide timely warnings. In Vulnerable Road User Safety Using Mobile Phones with Vehicle-to-VRU Communication, smartphone-based V2P systems are proposed as a practical solution where mobile devices carried by pedestrians communicate with nearby vehicles through wireless V2X networks. These systems allow early detection of dangerous interactions between vehicles and pedestrians and can significantly improve situational awareness for both parties. However, the study highlights limitations including high energy consumption, dependence on smartphone availability, and reduced reliability due to GPS inaccuracies.

Similarly, V2P Collision Warnings for Distracted Pedestrians: A Comparative Study with Traditional Auditory Alerts demonstrates that personalized digital warnings delivered through connected devices can improve pedestrian reaction time compared to conventional auditory alerts such as vehicle horns. While such approaches show promise in enhancing pedestrian safety, current implementations still face several practical challenges.

Many existing V2P solutions rely on onboard vehicle sensors such as cameras, radar, or LiDAR to detect pedestrians. These perception systems may fail in scenarios involving physical obstructions, poor lighting conditions, or non-line-of-sight situations. Meanwhile, smartphone-based applications may suffer from high battery consumption and low adoption rates among vulnerable populations such as children or the elderly.

Therefore, there is a need for alternative V2P solutions that provide reliable, low-latency communication while minimizing power consumption and improving user accessibility. This motivates the development of a dedicated wearable communication device capable of enabling efficient vehicle-pedestrian interaction and enhancing road safety.

References:
(Certad et al., 2025) Certad, N., Del Re, E., Varughese, J., & Olaverri-Monreal, C. (2025). V2P collision warnings for distracted pedestrians: A comparative study with traditional auditory alerts. arXiv. 
https://arxiv.org/abs/2504.13906
(Rashid et al., 2024) Rashid, M., Al-Khateeb, H., Alazab, M., & Alazab, M. (2024). Vulnerable road user safety using mobile phones with vehicle-to-VRU communication. Electronics, 13(2), 331. 
https://www.mdpi.com/2079-9292/13/2/331
</p>
<br>

## Visuals and Diagrams <br>
<p>Flow chart for system logic, architecture diagram, maybe some visual on how the final solution should look like. </p>
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
| BLE | Integrated (nRF5340) | ~100–150 m range, low latency | Vehicle discovery and messaging |
| Buzzer | CUI CMT-8540S-SMT | 100 dBA @ 10 cm, 4 kHz | Audible warning |
| PMIC | Nordic nPM1100 | Li-Po charging, low power | Power management |
| Battery | Li-Po 500–1000 mAh | 3.7 V nominal | Portable power source |

![gnomed](https://github.com/user-attachments/assets/bae9be1b-aced-4336-bc15-5f7f6c166a2d)

## AI Usage <br>
<p>Insert AI prompts and responses from Gen AI.</p>
<br>

## Real-World Case Study <br>
<p>
  
</p>
<br>

## Functions and Messages <br>
<p>
# grab car stats once at startup
host_vehicle = get_vehicle_telemetry() # gets speed, heading, gps
warning_threshold_ttc = 2.5 # threshold for collision warning in seconds
critical_distance = 100.0 # max uwb tracking range in meters

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
    
    # edge case: tag is moving fast and matching our heading (probably a passenger in a car ahead)
    if vru_speed > 30.0 and headings_match(host_vehicle.heading, vru_message.heading):
        flag_as_passenger(vru_message.id)
        continue
        
    # edge case: tag is basically standing still (like waiting at a bus stop)
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
</p>
<br>
