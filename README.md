# Smart India Hackathon Workshop
# Date:24.11.2026
## Reference Number:26012954
## Name:Harithra.K

## Problem Title
SIH 26033: Multiple intermediaries reduce farmers earnings and increase consumer prices.

## Problem Creater's Organization
Ministry of Consumer Affairs, Food & Public Distribution

## Theme
Agriculture, FoodTech & Rural Development

## Problem Description
Expected Solution: Create a digital marketplace that:

• Connects farmers/FPOs directly with consumers and bulk buyers.
• Provides logistics support.
• Uses AI for demand forecasting and route optimization.

Benefits:

• Better prices for farmers.
• Lower prices for consumers.
• Reduced supply chain inefficiencies.

## Proposed Solution
1. Detailed Explanation of the Proposed Solution
KrishiSetu is an AI-driven, hyperlocal B2B and B2C digital agricultural marketplace designed to eliminate multi-tiered middlemen by directly linking farmers and Farmer Producer Organizations (FPOs) with end consumers, retailers, and institutional bulk buyers (HoReCa, supermarkets, and processing units).

The platform operates across four core pillars:

Direct Farm-to-Fork Marketplace: A multilingual mobile app (with voice-assisted navigation) and web portal where farmers/FPOs list harvested or upcoming produce with transparent quality grades, harvest dates, and farm-gate pricing.

Dynamic Price Discovery Engine: Integrates real-time Mandi (e-NAM) prices, local demand, and input costs to recommend fair base prices, preventing distress sales by farmers while keeping retail prices 15–25% below traditional market rates.

Integrated Milk-Run Logistics Network: Aggregates smaller harvests from multiple nearby farms at local village collection centers (FPO hubs) and pairs them with verified third-party logistics (3PL) transporters and cold-chain fleet owners.

AI Demand & Harvest Synchronization: Predicts regional crop demand 7–14 days in advance, advising farmers on optimal harvest timing and crop allocation to minimize post-harvest wastage.

2. How It Addresses the Problem
Eliminates Commission Layers: Replaces 4–6 traditional intermediaries (village aggregators, commission agents/arhatiyas, wholesalers, sub-wholesalers) with a single transparent digital platform charging a minimal platform/logistics fee (3–5%).

Solves Fragmented Supply: Individual smallholders lack volume for bulk buyers; by pooling supply at the FPO level, the platform fulfills large institutional orders reliably.

Reduces Transit Spoilage: AI route optimization and cold-chain matching cut transit delays, lowering perishable post-harvest losses from the current 20–30% down to under 8%.

3. Innovation and Uniqueness
Offline-First & Voice-Native UI: Built for low-literacy and low-connectivity rural areas using regional voice commands (via Bhashini APIs) and SMS/IVR fallback for order confirmations.

AI Computer Vision Quality Grading: Farmers capture a short video/photo of produce; an on-device lightweight vision model grades size, ripeness, and defects, generating a trusted digital quality certificate for remote bulk buyers.

Dynamic Milk-Run Pooling: Instead of point-to-point transport (which is expensive for small loads), the routing engine dynamically clusters pickups along a single optimized route, splitting transport costs across multiple farmers.

## Technical Approach
1. Technologies to Be UsedFrontend (Mobile & Web): React Native / Flutter (offline-first SQLite caching for farmers), Next.js (for bulk buyers, FPO dashboards, and admin portals).Backend & APIs: Node.js / Python (FastAPI) microservices architecture, GraphQL/REST APIs, WebSockets for live bidding and fleet tracking.Database & Storage: PostgreSQL with PostGIS (geospatial queries for farm-to-buyer proximity), Redis (caching & real-time pricing), AWS S3 / Cloud Storage (produce images).AI / ML Stack:Demand Forecasting: Temporal Fusion Transformers (TFT) / Prophet trained on historical Mandi arrivals, weather APIs, and festival calendars.Route Optimization: Google OR-Tools (Vehicle Routing Problem with Time Windows and Capacity Constraints).Quality Grading: MobileNetV3 / YOLOv8-nano deployed via TensorFlow Lite for edge inference.Integrations: Bhashini API (vernacular voice/text), UPI / Razorpay Route (automated split payments directly to farmer bank accounts), OpenStreetMap / Google Maps API, e-NAM / Agmarknet open data APIs.
   SIH_26033_KrishiSetu_Technical_Architecture.pdf
   +---------------------------------------------------------------------------------------------------+
|                   KRISHISETU — END-TO-END SYSTEM ARCHITECTURE (SIH 26033)                         |
+---------------------------------------------------------------------------------------------------+

  [ 1. SUPPLY & EDGE LAYER ]                            [ 2. CORE PLATFORM & DPI ]
+-----------------------------+                       +-----------------------------------+
|  Farmers & FPO Hubs         |                       |  API Gateway & Auth               |
|  • Flutter Offline App      |  -- Crop Listings --> |  • Node.js / FastAPI              |
|  • Bhashini Voice UI        |                       |  • REST / GraphQL + WebSockets    |
+-----------------------------+                       +-----------------------------------+
               |                                                        |
               v                                                        v
+-----------------------------+                       +-----------------------------------+
|  Edge AI Quality Grader     |                       |  Core Data & Geospatial Store     |
|  • YOLOv8-Nano / TFLite     |  -- Quality Cert ---> |  • PostgreSQL + PostGIS           |
|  • Digital Quality Cert     |                       |  • Redis + e-NAM / Agmarknet API  |
+-----------------------------+                       +-----------------------------------+
               |                                                        |
               v                                                        | (Forecast & Pricing Data)
+-----------------------------+                                         v
|  FPO Aggregation Center     |                       [ 3. AI & OPTIMIZATION ENGINE ]
|  • Pools Smallholder Lots   |                       +-----------------------------------+
|  • QR Crate Tagging         |                       |  • AI Demand Forecast (TFT)       |
+-----------------------------+                       |  • Dynamic Price Discovery        |
               |                                      |  • Milk-Run Router (OR-Tools)     |
               |                                      +-----------------------------------+
               |                                                        |
               +------------------- Optimized Milk-Run Dispatch --------+
                                                |
                                                v
  [ 2. SETTLEMENT ENGINE ]                            [ 4. LOGISTICS & DEMAND LAYER ]
+-----------------------------+                       +-----------------------------------+
|  UPI Escrow & Split-Pay     |                       |  3PL & Cold-Chain Fleet           |
|  • Razorpay Route / UPI     | <-- QR Delivery ----- |  • GPS + IoT Temp Telemetry       |
|  • Direct Farmer Credit     |     Confirmation      |  • Multi-FPO Pickup Route         |
|    (< 24 Hours)             |                       +-----------------------------------+
+-----------------------------+                                         |
                                                                        v
                                                      +-----------------------------------+
                                                      |  Bulk Buyers & Consumers          |
                                                      |  • HoReCa, Retailers, B2C Groups  |
                                                      |  • Scans Crate QR on Delivery     |
                                                      +-----------------------------------+
   
   2. Methodology and Process for ImplementationEnd-to-End Operational Flow:Listing & Grading: Farmer logs harvest via voice/app $\rightarrow$ AI vision grades produce $\rightarrow$ Dynamic pricing engine suggests fair price.Demand Aggregation: AI forecasts regional demand $\rightarrow$ Bulk buyers/consumers place orders $\rightarrow$ Platform matches orders with nearest FPO clusters.Smart Dispatch: OR-Tools calculates optimal multi-pickup "milk-run" route $\rightarrow$ 3PL vehicle collects produce from FPO hub $\rightarrow$ Live GPS tracking to buyer.Instant Settlement: Digital proof of delivery (OTP/QR scan) triggers automated UPI split payment directly to the farmer's account within 24 hours.Phased Implementation Roadmap:Phase 1 (Weeks 1–4) – Core Platform & Onboarding: Develop MVP mobile/web apps, integrate UPI split payments, and onboard 5–10 pilot FPOs and local HoReCa buyers.Phase 2 (Weeks 5–8) – AI & Logistics Engine: Deploy OR-Tools routing algorithm, integrate Agmarknet price feeds, and onboard local mini-truck/cold-van operators.Phase 3 (Weeks 9–12) – Edge AI & Scale: Roll out offline-first sync, Bhashini vernacular voice support, and computer vision produce grading; run live pilot and iterate on unit economics.

## Feasibility and Viability
1. Feasibility Analysis
Technical Feasibility: High. Leverages proven open-source optimization frameworks (OR-Tools), lightweight edge ML models, and India’s mature Digital Public Infrastructure (UPI, Bhashini, e-NAM APIs).

Operational Feasibility: High. Partnering with existing FPOs (over 10,000+ registered across India) provides immediate access to aggregated farmer networks, physical collection points, and local trust without building brick-and-mortar warehouses from scratch.

Financial Viability: Sustainable unit economics through a B2B-first anchor model (predictable high-volume orders from retailers/HoReCa) supplemented by B2C apartment/community group-buying, monetized via a 3–5% transaction fee and logistics margin.

2. Potential Challenges and Risks
Digital Literacy & Smartphone Barriers: Smallholder farmers may struggle with complex app interfaces or lack high-end smartphones.

Quality Disputes in Remote Trading: Bulk buyers may reject produce upon delivery if quality doesn't match expectations.

Logistics Cold-Start Problem: Low initial order density in a new region can lead to underutilized trucks and high per-kg transport costs.

Resistance from Traditional Middlemen: Local commission agents may pressure farmers not to bypass traditional Mandis.

3. Strategies for Overcoming Challenges
FPO-Assisted Onboarding & Voice UI: Deploy "Krishi Mitras" (FPO field coordinators) to assist farmers with onboarding and grading, paired with simple vernacular voice/IVR workflows.

Standardized AI Grading + Escrow: Combine AI visual grading at pickup with an escrow payment system—funds release upon QR-verified delivery, and standardized grading parameters prevent arbitrary rejections.

Hyperlocal Cluster Launch: Launch cluster-by-cluster (within a 50–80 km radius of tier-1/tier-2 consumption hubs) to ensure high vehicle utilization from day one.

Credit & Input Linkages: Provide digital transaction histories that help farmers access low-interest institutional credit, creating strong retention incentives beyond just price.
## Impact and Benefits
Remove These Lines
1. Impact on Target Audience
Farmers & FPOs: Realize 20–35% higher net income by capturing margins previously lost to intermediaries, alongside guaranteed 24-hour digital payouts and data-backed crop planning.

Consumers & Bulk Buyers: Access fresher, traceable farm produce at 15–25% lower prices with reliable delivery schedules and standardized quality grades.

Local Transporters: Higher asset utilization and steady daily earnings through automated route clustering.

2. Multi-Dimensional Benefits
Economic: Eliminates cascading markups, curbs food inflation at the retail level, and creates formal digital financial footprints for rural producers.

Social: Empowers smallholder farmers with transparent price intelligence, reduces distress sales, and strengthens rural FPO ecosystems.

Environmental: AI route optimization reduces empty-mile truck emissions, while demand-aligned harvesting and faster transit significantly cut perishable food waste and associated methane emissions.

## Research and References
Government & Policy Frameworks:

Ministry of Agriculture & Farmers Welfare – National Agriculture Market (e-NAM) Operational Guidelines & Agmarknet Open Data Portal.

Ministry of Consumer Affairs, Food & Public Distribution – Price Monitoring Division (PMD) & Essential Commodities Supply Chain Reports.

Small Farmers' Agribusiness Consortium (SFAC) – Strategy Paper on Promotion of 10,000 Farmer Producer Organizations (FPOs).

Supply Chain & Post-Harvest Loss Studies:

NABARD / ICAR-CIPHET – Study on Quantitative Harvest and Post-Harvest Losses of Major Crops and Commodities in India (highlights 15–30% wastage in perishables due to fragmented logistics).

NITI Aayog – Task Force Report on Agricultural Development and Supply Chain Reforms.

Technical & Algorithmic References:

Google OR-Tools Documentation – Capacitated Vehicle Routing Problem with Time Windows (CVRPTW) for milk-run logistics optimization.

Lim et al. (2021) – Temporal Fusion Transformers for Interpretable Multi-horizon Time Series Forecasting (International Journal of Forecasting) for agricultural demand prediction.

Digital India Bhashini Division – Bhashini API Documentation for Multilingual Voice and Translation Integration.
