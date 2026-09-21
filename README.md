# GitHub Challenge

<img src="https://octodex.github.com/images/Professortocat_v2.png" align="right" height="200px" />

Hey there!

Your challenge is ready.
Follow the instructions provided for this challenge and complete the required tasks in this repository.

Make sure your work is committed and pushed to your repository before submission.

Good luck!

---

&copy; 2025 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)
## Task 1:Describe the AIOps scenario

This repository models a simple AIOps workflow for a payment-processing service called payment-service. The service generates operational data such as response time, CPU usage, memory usage, and log events, and the goal is to detect when the service starts degrading before it impacts customers. 
The data in the repository shows periods of normal behavior and a few clear incidents where response times jump, resources spike, and timeout errors appear. 
The major components work together to read the service data, detect abnormal patterns, publish those findings as events, and process them through a lightweight event pipeline. 
AIOps is useful here because it turns noisy operational signals into actionable alerts, helping teams spot service issues early instead of manually reviewing every metric and log entry.

## Task 2: Analyse Logs and Metrics

The repository contains operational telemetry for a payment-processing service. The metric fields are response_time_ms, cpu_percent, and memory_percent, while the log fields are log_level and message. 
The timestamp shows when each record was captured and is used to track changes over time in one-minute intervals. Most records are normal, with low response times, moderate CPU and memory usage, and INFO messages such as “Payment request processed successfully.”
The unusual records are around 10:05 and 10:06, where response time rises to 610–640 ms, CPU reaches 75–94%, memory reaches 70–91%, and ERROR messages such as “Payment service timeout” and “Database connection timeout” appear. 
These values clearly indicate service degradation and a likely operational incident.
## Task 3: Validate Anomaly Detection & Event Streaming Workflow

The anomaly detection workflow processes the operational data and checks each record against the configured thresholds for response time, CPU, memory, and log severity. 
The abnormal records are at 10:05 and 10:06, where response time rises to 610–640 ms, CPU reaches 75–94%, memory reaches 70–91%, and ERROR messages such as “Payment service timeout” and “Database connection timeout” appear. 
The remaining records are normal, with low response times, stable resource usage, and INFO messages such as “Payment request processed successfully.” 
The detection output is clear because it includes both the metric values and the related log message, making it easy to understand why each observation was flagged. No expected anomaly was missed, and no normal event was incorrectly flagged. 
One limitation is that the detection logic depends on fixed thresholds, so it may not adapt well to changing workload patterns or more subtle issues. 
A good improvement would be to use adaptive thresholds or combine multiple metrics over time to reduce false alarms and improve accuracy.

## Task 4: Verify the AIOps Event Flow

The repository simulates a simple event-driven AIOps workflow in which an anomaly is detected from the service telemetry, turned into an event, and then passed through the producer, topic, and consumer before reaching the downstream AIOps component. 
The producer sends the event to the in-memory topic, the topic stores the message, and the consumer reads it and passes it on for processing. In this dataset, the abnormal records at 10:05 and 10:06 are correctly published and consumed as anomaly events, with the event payload retaining the relevant service, timestamp, type, and reasons for the alert. 
This confirms that the workflow works as an end-to-end event pipeline and that each component has a clear role in moving the anomaly signal forward.