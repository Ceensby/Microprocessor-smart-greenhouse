<h1>🌿 Smart Greenhouse Control System</h1>

<p>
  This project designs and implements an <b>autonomous Smart Greenhouse Control System</b>
  using <b>two DMC8 (Z80-based) microprocessors</b>. The system simulates soil moisture monitoring
  and automated irrigation in a controlled digital environment.
</p>

<p>
  Communication between the <b>Transmitter (TX)</b> and <b>Receiver (RX)</b> units is achieved using a
  <b>hardware-synchronized Handshake Protocol (Strobe/Busy)</b>, ensuring reliable and lossless data transfer
  even when both processors run asynchronously.
</p>

<hr/>

<h2>1. Introduction</h2>
<p>
  This project demonstrates core concepts of <b>embedded systems</b>, <b>inter-processor communication</b>,
  and <b>microprocessor-based automation</b> through a greenhouse-style control scenario.
</p>

<hr/>

<h2>2. Design Motivation & Scope</h2>
<ul>
  <li>Models a <b>real-world greenhouse automation</b> scenario using low-level microprocessor techniques.</li>
  <li>Automates soil moisture monitoring to reduce manual effort and increase efficiency.</li>
  <li>Implemented as a <b>digital simulation in the DEEDS environment</b>.</li>
  <li>Architecture is suitable for real hardware adaptation with minor modifications.</li>
</ul>

<hr/>

<h2>3. System Architecture & Components</h2>

<h3>Transmitter (TX)</h3>
<ul>
  <li>Simulates a soil moisture sensor by generating incremental <b>8-bit humidity data</b>.</li>
  <li>Manages the <b>Strobe</b> signal to indicate valid data transmission.</li>
</ul>

<h3>Receiver (RX)</h3>
<ul>
  <li>Main control unit of the system.</li>
  <li>Processes incoming data.</li>
  <li>Updates a <b>7-segment display</b> and controls irrigation pump + status LEDs.</li>
</ul>

<h3>Handshake Interface</h3>
<ul>
  <li>Two-wire synchronization mechanism:</li>
  <ul>
    <li><b>Busy line (RX → TX)</b></li>
    <li><b>Strobe line (TX → RX)</b></li>
  </ul>
  <li>Ensures proper timing, data integrity, and collision-free communication.</li>
</ul>

<h3>Monitoring Units</h3>
<ul>
  <li>A <b>Hexadecimal Display</b> connected to the data bus enables real-time monitoring of transmitted values.</li>
</ul>

<hr/>

<h2>4. Communication Protocol (Handshake Mechanism)</h2>

<p>
  To prevent data loss and ensure synchronization, a <b>2-wire handshake protocol</b> is implemented.
</p>

<ol>
  <li><b>Busy Check:</b> TX monitors the Busy line (IA bit 7). If RX is busy, TX waits.</li>
  <li><b>Data Placement:</b> TX places the 8-bit humidity data on the OB port.</li>
  <li><b>Strobe Pulse:</b> TX sets Strobe high for ~0.5 ms using the <code>PTIME</code> delay routine.</li>
  <li><b>RX Reception:</b> RX detects Strobe via polling (IA bit 0), sets Busy to lock the bus, then processes data.</li>
</ol>

<p>
  +This handshake guarantees collision-free, lossless data transfer between both processors.
</p>

<hr/>

<h2>5. Smart Control Logic</h2>

<p>
  The Receiver (RX) evaluates soil moisture using a predefined threshold.
</p>

<ul>
  <li><b>Threshold Value:</b> <code>30h</code> (Decimal 48), approx. 19% of full scale (00h–FFh).</li>
</ul>

<h3>Dry Condition (Humidity &lt; 30h)</h3>
<ul>
  <li>Red LED activated</li>
  <li>Irrigation pump turned ON (OC port bit 0)</li>
</ul>

<h3>Sufficient Condition (Humidity ≥ 30h)</h3>
<ul>
  <li>Green LED activated</li>
  <li>Irrigation pump turned OFF (OC port bit 1)</li>
</ul>

<hr/>

<h2>6. Software Structure & Assembly Implementation</h2>

<ul>
  <li>Developed in <b>Z80 Assembly language</b>.</li>
  <li>Modular design using subroutines such as <code>CREATE</code>, <code>PTIME</code>, and <code>PROCESS</code>.</li>
  <li>Polling-based synchronization ensures reliable operation under timing differences.</li>
  <li>Decision-making logic implemented using comparison instructions like <code>CP 30h</code>.</li>
</ul>

<hr/>

<h2>7. System Reliability & Monitoring</h2>

<ul>
  <li>Hexadecimal display provides real-time visibility of raw transmitted data.</li>
  <li>Status LEDs provide immediate feedback for soil condition and irrigation state.</li>
  <li>These feedback mechanisms help debugging and system validation during simulation.</li>
</ul>

<hr/>

<h2>8. Assembly Coding Quality & Novelty</h2>

<ul>
  <li><b>Modularity:</b> Subroutine usage improves maintainability and readability.</li>
  <li><b>Robustness:</b> Handshake-based synchronization prevents data overwrite.</li>
  <li><b>Novelty:</b> Dual-status LED feedback clearly shows dry vs sufficient moisture conditions.</li>
</ul>

<hr/>

<h2>9. Conclusion</h2>

<p>
  This project successfully demonstrates key principles of <b>inter-processor communication</b>,
  <b>hardware synchronization</b>, and <b>autonomous decision-making</b> in an embedded environment.
  The integration of hardware monitoring and software-driven control logic provides a reliable model
  for smart greenhouse automation.
</p>

<p>
  The system also serves as a strong foundation for future improvements, such as:
</p>

<ul>
  <li>Integrating analog sensors</li>
  <li>Advanced control algorithms</li>
  <li>Real-time hardware implementation</li>
</ul>
