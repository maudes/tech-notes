---
date: 2026-03-08
categories:
  - Field Notes
  - Standards
  - IoT
  - Matter
---

# Case Study: Matter, from Protocol to Product

My first IoT role was as the platform product manager for WiZ at Signify (formerly Philips Lighting). My mission was to create a robust platform with smooth integration with major smart home systems. One of the key projects was to adopt Matter across our entire product portfolio within a year, bridging the gap by adding integration with the Apple Home ecosystem.

<!-- more -->
Before Matter, WiZ already supported third-party integrations with Google, Alexa, SmartThings, Homey, Mijia, and many others via cloud-to-cloud integration. Yet, due to the complexity and high cost associated with Apple Homekit certification, we never really achieved the integration with Apple Home. 

Matter, therefore, presented a perfect opportunity for us to integrate with the Apple ecosystem naturally and complete  our interoperability puzzle.

Here are my key takeaways from implementing Matter at scale.

***Keywords: #Matter #Signify #NPI #DualStack #ProductStrategy #SmartHome***

## Matter Implementation at a Glance

Adopting Matter is far more than just adding a new API. It's an end-to-end transformation from SDK integration to manufacturing and packaging adjustments.

I still remember vividly that no one in the room had experience managing such a complex program. To make it happen, I printed out the full specifications and all related documentation to map out a clear view of Matter. I joined the CSA working groups, asked countless questions, and drew diagrams that mapped Matter's requirements onto our internal flows for discussion. Working closely with my project manager, Sherry, we mapped out all tasks from end-to-end in the first few months, finally getting the team on track. 

Below is a brief overview of the five key pillars to consider when adopting Matter:

| Workstream | Key Tasks & Deliverables | Objective |
| :--- | :--- | :--- |
| <mark>**Research & Development** |• Chip-level SoC/SDK support<br>• Matter behavior logic definition<br>• SDK integration (strategic coexistence of Matter & brand's own systems) | Ensure protocol compliance while maintaining proprietary brand features. |
| <mark>**Security & Certification** | • Security: PAA setup, DAC issuance, and secure storage<br>• Certification: Collaboration with internal QA, test Labs, partners, and CSA Interop Labs<br>• DCL (Distributed Compliance Ledger) management | Establish device trust and obtain the "passport" for the Matter ecosystem. |
| <mark>**Cloud & Platform**| • Cloud scheme for Matter data sync (across manufacturing, app, and 3rd-party consoles) and data tracking<br> • App flow design: In-field OTA updates and fallback support mechanisms<br>• 3rd party integration: Integration testing, API development, and bulk updates of devices | Ensure seamless data flow, user experience and remote lifecycle management. |
| <mark>**Operations & NPI** | • NPI process alignment<br> • Cloud activation following manufacturing plans and certificate readiness<br>• Manufacturing tooling and test plans for Matter capability verification | Synchronize certification timelines with MP readiness. |
| **Go-to-Market (GTM)** | • GTM resource preparation: Digital assets, cross-platform narratives and standard introduction deck<br>• Packaging design <br>• Training sessions for internal/external partners and FAQ development | Drive market adoption and reduce customer support overhead. |


### Challenge 1: Memory & Performance

#### Memory and resource management
>The initial call was simple "I want to retain our brand identity and special features, but with Matter added on top."

How could we make this happen? The internal discussions shifted from a binary switch approach to coexistence model, to a fully merged architecture. Each had its own strengths. The switch version might seem awkward at first, but it could be a strategic choice for add-on business models, especially given our chipset's memory constraints. Conversely, the fully merged version would require replacing our current foundation with Matter. This could be a viable option to align user experience and improve the efficiency of the low-layer communication.

After weighing all factors including the tight timeline, UX, and business goals, I made the call to adopt the "coexistence (dual stack)" mode. We would support both feature sets at the same time.

This "**dual stack**" design could easily trigger one issue: **memory leaks**. We struggled through optimization as issues surfaced from commissioning to various coexistence scenarios, particularly with Wi-Fi sensing use cases. The team invested a massive amount of time into grooming the architecture, code quality, and potential new libraries for the case. We explored everything from command queueing, original heartbeat design to mDNS discovery coexistence mechanism.

Ultimately, we made it work and passed all certifications. To this day, I'm proud of what we achieved. My key takeaway would be realizing that "Hardware flexibility is inherently limited." Unlike pure software development, in IoT, the physical size and cost of the chipset dictate the boundaries of your software architecture.

### Challenge 2: Stability & Reliability
#### Define the release candidate
The memory issues significantly impacted reliability and stability. Our test results forced us to refine the handling of BLE pairing, which was utilized by both our own pairing flow and Matter device onboarding process. 

Once we tackled the first mile, the next blocker was the "drop-off" issue. During our month-long soak tests, we observed the drop-off issue emerging from time to time. Similar reports emerged from in-field testers according to the partners and our own dogfood testers. The troubleshooting process was not easy as the root cause could be anything from:

* Memory leaks
* Device firmware issues
* Smartphone or home hub issues (OS, app and firmware version)
* Network infrastructure stability
etc. 

One example was we received a "fatal issue" report from our partner, Deutsche Telekom. The report simply stated that "The Matter functionality on iPhone is broken." 

After several rounds of testing and debate, we finally identified that the root cause was on the Apple side. The issue was inconsistent. It affected some iPhone but not others, with no clear pattern regarding region or hardware version. But it was related to the bluetooth component as the commissioning would fail.

I synced with DT and notified Apple, providing testing logs through their tracking system. Eventually, the bug was solved without further explanation from Apple. The case highlights why the complexity and the cost of IoT troubleshooting are so high. To mitigate future risks, I developed a comprehensive testing guide for internal QA use, factory setup and partner troubleshooting.


### Challenge 3: Certification & Factory setup 

#### The chain of trust
Security is one of the key pillars in Matter. The importance of it in IoT is often underestimated. As recent reports on the DJI robotic vacuum vulnerabilities have revealed, those seemingly harmless gadgets could potentially leak house layouts or personal footage to anyone in the world. 
 
To prevent such risks, Matter established a series of rigorous regulations to build a robust "chain of trust". They even collaborated with the US government to align the security requirements for connected devices. 
    
According to the Matter specification, the end-device manufacturers must comply with the following Public Key Infrastructure (PKI) setup:

- **PAA (Product Attestation Authority)**
Manufacturers must possess a PAA certificate and be registered in the **DCL (Distributed Compliance Ledger)**. Companies could choose to maintain a self-built PAA or utilize a third-party trust anchor.
- **PAIs (Product Attestation Intermediate)**
The PAA issues PAIs to different brands or product lines. This is for the flexibility purpose. In our case, we have multiple global brands within the organization. Our self-hosted PAA could issue distinct PKIs for each brand. This also facilitates the Matter deployment to OEM sectors. The separation of PKI makes registration, revocation, and update easier to manage. 
- **DAC (Device Attestation Certificate)**
Each Matter certified end-device has to be flashed with a unique DAC for verification during the commissioning flow. This required tight alignment between our manufacturing schedule and certification process with test labs and the CSA, as our production timeline was extremely sensitive.
- **CD(certification declaration)**
Finally, I would bulk update the certified product data onto the DCL once CDs were issued by CSA.

 ``` mermaid
graph TD
accTitle: Matter DAC Provisioning Flow (Simplified Diagram)

    %% PKI Hierarchy
    CSA[CSA - Root of Trust] --> PAA[PAA]
    PAA --> PAI1["PAI: Brand A (Lighting)"]
    PAA --> PAI2["PAI: Brand B (Sensors)"]

    %% Certificate Management
    subgraph Cloud["PAA/PAI Cloud"]
        PAI1 --> KMS1["Cloud KMS / HSM<br>(Sign DACs)"]
        PAI2 --> KMS2["Cloud KMS / HSM"]
    end

    %% Factory Flow
    subgraph Factory["Factory Provisioning Flow"]
        KMS1 <-- "Auth / Order" --> BU["Brand BU Cloud"]
        BU <-- "Request Provisioning" --> VC["Vendor Cloud<br>(Chip Provider)"]
        
        %% DAC Distribution
        VC -- "Secure Tunnel" --> FL["Production Line Tool<br>(Flash Tool)"]
        
        FL --> DAC1["DAC for Bulb 001"]
        FL --> DAC2["DAC for Bulb 002"]
        
        DAC1 --> Device1["Flashed Chip: Bulb 001"]
        DAC2 --> Device2["Flashed Chip: Bulb 002"]
    end

    %% Styles
    style CSA fill:#f9f,stroke:#333,stroke-width:2px
    style Factory fill:#f5f5f5,stroke:#666,stroke-dasharray: 5 5
    style VC fill:#e1f5fe,stroke:#01579b
 ```

This overall process involves coordinating multiple cloud environments across:

- **PAA cloud**: Issues PAI and DAC
- **BU cloud**: Mapping data between PAA cloud,  manufacturing side and internal schemes
- **Chip vendor cloud**: Connect with the BU cloud for handling secure flashing

It took us almost a full year to finalize a feasible working process with all parties, and integrate it into our NPI process.

#### OTA mechanisms and in-field support

The whole infrastructure with DCL also raised a strategic question: Should we host OTA via the DCL, platform providers, or our own servers? 
 
As a lighting brand with functional end-to-end service, we already maintained our own OTA servers. However, the emergence of Matter introduced a possibility of separating basic Matter capabilities with advanced features. For our private label business, hosting OTA updates through third-party platforms might be a viable business choice. Platforms, like Google, had already introduced the OTA management within their home consoles. This leads back to the core business strategy as a brand or ODM providers have to answer to themselves based on their business goals. 

#### Investment in factory tooling

To comply with the Matter standard, we also had to upgrade our manufacturing tooling. As an early adopter, we had to manage the v1.0 commissioning flow which requires a unique Matter QRcode for each device. This code contains the discriminator, passcode, VID, PID, CertID, etc. required for controllers to verify and establish a communication channel. 
 
To ensure the correct flashing of DAC, CD, and the accurate mapping of internal model IDs to the Matter PIDs, we updated our factory tooling with new logic and accessories. This was essential for verifying the Matter Out-of-the-box (OOTB) experience and ensuring the quality standards were met and aligned on the production line.


## Conclusion
The adventure didn't stop at the factory. While we tackled the major technical blockers, a new set of strategic questions emerged: 
 
- How to design our own app flow for retaining users?
- How to manage the partnerships with platforms such as Alexa, Orange, Home Assistant and Apple?
- How to handle privacy in alignment with GDPR? 
- How do we leverage Matter to seize sales opportunities? 

I'll delve into those topics in the second half of this journey. Stay tuned!

---
### Reference
- [Matter specs](https://csa-iot.org/resources/developer-resources/)
- [mDNS Introduction](https://blog.chrisyuan.me/posts/mdns/)
- [DNS-Based Service Discovery](https://datatracker.ietf.org/doc/html/rfc6763)
- [Multicast DNS](https://datatracker.ietf.org/doc/html/rfc6762)
