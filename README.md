1. Data Capture
    Input source: CCTV cameras installed at each road junction.
    Task: Continuously stream live video feeds from each lane/road
    Details:
    High-mounted cameras capture a wide view of the road.
    Stream resolution optimized for AI processing (e.g., 720p for balance of clarity and speed).

2. Preprocessing
    Objective: Prepare the raw video for AI analysis.
    Steps:
    Extract frames from the live video stream at fixed intervals (e.g., every 1–2 seconds).
    Normalize image size and brightness.
    Apply background subtraction to focus on moving objects (vehicles).
    Optional: Region-of-interest (ROI) masking to analyze only lanes.

3. Vehicle Detection
    AI Model: Use an object detection algorithm like YOLOv8, Faster R-CNN, or SSD.
    Task: Detect and classify vehicles (car, bus, truck, bike, etc.).
    Details:
    Model outputs bounding boxes for each vehicle.
    Detects count per lane in real time.
    Can also classify for special rules (e.g., emergency vehicle detection).

4. Traffic Density Calculation
    Goal: Convert detection results into traffic density metrics.
    Methods:
    Vehicle Count Method: Simply count the number of detected vehicles.
    Area Occupancy Method: Calculate % of lane occupied by vehicles.
    Output: Density level (Low, Medium, High) or numerical count.

5. Signal Timing Decision Logic
    Dynamic Timing Algorithm:
    Assign base green time (e.g., 20 seconds) for all lanes.
    Add extra green time proportionally to the density.
    Prioritize lanes with higher density.
    Ensure minimum red time for other lanes to avoid starvation.
    Example:
    Lane A: 25 vehicles → +15s green
    Lane B: 10 vehicles → base time only
    Lane C: Empty → skip or short green

6. Traffic Light Control
    Hardware Interface:
    AI system sends timing instructions to the traffic light controller (via microcontroller like Raspberry Pi or Arduino, or directly to PLC).
    Operation:
    Signals change according to computed timings.
    The loop repeats continuously (e.g., every 30–60 seconds).

7. Optional Features
    Violation Detection:
    If a vehicle crosses during red → capture license plate (using ANPR).
    Store violation data in database for automatic challan generation.
    Emergency Vehicle Priority:
    If detected, immediately switch to green for its lane.
    Data Logging:
    Save traffic patterns for future planning.
