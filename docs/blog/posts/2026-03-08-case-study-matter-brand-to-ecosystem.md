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

#### ＊The App flow
In the standard Matter workflow, manufacturers often feel invisible since the platform handles most of the user interaction. This raised a critical concern: how do we encourage new users to engage with our app and service? 

Indeed, the request itself is pretty much at odds with the philosophy of Matter. However, maintaining a direct connection with users is vital for hardware brands. Besides requesting "manufacturer-specific" metadata from platform partners, I tackled this challenge through three aspects:

- We position our app as "fail-safe." For instance, if a user loses their physical onboarding QR code, they can always retrieve a digital version by installing the device through our app first.
- We distinguished ourselves by providing advanced light features that Matter v1.0 didn't yet support (same until v1.5). My role was to align with other value stream PMs to revamp our packaging storytelling and e-commerce campaign.
- We kept the legacy design where the factory reset could only be conducted through our app.

I quickly realized the last one was a mistake. I regretted keeping this legacy constraint instead of adopting for instance a more convenient and universal "x-time power cycle" reset method. The original design is fine as users must install devices into our app. Yet, with Matter, users could directly install devices into the selected platform and stay local. 

*Note: The QR code retrieval page wasn't just a standalone feature. It served as a centralized Matter dashboard for existing users to manually trigger Matter commissioning mode for any compatible devices already in their homes.*

#### ＊Privacy under multi-admin scenario
As a global brand, we understand the importance of privacy. I'd deployed the GDPR compliant adjustments to our service. One key thing is having users' consent after presenting the full disclosure policy note at the beginning of the user journey.

Yet, in the IoT scenario, it's getting complex due to the involvement of multiple players. This had been discussed thoroughly with the internal legal team and Matter working group at the time. Since users could install devices directly to any Matter platform, who should be responsible for the user consent and how to manage it. Moreover, Matter could run entirely locally. The information could possibly stay local instead of sharing to the platform. 
 
So far, on the device-end, it'll always include the link or content (depends on manufacturers) of privacy notes in the packaging. If users choose to install devices into the manufacturer's app, it shall show the standard GDPR compliant flow. The same as today. But, if users directly install devices into the platform, the responsibility shifts toward the platform. This is fair when you think of who could collect behavioral or potential PII data. Thus, when users share the device to other admin, supposedly that platform should also gather the user consent. 
 
This might change following the evolution of laws or the technical/ architecture design. However, always keep compliance in mind.


### Challenge 2: Partnerships & New Opportunities

#### ＊Partnership management
By nature, IoT is a multi-player game. Unlike pure software, it highly depends on network infrastructure and cross-platform coordination. A common scenario involves a home hub serving as the central controller, connecting devices like lighting, HVAC, Kitchen appliances and more. In this case, we would need to maintain good relationships with platforms. The major four are Google, Alexa, Apple, and SmartThings. 
 
As an early Matter adopter, we had a great chance to together fine tune the experience with those platforms. During the process, we even provisioned hundreds of sample devices to partners for multiple rounds of tests, alpha, beta or dogfood, you name it. By doing so, we gained valuable test results on issues we may have ignored, and helped us optimize the design and performance. The partnerships supported us to reach the ideal testing scope that one company may not reach.

Additionally, the partnership at this stage allowed us to impact the design on the platform side, including the certification flow (e.g. Work with Google Home, Work with Apple home badges etc.), adjustments of the existing cloud API, and home console features that may benefit us. Following the good relationship, we could also leverage the power of platforms to promote our products. It was mostly a win-win situation. 

One point in terms of the certification badges. Before Matter, manufacturers had to apply for it one by one on each platform console. The process included: registration, testing (via labs or co-test with their cert team. It depends.), and launch the integration. It was often a tedious, repetitive process. But with Matter, now all of them allow manufactures to gain those badges by providing the "pass" testing results from Matter interop lab. That will be a great relief for manufacturers.  

#### ＊New opportunities: EAP and bundle sales
The good relationships brought media exposure and potential new opportunities. One thing was having the chance to collaborate on new cool features through their Early Access Program (EAP). Yet, unlike those big tech giants, the manufacturer side normally won't have a big development team as they do. This indicated the capable resources might usually be insufficient. 
 
I would strongly suggest being very careful before agreeing on any EAP. I once navigated a challenging situation where the risks I raised were overlooked. You would not want to experience that.

In addition to technical related opportunities, I also had a chance to make our product FFS-certified (Frustration-Free Setup). It's an important certification program from the Alexa side that provides a seamless integration for Alexa home users. And, it's the ticket for any potential real deals on Amazon. 
 
> FFS allows a seamless OOTB experience where the device is pre-registered to the user's Alexa account upon purchase. The flow requires an unique barcode on the packaging which directly links to that device and its corresponding Matter data. That's how Alexa could find and commission the device once it's power-on. 

Through our close partnership with the Alexa team, we secured the invitation to this program just in time for the Black Friday season. Thanks to the foundation we built for Matter. After reviewing their spec, we simply:
- Integrated Alexa-specific fields into our data schemes
- Updated Matter tooling with feature flag for FFS 
- Revised factory testing plan for FFS products
- Adopted the new option within our NPI process
- Updated packaging design for FFS products

This project was a testament to how standardized protocols like Matter can accelerate specialized business opportunities.

### Challenge 3: OEMs
Our BU also supports private label business. So, I had a chance to be the technical contact to our clients. Before Matter, my job was sharing our API features and scope, then guiding them through the legal and technical process. With Matter, I was the go-to guy for clients to understand the standard and potential packages of their own Matter product lines.
 
#### ＊OEMs
Our clients surely wanted to know more about Matter. In this case, I spent quite some time developing the technical sales deck with our BD team. 

The pros of Matter is they had the spec prepare for this. For example, in CD, there are two option fields: 

- dac_origin_vid
- dac_origin_pid 

This means, any third-party companies can buy finished products with OEM-data flashed DAC and update with CDs having dac_origin fields through Certification Transfer Program afterwards.  
 
Yet, to do a proper OEM/ODM business, the implementation of PKI and support for customization are crucial. I didn't think we had enough resources and capability at the time. Plus, this sector was not exactly our focus as a business. But, it's worth digging considering industries like CPEs or small appliances have heavily relied on the OEM/ODM model. 


## Conclusion
Thanks for reading. This is the rough story of my Matter journey in those three full years. 

I think the biggest challenge of an IoT PM is it's hard to think in software and hardware's shoes at one time. As a software PM, I highly value the architecture improvement, performance optimization, and user experience. Yet, the hardware side is largely focused on BOM cost, and chipset deals. Numbers matter the most. This would take some time to fully put yourself in both shoes.

Now, I'm in the OEM business which is not famous for encouraging innovation. Yet on the other hand, it forces me to review the industry without the excited geeky rose glasses. I'm still excited about IoT, but understand a bit more on the hardware-centered mindset. 

Stay tuned!

---
### Reference
- [Matter specs](https://csa-iot.org/resources/developer-resources/)
