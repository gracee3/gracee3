# Emmy Grace Clark

[← Profile](./README.md) · [Technical portfolio](./portfolio.md)

Washington, DC | emmygraceclark@gmail.com | [github.com/gracee3](https://github.com/gracee3)

## Professional Summary

Technical subject-matter expert, solutions architect, and software engineer with 15+ years of professional experience spanning software development, AI evaluation, observability, compliance, data platforms, and infrastructure across enterprise, healthcare, and federal environments. Former remote SHL/Brainbench assessment author who created and validated more than 150 scenario-based Apple technical questions, code exercises, performance tasks, and multimedia simulations. Later served as Virtustream's monitoring product owner and principal technical architect within Dell Technologies, earning two promotions and multiple awards while working directly with engineering, management, audit, and executive stakeholders. Linux and open-source systems practitioner since 2004, with current public research in local AI inference, automatic speech recognition, Rust systems, hardware-aware optimization, and reproducible evaluation.

## Independent Research & Open-Source Engineering

**Public portfolio:** [github.com/gracee3](https://github.com/gracee3) | **2026-Present**

- **[native-asr](https://github.com/gracee3/native-asr) - CPU-only speech recognition and evaluation:** Designed two offline x86-64 Linux workflows for consumer-grade hardware: a deterministic long-form ensemble combining NeMo Parakeet TDT v3, Sherpa Parakeet Unified, and whisper.cpp `small.en`; and a low-latency streaming cascade using Nemotron provisional text with NeMo Parakeet authoritative phrase correction. Built reproducible WER/RTF harnesses, model and dataset locks, privacy-preserving offline containers, failure gates, and provenance-complete audit artifacts.
- Measured the long-form consensus at 1.78% WER on LibriSpeech `test-clean` and 3.28% on `test-other` deterministic 100-utterance snapshots, improving upon the best constituent in each split. Validated real-time PipeWire-loopback streaming on an 11th Gen Intel Core i5-1145G7 at 4.35%/6.17% committed WER, approximately 1.001 RTF, zero degraded segments, and no more than 142 ms p95 partial latency.
- **[qwen38-int8-lab](https://github.com/gracee3/qwen38-int8-lab) - architecture-aware LLM quantization and validation:** Built a Docker-first lab that converted the official Qwen3.8-27B BF16 checkpoint into a self-contained 36.8 GB W8A8 INT8 candidate for dual RTX 3090 inference. Designed a conservative 256-projection text quantization policy while preserving embeddings, `lm_head`, Gated DeltaNet/recurrent paths, vision components, normalization, and 15 MTP tensors; implemented guarded calibration, checkpoint-integrity validation, resource telemetry, deterministic generation tests, and fail-closed evidence publication.
- Validated vLLM tensor parallelism across both GPUs with native `CompressedTensorsW8A8Int8` to `CutlassInt8ScaledMMLinearKernel` dispatch. The functional candidate measured 0.608-second median TTFT, approximately 1,897 client-observed prefill tokens/second, and 10.41 decode tokens/second; standardized paired accuracy evaluation remains a separately reported gate.
- **[whisperX-batch](https://github.com/gracee3/whisperX-batch) - GPU batch transcription and benchmarking:** Developing a Docker-first WhisperX control plane with a pinned CUDA 12.8/Torch 2.8 core stack, explicit single-GPU sharding, offline cache behavior, resume semantics, bounded command construction, parameter sweeps, WER/RTF/tokens-per-second measurement, and optional GPU telemetry. A fresh LibriSpeech `dev`/`test` benchmark campaign is in progress; historical observations are not presented as comparative results without complete evidence.
- **[gpt-oss-rs](https://github.com/gracee3/gpt-oss-rs) - Rust-native inference research:** Developed and evaluated CPU-first GPT-OSS 20B execution with scalar, AVX2, AVX-512/VNNI, and capability-selected kernel paths, exact-bit equivalence gates, mapped checkpoints, versioned repack caches, and reproducible evidence bundles. Archived heterogeneous research demonstrated bounded end-to-end 20B execution across CPU, GPU0, and GPU1 while preserving failed gates and negative results rather than overstating incomplete 120B or performance work.
- **[supermicro-observability](https://github.com/gracee3/supermicro-observability) - secure hardware observability:** Translated enterprise monitoring experience into a portable containerized stack for Linux hosts, NVIDIA GPUs, SMART, fan telemetry, and container resources. Implemented 250 ms persistent GPU sampling, Prometheus/Grafana provisioning, hardened loopback-first defaults, optional systemd installation, bounded JSON observations, and a local MCP interface for automated evaluation and agent workflows.
- **[digital-liquid-light-lab](https://github.com/gracee3/digital-liquid-light-lab) - GPU-first real-time simulation:** Designing a performable digital liquid-light instrument in Rust, `wgpu`, and WGSL with explicit simulation, material, optics, interaction, and evidence boundaries. Completed the Stage 0 native Vulkan platform proof and am specifying a bounded 2.5D thin-layer solver and thickness-based optics for responsive RTX-3090-class execution, with future projector, gyro, touch, audio, and MIDI control kept behind device-neutral interfaces.
- **[Mirabile](https://github.com/gracee3/mirabile) - local-first Rust web application:** Building a pre-MVP Rust and Leptos 0.8 CSR/WASM application with a provider-neutral calculation engine, revisioned repository contracts, IndexedDB persistence, Web Worker execution, derived-state projection, and native plus headless-Chromium verification.
- **[Magnolia](https://github.com/gracee3/magnolia) - modular real-time signal processing:** Researching a Rust microkernel and patch-bay runtime for modular DSP, lock-free SPSC audio paths, dynamically loaded plugins, sandboxing, Ed25519 verification, Nannou visualization, and local streaming-caption workflows.

## Professional Experience

### Virtustream (Dell Technologies) - McLean, Virginia

**Advisor, Data Intelligence Engineer → Senior Advisor, IT Infrastructure → Consultant, IT Infrastructure** | **2018-2025**

*Functional role: Monitoring and Compliance Solutions Architect; technical product owner and principal architect*

Enterprise cloud and managed-colocation provider acquired by EMC for approximately $1.2 billion in 2015 and subsequently integrated into Dell Technologies, serving mission-critical enterprise, federal, and Epic healthcare environments through Virtustream Enterprise Cloud, Federal Cloud, and Healthcare Cloud services.

- Served as technical product owner and principal architect for global monitoring and compliance, owning architecture, technical priorities, operational standards, cross-functional requirements, and executive-facing strategy; promoted twice and recognized with multiple Inspire Awards, including Dell Technologies' "Game Changer."
- Supported Virtustream's Epic-certified Healthcare Cloud business, operating large national healthcare-system environments within a managed-colocation footprint representing more than $100 million in hosted business and later supporting the Rackspace handoff across hardware, vCenter, VM, and application layers.
- Architected and deployed a scalable global monitoring stack across 15 multi-tenant colocation sites, ingesting 2,000-5,000 metrics per second per site and integrating Zabbix, ServiceNow, and Grafana for automated real-time alerting and SLA assurance across more than 7,500 VMs and thousands of physical devices.
- Led Virtustream's Metrics Archive across architecture, operations, maintenance, secure decommissioning, and migration of a four-cabinet Apache HBase/Hadoop HDFS/Fluentd cluster - approximately 1 PB and geo-replicated between Durham, North Carolina, and St. George, Utah - into Google BigQuery for time-series analytics, improving security and eliminating legacy licensing for $2 million in annual savings from 2022 through 2024.
- Architected and delivered a net-new FedRAMP High GCP extension for Virtustream Federal Cloud, partnering with Google to move the Metrics Archive from managed colocation into the cloud while maintaining parity with on-premises controls, mapping NIST SP 800-53 requirements, co-authoring the SSP and POA&M, and leading 3PAO evidence through a first-pass JAB Provisional Authorization to Operate.
- Resolved a longstanding vCenter API performance constraint across the data-center footprint by modernizing the monitoring stack with Zabbix upgrades, Prometheus, custom exporters, Podman, RHEL 7/8 systems, and a fault-tolerant kube-prometheus deployment on K3s, reducing scrape load while expanding coverage across VMware, Cisco, FortiGate, F5, Dell EMC, and PowerEdge platforms.
- Led monthly RA-5 vulnerability-remediation sprints across a hybrid FedRAMP High boundary of more than 2,500 assets spanning dual Tier III colocation sites in Elk Grove, Illinois, and Sterling, Virginia, plus a GCP BigQuery/Grafana analytics tier; closed 100% of new High findings within the 30-day SLA and kept the service clear of JAB Corrective-Action Plans for six consecutive years.
- Rapidly architected, tested, and deployed security fixes, base-image rebuilds, hardened IAM policies, shielded-VM baselines, and custom validation payloads to restore customer security and support quarterly audits and annual 3PAO assessment evidence.
- Built automation across the monitoring organization through an Ansible AWX orchestration platform, dozens of playbooks, and Python and Bash tooling for diagnostics, reporting, remediation, and standardized operational workflows.
- Authored more than 50 Standard Operating Procedures, scaled the global support team from 5 to 25 engineers, conducted hundreds of change, risk, security, and production-readiness assessments, and carried Tier 3 24x7 on-call responsibilities for six years.
- Contributed beyond core engineering through mentoring, Future Ready Skills facilitation, co-founding the internal DellTalks speaker series, and serving on the ERG Executive Leadership Team as North America Community and Advocacy co-lead, working directly with managers and executives across the company.

### American Tire Distributors - Huntersville, North Carolina

**E-commerce Support Delivery Lead** | **2017-2018**

National tire-distribution and B2B commerce environment supporting internal operations, dealers, and purchasing workflows, where I led Tier 2/Tier 3 production support, incident triage, and cross-functional coordination across a large on-premises data-center footprint.

- Served as tower lead for 24x7 Tier 2/Tier 3 production support, triaging incidents, validating impact, and routing issues to engineering, product, and vendor teams to protect business-critical purchasing and logistics workflows.
- Worked directly with business analysts, internal users, vendors, and development teams to gather requirements, support user acceptance testing, verify fixes, and convert production issues into actionable engineering work.
- Orchestrated an SAP Hybris upgrade from 5.x to 6.x and migrated 90,000 B2B customer records with zero downtime.
- Diagnosed and coordinated resolution of high-impact commerce and system-wide outages through log analysis, real-time lookups, and data validation.
- Built infrastructure-monitoring dashboards and automated reports that improved availability visibility and enabled proactive alerting.
- Produced data-driven analyses and performance reports that informed strategic initiatives and improved client-side performance and overall system stability by 20%.
- Authored SOPs and operational documentation and used Jira and Confluence to manage incidents, technical debt, and production knowledge.

### Woozle, LLC - Columbia, South Carolina

**Lead Product Developer** | **2015**

Early-stage startup in the USC/Columbia Technology Incubator, where I led MVP development across a universal iOS client, backend APIs, and launch web assets.

- Designed and built the Woozle universal iOS 9 application for iPhone and iPad using UIKit, Storyboards, CoreLocation, and MapKit, implementing geofencing and real-time mapping.
- Built a Node.js/Express REST API for mobile clients and an HTML/CSS/JavaScript landing site for launch marketing and beta sign-ups.
- Mentored and onboarded two junior developers, established coding standards, and accelerated team delivery.
- Produced UI mockups and launch assets that aligned the mobile application and marketing site.

### 52 Apps, Inc. - Columbia, South Carolina

**Enterprise iOS Developer** | **2015**

Startup consultancy in the USC/Columbia Technology Incubator, where I delivered native iOS applications for enterprise and App Store release across implementation, API integration, payments, and launch.

- Led development of PolicyView, a flagship iPad application for iOS 8, owning native implementation from concept through App Store approval and release.
- Integrated payment gateways and internal and third-party RESTful APIs for secure transaction and data-synchronization workflows.
- Extended StoreKit in Wokut for iOS 7 to improve in-app purchase reliability and transaction handling.
- Improved PilotPass for iOS 7 through UI performance and accessibility work, reducing screen-load latency and improving usability.

### Kyrus Solutions - Greenville, South Carolina

**Enterprise iOS Developer** | **2013-2014**

Mobile-commerce and point-of-sale engineering firm, formerly Agilysys, delivering branded SAP-based mPOS solutions for global retail customers.

- Led the iOS implementation of SAP mPOS, collaborating with product owners and cross-functional teams to support stable enterprise payment workflows handling more than 10,000 transactions per day.
- Served as principal iOS 7 and Java developer for NextManager, a mobile point-of-sale product line that streamlined checkout through multithreaded I/O and tightly integrated retail workflows.
- Built customer-specific implementations for global retail brands including Apple Retail, PVH/Calvin Klein, and Sephora across complex client and vendor ecosystems.
- Integrated native iOS applications with Zebra scanners, Verifone payment terminals, and SAP and Oracle systems to enable scanning, payments, inventory workflows, and data synchronization.
- Designed adaptive iPhone and iPad interfaces with UIKit, Interface Builder, and Auto Layout, applying asynchronous processing, memory-management, and modular-architecture practices.

### SHL / Brainbench - Remote

**Enterprise Test Developer (Part-time)** | **2013-2015**

- Designed and authored the Apple iOS 7 Development Competency Exam and Apple OS X Desktop Administration Competency Exam, producing and validating more than 150 scenario-based questions, code snippets, performance tasks, and multimedia simulations.
- Collaborated remotely with subject-matter experts to verify technical correctness, answer keys, code behavior, clarity, and appropriate assessment coverage for professional skills evaluation.

### Computer Sciences Corporation - Blythewood, South Carolina

**Programmer Analyst** | **2011-2013**

- Led Java development for POINT IN J, a Java EE and SQL Server/SSIS application, building backend services and data-integration pipelines while serving as a go-to troubleshooter across projects.
- Improved diagnostic and development workflows, reducing average bug-turnaround time by 40%.

### Furman University - Greenville, South Carolina

**IT Specialist / Furman Alumni Fellow** | **2008-2009**

- Selected as a Furman Alumni Fellow immediately after graduation and assigned to Human Resources, where I automated secure ETL workflows that reduced manual data entry by 50%, delivered advanced Excel training to more than 80 staff, and redesigned CMS processes that reduced website-update turnaround from 30 days to one.

**Computer Help Desk and Multimedia Services - Paid Student Technical Employment** | **2005-2008**

- Provided hardware, software, account, network, classroom, and multimedia technology support for students, faculty, and staff while completing the Information Technology degree.
- Supported operational audiovisual and computing environments, developing practical experience across user support, troubleshooting, systems integration, and production technology services.

## Education

### Furman University - Greenville, South Carolina

**Bachelor of Arts in Information Technology, Department of Computer Science** | **2008**

**Selected Systems Engineering Projects**

- Built a six-node Ubuntu Beowulf cluster from retired university library computers, refurbishing and upgrading the systems and configuring distributed processing for parallel CPU-based simulations.
- Designed a custom 8-bit instruction-set architecture and implemented a functioning CPU in Logisim, integrating its computation, memory, datapath, and control behavior.
- Engineered and deployed a production NetBSD/SHOUTcast streaming appliance for Furman's radio station, integrating analog audio capture and routing, boot-time service orchestration, and unattended service management to deliver low-latency live Internet broadcasting through the station website 24x7.
- Built and compiled a complete working operating system from source using Linux From Scratch, integrating the compiler toolchain, kernel, libraries, boot process, and userland.
- Conducted authorized wireless-network analysis and red-team penetration testing, documented findings, and advised on and implemented web-hosting and HTTP improvements.

## Technical Expertise

- **AI systems and evaluation:** LLM and ASR inference; WER, RTF, latency, throughput, and accuracy evaluation; quantization; benchmark and evidence design; vLLM; LLM Compressor; PyTorch; CUDA; WhisperX; faster-whisper; CTranslate2; ONNX Runtime; ggml; whisper.cpp; model, dataset, and artifact provenance.
- **Languages and application development:** Rust, Python, Bash, Java, JavaScript/Node.js, SQL, HTML/CSS, REST APIs, native iOS, UIKit, StoreKit, CoreLocation, MapKit, accessibility, and mobile payments.
- **Linux and infrastructure:** Linux and FOSS since 2004; Ubuntu, RHEL, NetBSD, Docker, Kubernetes/K3s, Podman, systemd, Ansible/AWX, VMware/vCenter, Cisco, FortiGate, F5, Dell EMC, and PowerEdge.
- **Observability and data platforms:** Prometheus, Grafana, Zabbix, ServiceNow, Google BigQuery, Apache HBase, Hadoop HDFS, Fluentd, time-series analytics, exporters, telemetry, and performance tuning.
- **Security and compliance:** FedRAMP High, NIST SP 800-53, JAB P-ATO, 3PAO evidence, SSP/POA&M, RA-5 vulnerability remediation, IAM hardening, security validation, risk assessment, and authorized penetration testing.

## Licenses, Certifications & Clearance

- FCC General Mobile Radio Service License - active
- FAA Remote Pilot Certificate - Small Unmanned Aircraft Systems, Part 107 - inactive
- FCC Amateur Radio Service License - Amateur Extra Class - inactive
- Linux Foundation Certified System Administrator (LFCS) - inactive
- Previously held DoD Secret clearance - inactive
