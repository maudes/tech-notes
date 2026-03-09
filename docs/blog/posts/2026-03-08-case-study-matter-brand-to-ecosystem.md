---
date: 2026-03-08
categories:
  - Field Notes
  - Standards
  - IoT
  - Matter
---

# Case Study: Matter, from Brand to Ecosystem
In the previous post, I've shared about the firmware development trade-off, the complexity of IoT troubleshooting, and the overall certification process.

<!-- more -->

Now, I'm moving forward to user flows, privacy, partnership management, and new sales opportunities. 


***Keywords: #Matter #Signify #GTM***

## Matter Implementation at a Glance

| Workstream | Key Tasks & Deliverables | Objective |
| :--- | :--- | :--- |
| **Research & Development** |• Chip-level SoC/SDK support<br>• Matter behavior logic definition<br>• SDK integration (strategic coexistence of Matter & brand's own systems) | Ensure protocol compliance while maintaining proprietary brand features. |
| **Security & Certification** | • Security: PAA setup, DAC issuance, and secure storage<br>• Certification: Collaboration with internal QA, test Labs, partners, and CSA Interop Labs<br>• DCL (Distributed Compliance Ledger) management | Establish device trust and obtain the "passport" for the Matter ecosystem. |
|<mark>**Cloud & Platform**| • Cloud scheme for Matter data sync (across manufacturing, app, and 3rd-party consoles) and data tracking<br> • App flow design: In-field OTA updates and fallback support mechanisms<br>• 3rd party integration: Integration testing, API development, and bulk updates of devices | Ensure seamless data flow, user experience and remote lifecycle management. |
 **Operations & NPI** | • NPI process alignment<br> • Cloud activation following manufacturing plans and certificate readiness<br>• Manufacturing tooling and test plans for Matter capability verification | Synchronize certification timelines with MP readiness. |
|<mark> **Go-to-Market (GTM)** | • GTM resource preparation: Digital assets, cross-platform narratives and standard introduction deck<br>• Packaging design <br>• Training sessions for internal/external partners and FAQ development | Drive market adoption and reduce customer support overhead. |


### Challenge 1: UX & Multi-Admin
Apart from the firmware integration, another core topic was to bridge the user experience and data flow via cloud. 

#### The App flow
In the standard Matter workflow, manufacturers often feel invisible since the platform handles most of the user interaction. This raised a critical concern: how do we encourage new users to engage with our app and service? 

Indeed, the request itself is pretty much at odds with the philosophy of Matter. However, maintaining a direct connection with users is vital for hardware brands. Besides requesting "manufacturer-specific" metadata from platform partners, I tackled this challenge through three aspects:

- We position our app as "fail-safe." For instance, if a user loses their physical onboarding QR code, they can always retrieve a digital version by installing the device through our app first.
- We distinguished ourselves by providing advanced light features that Matter v1.0 didn't yet support (same until v1.5). My role was to align with other value stream PMs to revamp our packaging storytelling and e-commerce campaign.
- We kept the legacy design where the factory reset could only be conducted through our app.

I quickly realized the last one was a mistake. I regretted keeping this legacy constraint instead of adopting for instance a more convenient and universal "x-time power cycle" reset method. The original design is fine as users must install devices into our app. Yet, with Matter, users could directly install devices into the selected platform and stay local. 

*Note: The QR code retrieval page wasn't just a standalone feature. It served as a centralized Matter dashboard for existing users to manually trigger Matter commissioning mode for any compatible devices already in their homes.*

#### Privacy under multi-admin scenario
As a global brand, we understand the importance of privacy. I'd deployed the GDPR compliant adjustments to our service. One key thing is having users' consent after presenting the full disclosure policy note at the beginning of the user journey.

Yet, in the IoT scenario, it's getting complex due to the involvement of multiple players. This had been discussed thoroughly with the internal legal team and Matter working group at the time. Since users could install devices directly to any Matter platform, who should be responsible for the user consent and how to manage it. Moreover, Matter could run entirely locally. The information could possibly stay local instead of sharing to the platform. 
 
So far, on the device-end, it'll always include the link or content (depends on manufacturers) of privacy notes in the packaging. If users choose to install devices into the manufacturer's app, it shall show the standard GDPR compliant flow. The same as today. But, if users directly install devices into the platform, the responsibility shifts toward the platform. This is fair when you think of who could collect behavioral or potential PII data. Thus, when users share the device to other admin, supposedly that platform should also gather the user consent. 
 
This might change following the evolution of laws or the technical/ architecture design. However, always keep compliance in mind.


### Challenge 2: Partnerships & New Opportunities

#### Partnership management
By nature, IoT is a collaborative ecosystem. Unlike pure software, it highly depends on network infrastructure and cross-platform interdependence. A common scenario involves a home hub serving as the central controller, connecting diverse devices such as lighting, HVAC, Kitchen appliances and more. In this environment, maintaining  strong relationships with major platforms, Google, Alexa, Apple, and SmartThings, is essential. 
 
As an early Matter adopter, we had an unique opportunity to fine-tune the user experience in direct collaboration with these platforms. During this process, we provisioned hundreds of sample devices to partners for extensive testing phases, including dogfood, alpha, and beta sessions. This collaboration provided us with invaluable feedback on edge cases we might have otherwise overlooked, allowing us to optimize both design and performance. These partnerships enabled a testing scope that would be impossible for a single company to achieve alone. 

Furthermore, engaging at this stage allowed us to influence platform-side design, including the certification workflows (e.g. "Work with Google Home" and "Work with Apple Home" badges etc.), Cloud API adjustments, and home console features that directly benefit our brand. By leveraging these strong relationships, we could also utilize platform-driven marketing to promot our device, creating a win-win situation. 

``` mermaid
graph TD
accTitle: Matter Certification & Production Flow (Simplified)

    %% Certs
    ATL[CSA Authorized Test Labs] -- Pass --> CSA[CSA Certification Flow]
    Others["Wi-Fi / BT / Thread<br>Certification"] -- Pass --> CSA
    
    %% CSA certs
    CSA -- "Issue CD Blob" --> Brand["Manufacturer Cloud"]
    CSA -- Pass --> Plat[CSA Interop Lab Testing]
    
    %% Production line
    subgraph Factory_Process["Factory & Provisioning"]
        Brand -- "Authorize (CD + Model ID)" --> VC["Vendor Cloud<br>(Chip Provider)"]
        VC <--> FL["Production Line Tool<br>(Flash Tool)"]
        
        FL -- "Inject DAC + CD" --> Device["Physical Device<br>(Flashed Chip)"]
    end
    
    %% Platform side
    Brand --> PP2["In-field Updates<br>(OTA with CD)"]
    Plat -- Pass --> Badge["**Platform Badges**<br>e.g.<br> Work with Apple Home"]

    %% Style
    style Brand fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    style VC fill:#fff4dd,stroke:#d4a017
    style Factory_Process fill:#f5f5f5,stroke:#666,stroke-dasharray: 5 5
```

Regarding certification badges: Before Matter, manufacturers had to apply for badges individually through each platform's console. The process typically involved registration, sample preparation, lab testing (or co-test with their internal teams), and finally launching the integration. It was often a tedious, repetitive cycle. With Matter, platforms now allowed manufactures to obtain these badges by simply providing the "pass" results from Matter interop lab. This shift represents a huge relief for manufacturers, significantly streamlining the path to market. 

#### Working Groups in Matter
My team and I had spent considerable time participating in Matter working groups. It is a warm, supportive community that helped us scale our knowledge rapidly. I highly recommond joining these groups. Go for it. It's the best environment to connect with like-minded experts and clarify requirements with the best in the industry. In this section, I'd like to share our experience collaborating with CSA officials. 

The CSA certification framework was initially not as user-firendly as those for Wi-Fi or Bluetooth. As a lighting company, we produce hundreds of SKUs based on the same firmware. However, early policy required each finished product with a distinct form factor to be certified individually. For company as our scale, the certification cost would have been astronomical. To address this,a cross-BU task forces had been formed to research and propose a "Family certification" concept similar to those found in other standards. We successfully convinced CSA to adopt and approve this concept just before our massive manufacturing rollout, resulting in significant cost savings.  

On other occasion, we envountered a situation where the CSA unexpectedly withheld our certification. I immediately formed a squat team once been informed the situation and coordinated with Signify HQ to arrange an emergency sync with the CSA certification group. The issue stemmed from our use of one shared PID across multiple models, which was a strategic decision based on our manufacturing and inventory management. 

> The product was a LED strip with a universal form factor and firmware base. To optimize the inventory allocation and cost efficiency, final assembly with the power supply was dynamically determined based on market orders. Since we could not perdict whether a product will be assigned as a US or EU version during early production, we opted to use a single PID for SKUs across different markets. 

#### New opportunities: EAP and bundle sales
Strong partnerships brought not only media exposure but also strategic opportunities such as collaborating new features through the Early Access Program (EAP). Yet, unlike big tech giants, the manufacturer side typically do not have the same vast development resources. The disparity means that even with a capable team, resources can quickly become overextended.  
 
I would strongly suggest being very cautious before committing to any EAP. I once navigated a challenging situation where the risks I raised were overlooked. It is an experience I do not want others to repeat.

Beyond technical opportunities, I also led the initiatives to get our products FFS-certified (Frustration-Free Setup). This is an critical Alexa certification that ensures a seamless experience for Alexa home users and it is often the prerequisite for significant retail deals on Amazon. 
 
> FFS delivers a seamless OOTB experience where the device is pre-registered to the user's Alexa account upon purchase. The flow requires an unique barcode on the packaging which directly links to that device and its corresponding Matter data. This allows Alexa to automatically discover and commission the device the moment it is powered on. 

Through our close partnership with the Alexa team, we secured the invitation to this program just in time for the Black Friday season. Thanks to the foundation we built for Matter. After reviewing the spec, we excure the following:

- Integrated Alexa-specific fields into our data schemes
- Updated Matter tooling with feature flag for FFS 
- Revised factory testing plan for FFS products
- Adopted the new option within our NPI process
- Updated packaging design for FFS products

This project was a testament to how standardized protocols like Matter can accelerate specialized business opportunities.

### Challenge 3: OEMs
Our BU also supports private label partnerships, where I served as the primary technical point of contact for our clients. Prior to Matter, the sales-technical portion of my role involved outlining our API features and guiding clients through legal and technical onboarding. With the advent of Matter, I became the subject matter expert, helping clients navigate the new standard and identifying potential solutions for their Matter enabled product lines.

Given the intense market interest, I collaborate closely with our business development team. One of Matter's significantly advantages is that the specification was designed with these business models in mind. For example, the CD includes below two optional fields: 

- dac_origin_vid
- dac_origin_pid 

This means, any third-party companies can procure finished products with OEM-data DAC and subsequently update them with CDs containing `dac_origin` fields through the Certification Transfer Program.  
 
However, to sacle a successful OEM/ODM business under Matter, the PKI implementation and high levels of customization support are crucial. At the time, I felt we lack the dedicated resources and specialized capability to fully commit to this sector, as it wasn't our primary business focus. Nevertheless, this remains an area worth exploring, especially as industries like CPEs or small appliances continue to rely heavily on the OEM/ODM model. 

## Conclusion
Thanks for reading. This is the rough story of my Matter journey in those three full years. 

I think the biggest challenge of an IoT PM is it's hard to think in software and hardware's shoes at one time. As a software PM, I highly value the architecture improvement, performance optimization, and user experience. Yet, the hardware side is largely focused on BOM cost, and chipset deals. Numbers matter the most. This would take some time to fully put yourself in both shoes.

Now, I'm in the OEM business which is not famous for encouraging innovation. Yet on the other hand, it forces me to review the industry without the excited geeky rose glasses. I'm still excited about IoT, but understand a bit more on the hardware-centered mindset. 

Stay tuned!

### Related Posts
- [Case Study: Matter, from Protocol to Product](https://maudes.github.io/tech-notes/blog/2026/03/08/case-study-matter-from-protocol-to-product/)

---
### Reference
- [Matter specs](https://csa-iot.org/resources/developer-resources/)
