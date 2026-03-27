Demonstrate how responsible use of AI tools supported your project work and how you verified the
results. This section should include
• List of used AI tools and how (in which project phases) you have used them
• Examples of prompts and generated outputs [at least 3]
• Examples of identified weaknesses or hallucinations [at least 3]
• Individual reflection and own contributions [approx. 5-10 sentences per team member]

## **AI tools used:**
ChatGPT

## **Prompts and generated outputs:**
1. What are some ways to improve the safety and comfort of pedestrians, cyclists, or wheelchair users for a Vehicle-to-Pedestrian (V2P) application? <br>
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
<ins>wenbin</ins> <br>
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
