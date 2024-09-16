
# FireTracking Optimization

## Overview
This project focused on optimizing real-time video stream processing and executing AI-based fire detection models directly at the source, i.e., as close to the cameras as possible. The project was done in collaboration with Analytics.nc, which specializes in AI-based solutions for wildfire detection in New Caledonia.

## Objective
The main objective was to improve the performance and efficiency of wildfire detection by optimizing the transmission of video streams from cameras located in the forests to Analytics.nc's servers. This involved reducing bandwidth consumption by bringing data processing closer to the source, using **Edge Computing**.

## Tools and Technologies
- **Edge Computing**: Leveraged to process data near the cameras, reducing dependency on public networks and bandwidth issues.
- **NVIDIA Jetson Nano**: Used to deploy the AI model close to the cameras for real-time processing.
- **Rust**: Employed to rewrite parts of the original Python code for enhanced performance and memory management.
- **Docker**: Used to containerize the solution for easier deployment and to ensure compatibility across devices.
- **K3S and Ansible**: Explored for automating deployment and managing updates remotely.

## Project Phases
1. **Code Optimization**: We transcribed Python code to **Rust** to enhance performance and efficiency.
2. **Deployment on Edge Devices**: The optimized code was deployed on **Jetson Nano** using **Docker** containers.
3. **Automation**: We explored automation tools like **K3S** and **Ansible** to manage and update the system remotely.

## Key Challenges
- **Bandwidth Constraints**: Overcoming limited bandwidth when transmitting video streams from remote cameras over public 4G networks.
- **Rust Transcription**: Translating complex Python code to Rust, a low-level programming language, to improve efficiency.
- **Edge Device Deployment**: Ensuring smooth deployment and operation on resource-constrained devices like Jetson Nano.
- **Automation Issues**: Challenges with Kubernetes (K3S) led us to implement **Ansible** for automation.

## Conclusion
This project demonstrated the potential of Edge Computing and AI to optimize resource-intensive tasks like wildfire detection.

## About

For more information, feel free to connect with me on [LinkedIn](https://www.linkedin.com/in/salma-bouaouda-049395265), email me at [bouaouda.salma@gmail.com](mailto:bouaouda.salma@gmail.com), and explore my complete [portfolio](https://salma-svg.github.io/).


