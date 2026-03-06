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
<p>Current Vehicle-to-Pedestrian solutions relying on onboard sensors are limited by physical obstructions, while smartphone applications suffer from high battery drain and low adoption rates among vulnerable demographics. Our solution is a low-power, dedicated wearable safety tag designed for the safety of pedestrians and drivers alike. Utilizing Cellular LTE/5G protocols, the tag ensures low latency communication (around 1ms) with approaching vehicles. It provides high accuracy location and trajectory tracking and alerting of both driver and pedestrians, emitting a high volume acoustic warning to the pedestrian while simultaneously triggering an alert within the vehicle's dashboard when a high risk trajectory is detected.</p>
<br>

## Literature Review <br>
<p>~200-300 words, require research and reference.</p>
<br>

## Visuals and Diagrams <br>
<p>Flow chart for system logic, architecture diagram, maybe some visual on how the final solution should look like. </p>
<br>

## Reiterations <br>
<ol>
  <li>Drains battery: so we change to a low-footprint and low-power wearable</li>
  <li>May be hard to adopt: as certain demographics may not choose to install/keep updated, therefore we change to wearable</li>
  <li>Communication protocol/location tracking: Standard GNSS not accurate enough, therefore we change to UWB (Centimeter level)</li>
  <li>Broadcasting frequency: High battery drain detected at 10hz broadcasting. Modifying to lower suitable frequency or adaptive frequency based on nearby vehicles.</li>
  <li>False positive? Based on how the solution is designed, high degree of false positive for high risk may be detected (Accuracy? Finetuning of algorithm?)</li>
  <li>Addressing both sides of interaction: Wearable device will also emit a high volume tweet/beep in response to being marked as high-risk.</li>
  <li>Issues with Bluetooth 5.0 for peer to peer communication (Tag-to-Vehicle)</li>
</ol>


## Hardware Parameters <br>
<p>Need research for this section as well. Create a table and fill it in with possible hardware implementations and their respective parameters.</p>
<br>

## AI Usage <br>
<p>Insert AI prompts and responses from Gen AI.</p>
<br>
