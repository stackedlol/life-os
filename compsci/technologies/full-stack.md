---
tags: technologies
---

> breaking down the complete modern tech stack

(updated for May 22nd 2025)

### Layer 1: bare-metal hardware & infrastructure
- physical components

- cpu & [[bare-metal-architecture]]... with the most optimal **RISC-V** processors being at the top of the food chain. Developed at Berkley in 2010, they are open-source and would receive massive improvements from the developer community.

- **CXL** - *Compute Express Link (CXL)*... a high-speed connection standard that links CPU's with memory and accelerators like GPU's... it allows for AI systems to optimize their resources more efficiently. (It is replacing PCIe) 
  
  - **NVIDIA H100 GPU's** - the most powerful graphics processing unit designed for AI and high-performance computing tasks. Contains thousands of cored optimized for parallel processing, with specialized units called tensor cores for AI workloads

- **NVIDIA BlueField-3 SmartNIC** - in modern data centers offloading tasks like encryption, firewall protection, and data compression from the main CPU to the network card can improve performance and efficiency. 

- **Xilinx Alveo U280 FPGA** - is a specialized hardware card designed to accelerate specific computing tasks.... like data analysis or machine learning inference. (crucial for the data and ai surge in the industry )

> provides the **FOUNDATION** and essential resources for all higher-level software and applications to run effectively 

### Layer 2: low-level systems & OS
- operating systems like macos, windows, and linux
- used to manage hardware resources and provide a platform for applications
### Layer 3: backend & middleware
- designed to handle logic and process client-side requests
- 

### Layer 4: Frontend & Applications
- user interface
- design systems
- API consumption
- state management
- deployment 

### Layer 5: deployment and devops
- **docker** - packaging your application and your dependencies into a single unit called a **container**... enables you to consistently run your application (like [[react]] a web app) in development, testing and production environments.

- **kubernetes** - supposed your react app becomes popular, and you need to handle more traffic... **kubernetes** can automatically scale your application by running multiple instances of your docker container. (requests are evenly distributed across all instances )

- 

### layer 6: AI & Edge computing

