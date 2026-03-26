Functions and messages, [flow charts, pseudo codes, tables]

Flow Chart
<img width="1920" height="1080" alt="Flowchart of Vehicle-Side Risk Detection and Alert Logic" src="https://github.com/user-attachments/assets/3dbbf06f-2fef-48a4-82d9-68073587573d" />


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


