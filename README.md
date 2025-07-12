# AutomatedPhoenix - Orchestrating System Resilience

AutomatedPhoenix is a Python-based framework designed to automate the process of system resilience testing and recovery. It provides a comprehensive suite of tools and APIs for injecting faults, monitoring system behavior, and triggering automated recovery procedures. The goal is to proactively identify weaknesses in system architecture and operational procedures, allowing for continuous improvement of system resilience and reduced downtime. Unlike traditional disaster recovery solutions that focus on recovery after a failure, AutomatedPhoenix emphasizes prevention and early detection of potential issues, enabling a more proactive and robust approach to system management.

This framework empowers DevOps teams to perform controlled experiments simulating real-world failure scenarios. By automating these experiments, it becomes possible to regularly test the effectiveness of recovery mechanisms and identify areas for optimization. The framework integrates with various monitoring systems and infrastructure platforms, allowing for a holistic view of system behavior under stress. AutomatedPhoenix supports a wide range of fault injection techniques, including network latency simulation, resource exhaustion, and service disruption, providing a comprehensive testing environment. Furthermore, it allows users to define custom recovery strategies based on specific failure conditions, ensuring that the system can automatically recover from unexpected events.

AutomatedPhoenix aims to bridge the gap between theoretical resilience and practical implementation. It provides a user-friendly interface for designing and executing resilience tests, reducing the complexity of system testing and allowing developers to focus on building more robust applications. Through automated fault injection and recovery, AutomatedPhoenix enables organizations to build confidence in their system's ability to withstand unexpected failures and maintain business continuity. It's designed to be extensible and customizable, allowing integration with existing infrastructure and development workflows. This makes it a valuable asset for any organization looking to improve the reliability and availability of its systems.

## Key Features

*   **Automated Fault Injection:** Injects various types of faults, including network latency, packet loss, CPU exhaustion, memory leaks, and disk I/O errors. Fault injection is performed using the `psutil` library for resource management and network simulation is achieved via traffic control (tc) commands. Configuration is handled via YAML files allowing for easy customization of fault parameters.

*   **Real-time Monitoring Integration:** Integrates with monitoring systems such as Prometheus and Grafana to track system metrics during fault injection. Uses the Prometheus client library to collect custom metrics related to fault injection and recovery processes. Dashboards can be configured in Grafana to visualize system behavior under stress.

*   **Automated Recovery Triggering:** Detects system failures based on predefined thresholds and automatically triggers recovery procedures. Thresholds are defined in configuration files and are evaluated using the `watchdog` library for file system monitoring and custom Python scripts. Recovery procedures can include restarting services, scaling up resources, or rolling back deployments.

*   **Customizable Recovery Scripts:** Allows users to define custom recovery scripts in Python to handle specific failure scenarios. These scripts are executed using the `subprocess` module allowing for interaction with the underlying operating system. The scripts can be version-controlled and managed as part of the application code.

*   **Comprehensive Reporting:** Generates detailed reports on the outcome of resilience tests, including fault injection parameters, system metrics, and recovery performance. Reports are generated in both human-readable (Markdown) and machine-readable (JSON) formats. The reporting system leverages the `jinja2` templating engine for flexible report generation.

*   **API-Driven Interface:** Provides a REST API for programmatically managing fault injection, monitoring, and recovery processes. The API is built using the Flask framework and provides endpoints for creating, starting, stopping, and monitoring resilience tests. API documentation is available in OpenAPI (Swagger) format.

## Technology Stack

*   **Python:** The primary programming language for the framework, providing a flexible and extensible foundation.
*   **Flask:** A lightweight web framework used for building the REST API.
*   **psutil:** A cross-platform library for retrieving system and process information, used for fault injection and resource monitoring.
*   **Prometheus:** A monitoring system for collecting and storing time-series data.
*   **Grafana:** A data visualization tool for creating dashboards and visualizing system metrics.
*   **watchdog:** A library for monitoring file system events, used for detecting configuration changes and triggering recovery procedures.
*   **jinja2:** A templating engine used for generating reports.
*   **PyYAML:** A Python library for reading and writing YAML configuration files.

## Installation

1.  Clone the repository:
    git clone https://github.com/your-username/AutomatedPhoenix.git

2.  Navigate to the project directory:
    cd AutomatedPhoenix

3.  Create a virtual environment:
    python3 -m venv venv

4.  Activate the virtual environment:
    source venv/bin/activate  (Linux/macOS)
    venv\Scripts\activate  (Windows)

5.  Install the required dependencies:
    pip install -r requirements.txt

## Configuration

AutomatedPhoenix relies on several configuration files to define fault injection parameters, monitoring thresholds, and recovery procedures. These files are typically located in the `config` directory.

*   `fault_injection.yaml`: Defines the parameters for fault injection, such as fault type, duration, and target process.

*   `monitoring.yaml`: Specifies the monitoring systems to integrate with, including Prometheus endpoints and Grafana dashboards.

*   `recovery.yaml`: Defines the recovery procedures to execute based on specific failure conditions.

Environment variables:

*   `AP_API_KEY`: API key for accessing the REST API (optional).
*   `AP_PROMETHEUS_URL`: URL of the Prometheus server (required if using Prometheus integration).

## Usage

After installation and configuration, you can start using AutomatedPhoenix to perform resilience tests.

1.  Start the API server:
    python app.py

2.  Access the API documentation at `http://localhost:5000/apidocs` to view available endpoints.

Example: Inject network latency using the API

First, create a fault injection configuration file (e.g., `latency.yaml`):

    fault_type: network_latency
    target_process: my_application
    latency: 100ms
    duration: 60s

Then, use the API to inject the fault:

    curl -X POST -H "Content-Type: application/json" -d @latency.yaml http://localhost:5000/faults

To retrieve the status of the fault injection:

    curl http://localhost:5000/faults/1  (assuming the fault ID is 1)

To stop the fault injection:

    curl -X DELETE http://localhost:5000/faults/1

Custom recovery scripts can be executed by configuring the recovery.yaml with a path to your python script and the trigger conditions.

## Contributing

We welcome contributions to AutomatedPhoenix! Please follow these guidelines:

1.  Fork the repository.
2.  Create a new branch for your feature or bug fix.
3.  Write clear and concise commit messages.
4.  Submit a pull request to the `main` branch.
5.  Include unit tests for your changes.

## License

This project is licensed under the MIT License.

Copyright (c) [Year] [Your Name/Organization]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## Acknowledgements

We would like to thank the open-source community for providing the tools and libraries that make AutomatedPhoenix possible. Specifically, we acknowledge the contributions of the developers of Flask, psutil, Prometheus, Grafana, watchdog, jinja2, and PyYAML.