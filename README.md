Table of Contents
Introduction & Purpose
Curve Definitions
2.1 What is a Curve?
2.2 What is a Forward Curve?
2.3 Key Concepts and Terminology
Forward Curve Modelling by Asset Class
3.1 Energy Products
3.2 Carbon Markets
3.3 Base Metals
3.4 Precious Metals
3.5 Agricultural Commodities
3.6 Soft Commodities
3.7 Freight & Shipping
Model Assumptions
Model Governance Framework
Model Validation
Challenges & Risk Factors
Technology & Infrastructure
Stakeholder Map & Responsibilities
Key Performance Metrics & Controls
Regulatory & Compliance Considerations
Role Competency Framework
Glossary of Terms
1. Introduction & Purpose
1.1 Purpose of this Document
This document provides a detailed reference for the role of Forward Curve Methodology Lead within the Commodity & Energy quantitative function. It describes:

The theoretical foundations of forward curve construction
Product-specific modelling methodologies and their mathematical bases
Governance, validation, and quality control frameworks
Model assumptions and their implications
Challenges inherent in commodity forward curve management
The skills, responsibilities, and stakeholder landscape for this role
1.2 Business Context
Forward curves are foundational to all valuation, risk management, and trading activities in commodity and energy markets. Every trade valuation, P&L calculation, VaR estimate, hedge effectiveness test, and regulatory capital computation depends on the quality and integrity of forward curves.

A robust, well-governed forward curve methodology function therefore sits at the intersection of:

Front Office – trading desks that mark and consume curves
Risk Management – using curves for exposure and capital calculation
Finance – P&L attribution and balance sheet valuation
Compliance – fair value audit trails
Technology – systems that compute, store, and distribute curves
1.3 Scope
This document covers commodity and energy forward curves across the following asset classes:

Asset Class	Products
Energy	Crude Oil (WTI, Brent), Natural Gas, Refined Products
Carbon	EU ETS, UK ETS, ACCU, CORSIA
Base Metals	Copper, Aluminium, Zinc, Lead, Nickel, Tin
Precious Metals	Gold, Silver, Platinum, Palladium
Agricultural	Corn, Wheat, Soybeans, Livestock
Soft Commodities	Coffee, Sugar, Cocoa, Cotton
Freight	Baltic Dry, Capesize, Panamax, Supramax
2. Curve Definitions
2.1 What is a Curve?
In financial markets, a curve is a mathematical construct that maps a continuous or discrete set of market prices or rates across a dimension – most commonly time-to-maturity. A curve transforms a sparse set of observable market prices into a complete, usable representation of market expectations across all tenors.

Curves serve three primary functions:

Valuation – pricing instruments with cash flows at future dates
Risk – computing sensitivities (delta, gamma, vega) to market movements
Scenario Analysis – stress testing and scenario generation
2.2 What is a Forward Curve?
A forward curve (also called a price curve, futures curve, or term structure of prices) represents the market's expectation of the price of a commodity or financial asset at various future delivery dates.

Formally:

F(t, T) = the price agreed today (at time t) to buy or sell a commodity at future time T
Unlike interest rate yield curves (which are continuous), commodity forward curves are typically:

Discrete – defined at specific contract maturities (e.g., monthly, quarterly)
Non-constant tenor – each pillar represents a fixed calendar date, not a rolling period
Physically motivated – shaped by storage costs, convenience yields, seasonal demand, and supply fundamentals
2.2.1 Spot vs. Forward Price
Concept	Definition
Spot Price S(t)	The current market price for immediate delivery
Forward Price F(t,T)	Price agreed today for delivery at future date T
Futures Price	Exchange-standardised forward contract traded on a regulated exchange
For most commodities, the theoretical relationship is:

F(t, T) = S(t) × exp[(r + s - c) × (T - t)]
Where:

r = risk-free interest rate
s = storage cost (per unit time, as a proportion of price)
c = convenience yield (benefit of holding physical inventory)
2.2.2 Contango and Backwardation
Term	Definition	Typical Driver
Contango	Forward price > Spot price (F > S)	Storage costs, financing costs; ample supply
Backwardation	Forward price < Spot price (F < S)	Tight near-term supply; high convenience yield
Normal Contango	Mild upward slope reflecting cost of carry	Base case for most commodities
2.3 Key Concepts and Terminology
2.3.1 Cost of Carry
The theoretical cost of holding a physical commodity from today to a future delivery date:

Cost of Carry = Financing Cost + Storage Cost + Insurance Cost - Convenience Yield
2.3.2 Convenience Yield
An implicit benefit to holding physical inventory – reflects the value of being able to meet unexpected demand immediately without waiting for delivery. High when inventories are low or supply is disrupted.

Convenience Yield (c) such that: F(t,T) = S(t) × exp[(r + s - c)(T-t)]
2.3.3 Basis
The difference between the spot price and the futures price, or between two related futures prices:

Basis = Spot Price - Futures Price
      OR
Basis = Price at Location A - Price at Location B
2.3.4 Calendar Spread
The price difference between two futures contracts for the same commodity but different delivery months:

Calendar_Spread(M1, M2) = Futures_Price(M2) - Futures_Price(M1)
2.3.5 Pillar Points / Liquid Tenors
Market-observable prices exist only at specific tenors (e.g., front month, quarterly, annual contracts). These are called pillar points or liquid tenors. Prices at all other dates must be interpolated or extrapolated.

3. Forward Curve Modelling by Asset Class
3.1 Energy Products
3.1.1 Brent Crude Oil (ICE)
Market Structure:

Primary global crude oil benchmark
ICE Brent futures are the most liquid crude oil contracts globally
Liquid up to approximately 3 years; illiquid beyond
Methodology: Exchange Settlement + Interpolation

Step 1: Obtain ICE settlement prices for all liquid contract months
Step 2: Identify pillar points (front month + December contracts)
Step 3: Interpolate between pillars using calendar spreads or linear interpolation
Step 4: Extrapolate beyond last liquid contract using flat or slope assumption
Mathematical Formula:

For liquid contracts:

Brent(T) = ICE_Settlement(T)
For broken dates (interpolation):

Brent(t) = Brent(t₁) + [(Brent(t₂) - Brent(t₁)) × (t - t₁) / (t₂ - t₁)]
Data Sources:

ICE settlement prices (primary)
Bloomberg real-time live pricing (intraday)
Broker quotes for illiquid tenors
Key Assumptions:

ICE settlement prices are the most reliable observable market price
Calendar spreads between liquid pillar points accurately represent market expectations
Linear interpolation is appropriate between adjacent monthly contracts
3.1.2 WTI Crude Oil (CME/NYMEX)
Market Structure:

US domestic crude oil benchmark
Traded at CME/NYMEX; delivery at Cushing, Oklahoma
Historically trades at a discount to Brent (location and quality differential)
Methodology: Brent Benchmark + WTI/Brent Spread + Calendar Spread Construction

Step 1: Front Month = Brent_Front_Month + WTI/Brent_Spread
Step 2: For each subsequent month i:
        WTI(i) = WTI(i-1) + Calendar_Spread(i-1, i)
Step 3: Calendar spreads = manually input by trader (liquid) or interpolated (illiquid)
Mathematical Formula:

WTI_M1 = Brent_M1 + WTI_Brent_Spread

WTI_Mᵢ = WTI_Mᵢ₋₁ + CalSpread(i-1, i)    for i = 2, 3, ..., n
Example:

Brent_Jan = $80.00/bbl
WTI/Brent spread = -$2.50
WTI_Jan = $80.00 - $2.50 = $77.50

Calendar spread Jan→Feb = +$0.20
WTI_Feb = $77.50 + $0.20 = $77.70

Calendar spread Feb→Mar = +$0.15
WTI_Mar = $77.70 + $0.15 = $77.85
Key Assumptions:

WTI price is structurally determined relative to Brent
Calendar spreads reflect storage costs at Cushing
Pipeline infrastructure capacity constrains location spreads
3.1.3 Natural Gas (NYMEX Henry Hub)
Methodology: Futures-Based Term Structure + Location Basis

NG_HH(T) = NYMEX_Settlement(T)

NG_Other_Location(T) = NG_HH(T) + Location_Basis(T)
Seasonality: Natural gas curves exhibit strong seasonal patterns driven by:

Heating demand (winter)
Cooling demand (summer)
Storage injection/withdrawal cycles
Key Assumptions:

Henry Hub serves as the primary pricing hub
Location basis reflects pipeline and infrastructure constraints
Storage cycle (April–October injection; November–March withdrawal) drives seasonal shape
3.1.4 Refined Products (RBOB Gasoline, Heating Oil, Diesel)
Methodology: Crack Spread Model

Product_Forward(T) = Crude_Benchmark(T) + Crack_Spread(T) + Location_Differential(T)

RBOB_Gasoline(T) = WTI(T) + RBOB_Crack_Spread(T) + Gulf_Coast_Differential
Heating_Oil(T)   = WTI(T) + HO_Crack_Spread(T)   + Location_Differential
Crack Spread: The margin earned from refining crude oil into refined products:

3-2-1 crack = (2 × Gasoline + 1 × Heating Oil) - 3 × Crude Oil
Reflects refinery profitability
3.2 Carbon Markets
Carbon markets have a structurally different forward curve behaviour: no seasonal pattern, the entire curve shifts up/down together, and the theoretical framework is based on cost of carry with no convenience yield.

3.2.1 EU ETS (European Union Emissions Trading Scheme)
Market Structure:

EU allowances (EUAs) grant the right to emit 1 tonne of CO₂
Primary regulated cap-and-trade scheme in Europe
Annual compliance cycle (April surrender deadline)
Traded on ICE
Methodology: Cost of Carry Model (ESTR-based)

F(t, T) = S(t) × exp(ESTR × (T - t))
Simplified for short tenors:

F(t, T) = S(t) × (1 + ESTR × (T - t) / 365)
Where:

S(t) = Current EUA spot price (€/tonne CO₂)
ESTR = Euro Short-Term Rate (daily compounded)
T - t = Days to maturity
No Dividend, No Convenience Yield:

Carbon allowances earn no yield and have no physical convenience yield
Storage cost = negligible (electronic registry)
Therefore: F(t,T) = S(t) × e^(r(T-t)) purely
Worked Example:

EUA Spot        = €85.00/tonne
ESTR            = 3.50% (0.0350)
Days to Dec 26  = 180

EUA_Dec26 = €85.00 × (1 + 0.0350 × 180/365)
           = €85.00 × 1.01726
           = €86.47/tonne
Broken Date Pricing (Asian Swap):

Asian_Swap_Price = Average[F(t, Tᵢ)] for all business days Tᵢ in the tenor period
3.2.2 UK ETS
Methodology: Identical to EU ETS but uses SONIA (Sterling Overnight Index Average):

F(t, T) = S(t) × (1 + SONIA × (T - t) / 365)
3.2.3 ACCU (Australian Carbon Credit Units)
Methodology: Uses BBSW (Bank Bill Swap Rate):

F(t, T) = S(t) × (1 + BBSW × (T - t) / 365)
Limited secondary market; primarily spot-driven with illiquid forward market.

3.2.4 CORSIA (Carbon Offsetting and Reduction Scheme for International Aviation)
Methodology: Uses SOFR (Secured Overnight Financing Rate):

F(t, T) = S(t) × (1 + SOFR × (T - t) / 365)
Very limited liquidity; theoretical pricing only for most tenors.

3.3 Base Metals
3.3.1 LME-Traded Metals (Copper, Aluminium, Zinc, Lead, Nickel, Tin)
Market Structure:

London Metal Exchange (LME) is the primary global benchmark
Standard LME dates: Cash, 1-week, 2-week, 1M, 2M, 3M, 6M, 15M, 27M
Beyond 27M: OTC market, limited liquidity
Methodology: Term Structure + Storage Costs

F(t, T) = Cash_Price + Contango(T) + Storage_Cost(T)
Where:

Storage_Cost(T) = Storage_Rate × Cash_Price × (T - t) / 365
Contango(T)     = LME_market_contango at tenor T (directly observable at standard dates)
Interpolation for Non-Standard Dates:

F(t) = F(t₁) + [(F(t₂) - F(t₁)) × (t - t₁) / (t₂ - t₁)]
Worked Example (Copper):

LME Cash     = $8,500/tonne
3M Contango  = $50/tonne
15M Contango = $180/tonne
Storage Rate = 2% p.a.

Copper_3M  = $8,500 + $50  = $8,550/tonne
Copper_15M = $8,500 + $180 = $8,680/tonne

Copper_9M (interpolated):
= $8,550 + [($8,680 - $8,550) × (9 - 3) / (15 - 3)]
= $8,550 + [$130 × 0.5]
= $8,550 + $65 = $8,615/tonne
Key Assumptions:

LME official settlement prices are definitive
Storage costs are proportional to spot price
Backwardation may occur when nearby supply is tight
Warehouse stock levels affect contango/backwardation structure
3.4 Precious Metals
3.4.1 Gold
Market Structure:

Dual role: monetary asset and industrial/jewellery commodity
Active lending/leasing market (gold lease rates)
LBMA (London Bullion Market Association) sets benchmark prices
Methodology: Interest Rate minus Lease Rate Model

F(t, T) = S(t) × exp[(r - q) × (T - t)]
Simplified:

Gold_Forward(T) = Gold_Spot × (1 + (USD_Rate - Gold_Lease_Rate) × (T - t) / 365)
Where:

r = USD risk-free rate (SOFR)
q = Gold lease rate (typically 0.1% – 1.0% p.a.)
Lease rate = the rate at which gold holders lend gold to borrowers
Worked Example:

Gold Spot       = $2,000/oz
USD Rate (SOFR) = 5.25%
Gold Lease Rate = 0.50%
Days to 3M      = 90

Gold_3M = $2,000 × (1 + (0.0525 - 0.005) × 90/365)
         = $2,000 × (1 + 0.0475 × 0.2466)
         = $2,000 × 1.01171
         = $2,023.42/oz
3.4.2 Silver
Silver_Forward(T) = Silver_Spot × (1 + (USD_Rate - Silver_Lease_Rate) × (T - t) / 365)
Silver lease rates are typically higher than gold (0.5%–2.0% p.a.) due to larger industrial demand component.

3.4.3 Platinum & Palladium
Primarily futures-based (NYMEX), with limited lease market:

PGM_Forward(T) = NYMEX_Futures(T) + Basis_Adjustment
3.5 Agricultural Commodities
3.5.1 Grains (Corn, Wheat, Soybeans)
Market Structure:

Traded on CBOT (Chicago Board of Trade)
Strong seasonal patterns driven by harvest cycles
Specific contract months (e.g., corn: March, May, July, September, December)
Methodology: Futures + Cost of Carry + Convenience Yield + Seasonal Adjustment

F(t, T) = Futures_Price(T) + Storage_Cost(T) - Convenience_Yield(T)
Full cost of carry:

F(t, T) = S(t) × exp[(r + s - c) × (T - t)]
Where:

s = storage cost per unit time (~
0.05/bushel/month)
c = convenience yield (high near harvest, low at other times)
Seasonal Factor:

F_seasonal(T) = F_base(T) × Seasonal_Factor(Month(T))
Seasonal factors are derived from historical price patterns and crop calendars:

Month	Corn Seasonal Factor
October–November	0.97 (harvest, ample supply)
February–March	1.00 (base)
July–August	1.03 (pre-harvest tightness)
Worked Example:

Corn Dec Futures  = $4.50/bushel
Storage Rate      = $0.04/bushel/month
Interest Rate     = 5%
Months to Dec     = 6

Storage_Cost      = 6 × $0.04 = $0.24/bushel
Interest_Cost     = $4.50 × 5% × 6/12 = $0.1125

Corn_Dec_Forward  = $4.50 + $0.24 + $0.11 = $4.85/bushel
3.5.2 Livestock (Live Cattle, Feeder Cattle, Lean Hogs)
Methodology: Biological Growth Model

Livestock cannot be stored in the traditional sense; the "cost of carry" is replaced by a biological growth model:

Cattle_Forward(T) = Feeder_Price × Weight_Gain_Factor + Feed_Cost(T) + Operating_Margin
Hog_Forward(T)    = Current_Price + Feed_Cost_Impact(T) + Seasonal_Demand(T)
3.6 Soft Commodities
3.6.1 Coffee (Arabica & Robusta)
Arabica_Forward(T) = ICE_US_Futures(T) × BRL_USD_Adjustment + Weather_Premium
Robusta_Forward(T) = ICE_Europe_Futures(T) × VND_USD_Adjustment + Monsoon_Factor
Key drivers: Brazilian frost risk, Vietnamese monsoon, currency (BRL/USD, VND/USD).

3.6.2 Sugar
Sugar_11_Forward(T) = ICE_Futures(T) × BRL_USD_Factor + Brazil_Ethanol_Parity
Sugar_5_Forward(T)  = Sugar_11_Forward(T) + White_Premium(T) + Refining_Margin(T)
Key driver: Brazilian mill decision between sugar and ethanol production.

3.6.3 Cocoa
Cocoa_Forward(T) = Futures_Price(T) + Processing_Spread(T) + Weather_Risk_Premium(T)
Processing Spread (grind spread):

Bean_Value = (Butter_Price × Butter_Yield) + (Powder_Price × Powder_Yield)
             where Butter_Yield ≈ 20%, Powder_Yield ≈ 80% of bean weight
3.7 Freight & Shipping
Methodology: Route-Specific Time Charter Equivalent (TCE)

Forward_Rate(T) = Spot_Rate × Seasonal_Factor(T) + Supply_Demand_Adjustment(T)

Capesize(T)  = Brazil_China_Rate × Fleet_Utilisation + Bunker_Adjustment
Panamax(T)   = USG_Japan_Rate × Grain_Export_Factor + Panama_Canal_Premium
Freight curves are highly mean-reverting; long-dated curves tend to converge to equilibrium TCE estimates.

4. Model Assumptions
4.1 Universal Assumptions (Across All Asset Classes)
#	Assumption	Justification	Limitation
A1	No-arbitrage condition holds	Prevents risk-free profits; foundational to pricing	Breaks down in stressed/illiquid markets
A2	Markets are sufficiently liquid at pillar points	Ensures observable prices are reliable	Illiquid markets require model prices not market prices
A3	Interest rates are deterministic (for cost of carry)	Simplifies calculation; adequate for short-dated curves	Stochastic rates may matter for long-dated instruments
A4	Counterparty risk is zero (or fully collateralised)	Clean theoretical pricing	Must be adjusted for uncollateralised trades (CVA)
A5	Interpolation between pillar points is smooth and monotonic	Prevents arbitrage between consecutive tenors	Real markets may exhibit discontinuities (e.g., seasonal)
4.2 Energy-Specific Assumptions
#	Assumption	Detail
E1	WTI is priced relative to Brent	WTI/Brent spread is a market-observable, stable relationship
E2	Calendar spreads reflect storage economics	Contango structure matches cost-of-carry for crude oil storage
E3	Seasonal shape in gas is stable year-on-year	Winter/summer demand patterns persist; disrupted by LNG, weather anomalies
E4	Location basis is a stable additive spread	Pipeline infrastructure is stable; disrupted by outages, regulatory changes
4.3 Carbon Market Assumptions
#	Assumption	Detail
C1	No seasonality in the forward curve	Carbon allowances do not reflect seasonal demand; entire curve shifts together
C2	Cost of carry is purely interest-rate-driven	No storage costs, no convenience yield for electronic allowances
C3	Regulatory framework remains stable	Cap trajectory and compliance rules do not change during curve horizon
C4	Interest rate used is the overnight rate for that currency	ESTR (EUR), SONIA (GBP), SOFR (USD), BBSW (AUD)
4.4 Metal Market Assumptions
#	Assumption	Detail
M1	LME prices are definitive market prices	LME is the benchmark for base metals globally
M2	Storage costs are proportional to spot price	Holds for most metals; warehouse premiums add complexity
M3	Lease rates for precious metals are stable	Gold lease rates are slow-moving; can spike during market stress
M4	LME standard dates adequately capture term structure	Standard maturities (Cash, 3M, 15M, 27M) represent the majority of liquidity
4.5 Agricultural Assumptions
#	Assumption	Detail
AG1	Crop calendar is stable year-on-year	Harvest dates may shift due to weather/climate change
AG2	Storage costs are linear over time	Warehouse costs are approximately linear for standardised storage
AG3	Convenience yield can be estimated from futures prices	Implied from the spread between futures and cost-of-carry-implied prices
5. Model Governance Framework
5.1 Governance Principles
A robust model governance framework for forward curves should follow these principles:

Independence – Model validation and approval must be independent from model development
Transparency – All methodologies, assumptions, and parameter choices must be documented
Proportionality – Governance intensity should be proportional to model risk and business materiality
Accountability – Clear ownership at every stage: development, validation, approval, ongoing monitoring
Continuous Review – Models must be regularly reviewed, not only at initial approval
5.2 Model Lifecycle
┌─────────────────────────────────────────────────────────────────────┐
│                    FORWARD CURVE MODEL LIFECYCLE                    │
│                                                                     │
│  DEVELOPMENT → DOCUMENTATION → VALIDATION → APPROVAL → DEPLOYMENT  │
│       ↑                                                     │       │
│       └─────────────── ONGOING MONITORING ──────────────────┘       │
└─────────────────────────────────────────────────────────────────────┘
Stage 1: Development
Quant team designs methodology
Technical Design Document (TDD) produced
Peer review within quant team
Stage 2: Documentation
Full methodology documentation
Mathematical derivations
Parameter choices justified
Known limitations disclosed
Stage 3: Independent Validation
Conducted by Independent Model Validation (IMV) or Model Risk Management (MRM)
Technical Validation Report (TVR) produced
Conceptual soundness review
Back-testing and benchmark testing
Stage 4: Approval
Model Risk Committee (MRC) or equivalent governance body
Conditions and limitations recorded
Approved use cases defined
Restrictions on use documented
Stage 5: Deployment
IT implementation review
User acceptance testing (UAT)
Training for model users
Stage 6: Ongoing Monitoring
Periodic revalidation (typically annual for significant models)
Trigger-based review (market structure change, significant P&L unexplained variance)
Ongoing performance metrics tracked
5.3 Roles and Responsibilities in Governance
Role	Responsibility
Curve Methodology Owner	Owns the methodology, proposes changes, ensures documentation currency
Front Office (Model User)	Uses model for trading; reports anomalies; provides expert judgment inputs
Independent Validation (MRM)	Validates conceptual soundness; back-tests; issues TVR
Model Risk Committee	Approves/rejects models; sets conditions and restrictions
Technology / Quant IT	Implements approved models in production systems
Internal Audit	Reviews compliance with governance framework
Risk Management	Consumes curves; monitors daily P&L unexplained
5.4 Model Documentation Standards
Every forward curve methodology must be documented with:

Executive Summary – high-level description of the methodology
Scope and Applicability – which products, geographies, and use cases
Mathematical Formulation – full derivation of the pricing formula
Input Data Specification – all inputs, their sources, and acceptable ranges
Parameter Choices – all parameters, their justification, and calibration procedure
Known Limitations – explicit statement of conditions under which the model may fail
Alternatives Considered – why this methodology was chosen over alternatives
Back-test Results – historical performance evidence
Sensitivity Analysis – model output sensitivity to key assumptions
Change Log – version history with rationale for changes
5.5 Curve Approval and Update Cycle
┌────────────────────────────────────────────────────────┐
│              CURVE UPDATE & APPROVAL CYCLE             │
│                                                        │
│  DAILY:   EOD curve production and quality checks      │
│  WEEKLY:  Curve owner review of illiquid tenors        │
│  MONTHLY: Cross-asset consistency review               │
│  QUARTERLY: Parameter recalibration review             │
│  ANNUALLY: Full methodology revalidation               │
│  AD HOC:  Major market structural changes              │
└────────────────────────────────────────────────────────┘
6. Model Validation
6.1 Validation Objectives
Model validation for forward curves must assess:

Conceptual Soundness – Is the theoretical framework appropriate for the market?
Data Quality – Are the inputs reliable, timely, and complete?
Implementation Accuracy – Is the model correctly coded and deployed?
Performance – Does the model produce accurate and stable prices?
Limitation Awareness – Are model users aware of conditions under which the model may be unreliable?
6.2 Validation Techniques
6.2.1 No-Arbitrage Testing
Verify that forward curves do not contain calendar arbitrage opportunities:

For all t₁ < t₂ < t₃:
No arbitrage requires: F(t₁) discounted to t₂ = F(t₂) [approximately]

Formally: |F(t, t₂) - F(t, t₁) × exp(r × (t₂ - t₁))| < ε
6.2.2 Back-Testing
Compare model-produced forward prices against subsequently realised spot prices:

Back-test Error(T) = F(t, T) - S(T)   [realised at time T]

Metrics:
  Mean Error (Bias)  = Average[F(t, T) - S(T)]
  RMSE               = sqrt(Average[(F(t, T) - S(T))²])
  Hit Rate           = % of months where F was within ±5% of S(T)
Interpretation: Systematic bias indicates a structural model error or missing risk premium.

6.2.3 Benchmark Comparison
Compare the model output against an independent benchmark:

Model_Spread = |Internal_Curve(T) - Benchmark_Curve(T)|

Acceptable tolerance bands should be defined per product (e.g., ±0.5% for crude oil)
Benchmark sources: broker consensus marks, third-party curve providers (e.g., OPIS, Argus, Platts).

6.2.4 Sensitivity Analysis
Assess how sensitive the model output is to key input assumptions:

Sensitivity_to_X = ∂F(t,T) / ∂X   (partial derivative)

For EU ETS:
∂F/∂S   = (1 + ESTR × (T-t)/365)         [spot sensitivity]
∂F/∂ESTR = S × (T-t)/365                  [rate sensitivity]
6.2.5 Stress Testing
Apply extreme but plausible scenarios to assess model behaviour:

Scenario	Description
Spot shock	Spot price moves ±20% instantaneously
Curve inversion	Backwardation scenario (extreme nearby tightness)
Interest rate shock	Rates move ±300bps
Data outage	Primary data source unavailable; reversion to secondary source
Liquidity drought	No market prices available for 5+ business days
6.3 Ongoing Performance Monitoring
Metric	Frequency	Alert Threshold
Curve change (absolute $)	Daily	3 × historical daily move
Cross-pillar arbitrage	Daily	Any violation
Source deviation	Daily	2σ vs previous 30-day vol
Back-test RMSE	Monthly	2× expected model error
Benchmark deviation	Weekly	agreed tolerance band
7. Challenges & Risk Factors
7.1 Data Quality and Availability Challenges
Challenge	Description	Mitigation
Illiquid tenors	No observable market prices beyond 1–3 years for many commodities	Use expert-judgment inputs with governance sign-off; disclose uncertainty
Source conflicts	Different data sources (Bloomberg, ICE, Platts) may provide different prices	Define a clear source hierarchy; document exceptions
Stale data	Data not updated intraday or delayed	Monitor data freshness; use automated staleness alerts
Data gaps	Public holidays, trading halts, system outages	Define fallback procedures; use last-known-good with age flagging
Outliers/errors	Fat-finger errors in broker quotes or exchange settlements	Automated spike detection; manual review process
7.2 Structural Market Challenges
Challenge	Description	Impact
Curve regime changes	Market transitions from contango to backwardation (or vice versa)	Model calibrated in one regime may be wrong in another
Market microstructure	Settlement prices may not reflect true fair value (e.g., illiquid settlement)	Curves carry model risk of input quality
New products	New markets (e.g., new carbon schemes, new gas hubs) may not have an established methodology	Requires ad hoc methodology development under time pressure
Liquidity evaporation	In stress events, markets may become untradeable	Model prices may diverge significantly from transactable prices
Seasonality changes	Climate change alters seasonal demand patterns (e.g., gas in Europe)	Historical seasonal adjustment factors become unreliable
7.3 Modelling Challenges
Challenge	Description	Mitigation
Interpolation choice	Different interpolation methods produce different intraday risk profiles	Document and standardise; validate against market practice
Extrapolation beyond last liquid point	No market evidence for long-dated tenors	Use model-based extrapolation with appropriate uncertainty disclosure
Missing convenience yield	Convenience yield is unobservable and must be implied	Back-calibrate from futures prices; validate stability
Cross-asset consistency	Curves for related products (e.g., crude oil and refined products) must be mutually consistent	Implement cross-asset consistency checks as part of daily quality control
Holiday calendars	Different calendars for different markets create edge cases in interpolation	Use standardised holiday calendar system; test edge cases
7.4 Governance and Operational Challenges
Challenge	Description
Decentralised marking	Front-office-driven marking creates conflicts of interest and inconsistent standards
Model creep	Small undocumented changes to models accumulate over time; methodology drift
Knowledge concentration	Methodology held in one person's head; creates key-person dependency
Legacy systems	Old systems may not support modern interpolation methods or real-time requirements
Regulatory changes	New regulations (FRTB, IFRS 13) may require methodology changes with short notice
7.5 Counterparty and Risk Challenges
Challenge	Description
Curve used for multiple purposes	Same curve used for trading P&L, risk, and financial reporting – conflicting requirements
Collateral disputes	Counterparties may have different curves, leading to margin call disputes
XVA impact	Forward curve level affects CVA, DVA, FVA, MVA calculations for derivatives
Stress VaR	Historical stressed scenarios may be based on outdated market regimes
8. Technology & Infrastructure
8.1 Current Technology Stack
System	Role
IMDS (Integrated Market Data System)	In-house application for curve construction and storage
Asset Control (MRS)	Primary market data repository
CMD (Commodity Marking Desktop)	Trader-facing UI for manual curve marking
FALCON	Next-generation computation and distribution platform
Bloomberg / Refinitiv	External market data sources
8.2 Data Templates and Standards
Template	Content
SC_COM_FUT_LSA	Commodity futures prices
SC_COM_VOL_LSA	Commodity volatilities
SC_COM_SPT_LSA	Commodity spot prices
SC_COM_SWP_LSA	Commodity swap prices
8.3 FALCON Migration
Standard Chartered is migrating commodity curve production from IMDS to FALCON:

Phase 1: PDS topic ingestion into FALCON
Phase 2: Intraday/EOD alignment and real-time curve production
Phase 3: Direct CMD–FALCON integration for trader marking
Benefits of FALCON:

Real-time computation (vs. EOD-only in legacy)
Unified framework across curves, volatilities, and smiles
Improved auditability and governance
Faster response to market events
8.4 Data Flow Architecture
External Sources                Internal Processing             Consumers
(Bloomberg, ICE,         →      IMDS / FALCON             →   Front Office (CMD)
 CME, Platts, LBMA)     →      Quality Control            →   Risk Systems
                         →      Curve Construction         →   Finance (P&L)
                         →      Asset Control (MRS)        →   Regulatory Reporting
9. Stakeholder Map & Responsibilities
9.1 Internal Stakeholders
Stakeholder	Role	Interaction with Forward Curve Team
Trading Desks	Primary curve users; provide expert judgment inputs	Daily: consume curves, provide manual marks for illiquid tenors
Commodity Risk	Risk management function	Daily: use curves for VaR, limits, exposure reporting
Independent Valuations Group (IVG)	Validates source data independence	Periodic: challenge and verify external data sources
Model Risk Management (MRM)	Independent model validation	At initial approval and annual revalidation
Finance / Product Control	P&L attribution and financial reporting	Daily: use curves for official P&L; IPV (Independent Price Verification)
Technology / Quant IT	System implementation	When methodologies change; ongoing maintenance
Compliance / Legal	Regulatory adherence	When regulatory changes affect methodology
Senior Management	Strategy and resource allocation	Periodic: governance reporting
9.2 External Stakeholders
Stakeholder	Role
Exchanges (ICE, CME, LME)	Provide settlement prices
Data Vendors (Bloomberg, Refinitiv, Platts)	Live and historical market data
Brokers	OTC market quotes for illiquid tenors
Regulators (PRA, FCA, etc.)	Set model risk and fair value standards
Auditors	External validation of methodology and fair value
10. Key Performance Metrics & Controls
10.1 Daily Controls
Control	Definition	Threshold
Curve completeness	% of required tenors with valid prices	100% mandatory
Data freshness	Maximum age of input data at EOD	< 4 hours for liquid; < 24h for illiquid
Arbitrage-free check	No calendar arbitrage in curve	Zero violations
Spike detection	Change vs. previous day > N × σ	Alert > 3σ; hard block > 5σ
Source reconciliation	Internal curve vs. external benchmark	Alert if > agreed tolerance
10.2 Weekly / Monthly Controls
Control	Frequency	Owner
IPV (Independent Price Verification)	Monthly	Finance / Product Control
Back-test performance review	Monthly	Curve Methodology Team
Benchmark deviation report	Weekly	Curve Methodology Team
Governance exception report	Monthly	MRM / Model Risk Committee
10.3 Quality Metrics Dashboard
The following metrics should be tracked and reported to governance committees:

Mean Absolute Deviation (MAD) of curves vs. benchmarks
Back-test Hit Rate – % of forward prices within tolerance of realised spot
Stale Data Events – number of instances where data freshness threshold was breached
Model Override Count – number of manual overrides applied to automated curves
Arbitrage Violations – number of arbitrage-free violations detected (target: zero)
11. Regulatory & Compliance Considerations
11.1 Relevant Regulatory Standards
Standard	Description	Relevance
IFRS 13	Fair Value Measurement – requires observable inputs where available; Level 1/2/3 hierarchy	Determines whether forward curve prices are Level 1 (exchange), Level 2 (observable), or Level 3 (model)
FRTB (Fundamental Review of the Trading Book)	Basel IV market risk rules; affects which risk factors can be modellable	Requires 250 days of daily observations for a risk factor to be modellable (RFET)
SR 11-7 (Federal Reserve)	US model risk management guidance	Best-practice standard for model governance globally
SS1/23 (PRA)	UK model risk management supervisory statement	UK-specific requirements for model risk management
EMIR / Dodd-Frank	Derivatives reporting and clearing	Affects trade lifecycle and collateral valuation
MiFID II	Market transparency and best execution	Affects pricing and documentation standards
11.2 IFRS 13 Fair Value Hierarchy
Level	Description	Examples for Commodity Curves
Level 1	Quoted prices in active markets for identical assets	Front-month exchange futures prices
Level 2	Observable inputs other than Level 1	Interpolated prices between liquid futures; broker quotes
Level 3	Unobservable inputs (model-based)	Long-dated tenors beyond liquid market; exotic seasonal adjustments
The proportion of a portfolio valued at Level 3 is a key risk metric for regulators and auditors.

11.3 FRTB Modellability Requirements
For a risk factor (e.g., a specific tenor of a commodity curve) to be deemed modellable under FRTB:

Requirement: ≥ 24 verifiable price observations per year
             (approximately one every 2 weeks)
             AND minimum 250 days of price history
Failing this, the risk factor must be treated as Non-Modellable Risk Factor (NMRF) with a punitive capital charge.

Implication for curve methodology: The team must maintain records of when prices are market-observable vs. model-derived, and track the RFET (Risk Factor Eligibility Test) for each tenor.

12. Role Competency Framework
12.1 Technical Competencies
Competency	Description	Level Required
Mathematical Finance	Stochastic calculus, no-arbitrage pricing, derivatives theory	Expert
Commodity Markets	Deep knowledge of energy, metals, agricultural market structure and fundamentals	Expert
Statistics & Econometrics	Time-series analysis, regression, volatility modelling	Advanced
Programming (Python)	Data analysis, model implementation, automation	Advanced
Model Validation	Back-testing methodology, benchmark comparison, sensitivity analysis	Advanced
Systems & Data	Familiarity with Bloomberg, market data systems, curve construction platforms	Intermediate–Advanced
12.2 Governance & Soft Competencies
Competency	Description
Stakeholder Management	Ability to manage and influence multiple senior stakeholders simultaneously
Communication	Ability to explain complex quantitative concepts clearly to non-technical audiences
Challenge & Independence	Willingness and ability to challenge assumptions made by front office or senior management
Documentation	Ability to write clear, precise, and complete model documentation
Decision-Making	Ability to make sound judgements under uncertainty and time pressure
Regulatory Awareness	Up-to-date knowledge of model risk and fair value regulations
12.3 Day-in-the-Life Activities
Daily:

Review curve quality dashboard; investigate any alerts or anomalies
Review any manual overrides applied by front office
Liaise with trading desks on any illiquid tenor marks
Monitor data freshness and source integrity
Weekly:

Produce benchmark deviation report
Review curve changes and assess whether methodology adjustments are needed
Attend cross-functional model governance calls
Monthly:

Produce back-test performance report
Contribute to Model Risk Committee reporting
Review and challenge IPV results from Finance
Quarterly:

Parameter recalibration review
Governance committee presentation on curve quality
Review any new products or market changes requiring methodology assessment
Annually:

Full methodology review and revalidation
Update of model documentation
Review of regulatory changes affecting methodology
13. Glossary of Terms
Term	Definition
ACCU	Australian Carbon Credit Unit – offset credit in Australian carbon market
Backwardation	Market structure where forward price < spot price
Basis	Difference between spot and futures price, or between two related prices
BBSW	Bank Bill Swap Rate – Australian interest rate benchmark
Calendar Spread	Price difference between two futures contracts for the same commodity, different months
Carry	The cost (or benefit) of holding a position in a commodity over time
Contango	Market structure where forward price > spot price
Convenience Yield	Benefit of holding physical inventory; reduces the forward price below pure cost-of-carry
CORSIA	Carbon Offsetting and Reduction Scheme for International Aviation
Cost of Carry	Financing + storage + insurance costs minus convenience yield
Crack Spread	Margin from refining crude oil into refined products
ESTR	Euro Short-Term Rate – overnight rate for EUR
EU ETS	European Union Emissions Trading System – cap-and-trade carbon scheme
FRTB	Fundamental Review of the Trading Book – Basel IV market risk framework
Forward Curve	A representation of expected future prices across different delivery dates
IPV	Independent Price Verification – Finance team's independent validation of fair values
LBMA	London Bullion Market Association – sets gold and silver benchmarks
LME	London Metal Exchange – primary exchange for base metals
MRM	Model Risk Management – function responsible for model validation and governance
NMRF	Non-Modellable Risk Factor – risk factor without sufficient price observations for FRTB
Pillar Points	Observable market-price tenors used as inputs to curve construction
RFET	Risk Factor Eligibility Test – FRTB test for modellability of a risk factor
SOFR	Secured Overnight Financing Rate – USD risk-free rate benchmark
SONIA	Sterling Overnight Index Average – GBP overnight rate benchmark
Term Structure	The relationship between price (or rate) and time-to-maturity
UK ETS	United Kingdom Emissions Trading System – post-Brexit UK carbon scheme
VaR	Value at Risk – statistical measure of potential loss
XVA	Collective term for valuation adjustments (CVA, DVA, FVA, MVA, KVA)
