# GitHub Challenge

<img src="https://octodex.github.com/images/Professortocat_v2.png" align="right" height="200px" />

Hey there!

Your challenge is ready.
Follow the instructions provided for this challenge and complete the required tasks in this repository.

Make sure your work is committed and pushed to your repository before submission.

Good luck!

---

&copy; 2025 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)

TASK 1:
## AIOps scenario
This repository models a lightweight AIOps workflow for a payment-processing service called `payment-service`. The service continuously emits operational telemetry, including request latency, CPU usage, memory usage, and log messages. The challenge is to detect when a healthy service begins to degrade and to convert those signals into actionable operational events.

## Service being monitored
The service under observation is a transaction-processing application that must stay responsive and reliable for customer requests. In normal operation, it handles requests with low latency and stable resource usage. During degraded states, it begins to show increased response times, elevated resource utilization, and timeout-related error events that can impact customers if not caught early.

## Operational problem being addressed
The operational issue is intermittent service degradation and failure under load. The telemetry may show partial indicators of trouble before a full outage occurs, such as slow response times, abnormal CPU or memory consumption, and error logs indicating timeouts or connection problems. This project simulates the real-world need for proactive detection and alerting before reliability issues become user-visible incidents.

## Purpose of the major components
- `data/service_data.json`: contains the operational data used by the workflow. It represents the raw signals the system monitors from the service.
- `src/anomaly_detector.py`: analyzes the service metrics and log levels to identify abnormal behavior. Its job is to detect likely incidents such as high latency, high resource consumption, and error events.
- `src/event_producer.py`: takes detected anomalies and publishes them as structured events so they can be handled by downstream processing.
- `src/event_topic.py`: simulates a message topic or event stream, providing an in-memory channel for passing events between producers and consumers.
- `src/event_consumer.py`: receives events from the topic so that processed anomalies can be observed or acted on as part of the workflow.
- `src/aiops_pipeline.py`: ties the workflow together by loading the operational data, running the anomaly detection logic, publishing events, and consuming the results.

## Why AIOps is used here
AIOps is used to turn noisy operational data into a smaller set of meaningful signals. Instead of manually reading every metric and log record, the system correlates telemetry, identifies patterns that look abnormal, and turns those findings into event-driven alerts. In this assessment, the goal is to simulate a practical AIOps pattern: monitor service health, detect degradation, and surface incidents through an event pipeline.


## Task 2: Analyse Logs and Metrics

The repository contains operational telemetry for a payment-processing service. The metric fields are response_time_ms, cpu_percent, and memory_percent, while the log fields are log_level and message. 
The timestamp shows when each record was captured and is used to track changes over time in one-minute intervals. Most records are normal, with low response times, moderate CPU and memory usage, and INFO messages such as “Payment request processed successfully.”
The unusual records are around 10:05 and 10:06, where response time rises to 610–640 ms, CPU reaches 75–94%, memory reaches 70–91%, and ERROR messages such as “Payment service timeout” and “Database connection timeout” appear. 
These values clearly indicate service degradation and a likely operational incident.
## Task 3: Validate Anomaly Detection & Event Streaming Workflow

The anomaly detection workflow processes the operational data and checks each record against the configured thresholds for response time, CPU, memory, and log severity. The abnormal records are at 10:05 and 10:06, where response time rises to 610–640 ms, CPU reaches 75–94%, memory reaches 70–91%, and ERROR messages such as “Payment service timeout” and “Database connection timeout” appear. The remaining records are normal, with low response times, stable resource usage, and INFO messages such as “Payment request processed successfully.” The detection output is clear because it includes both the metric values and the related log message, making it easy to understand why each observation was flagged. No expected anomaly was missed, and no normal event was incorrectly flagged. 
One limitation is that the detection logic depends on fixed thresholds, so it may not adapt well to changing workload patterns or more subtle issues. 
A good improvement would be to use adaptive thresholds or combine multiple metrics over time to reduce false alarms and improve accuracy.