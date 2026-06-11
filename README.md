Commodity Forward Curve Methodology
Comprehensive Reference Document
Prepared by: Commodity Quantitative Analytics
Date: June 2026
Classification: Internal – Restricted
Role: Forward Curve Methodology Lead / Senior Quantitative Analyst – Commodity & Energy

Table of Contents
Introduction & Business Context
Curve Definition & Core Theory
Forward Curve Modelling by Commodity Asset Class
3.1 Crude Oil (Brent & WTI)
3.2 Natural Gas
3.3 Refined Products
3.4 Carbon Markets (EU ETS, UK ETS, ACCU, CORSIA)
3.5 Base Metals (LME)
3.6 Precious Metals
3.7 Agricultural Commodities (Grains & Livestock)
3.8 Soft Commodities (Coffee, Sugar, Cocoa, Cotton)
3.9 Freight & Shipping
Interpolation & Extrapolation Methodologies
Model Assumptions by Asset Class
Model Governance Framework
Model Validation
Challenges & Risk Factors
Stakeholder Map & Responsibilities
Key Controls & Quality Metrics
Regulatory Considerations
Role Competency Framework
Glossary
1. Introduction & Business Context
1.1 Why Forward Curves Matter in Commodity Markets
Commodity forward curves are the single most important input to all commodity business activity. Every transaction — whether a futures trade, a physical commodity swap, an option on oil, a structured commodity financing deal, or a carbon credit trade — requires a forward curve to:

Price the transaction at inception
Mark the position to market daily for P&L purposes
Compute risk exposures (delta, gamma, vega) for risk limits
Calculate regulatory capital (VaR, stressed VaR, FRTB IMA/SA)
Produce hedge effectiveness calculations for accounting purposes
Settle margin calls on cleared derivatives
Without accurate, timely, and well-governed forward curves, no commodity business can operate. A one-dollar error in a crude oil forward curve multiplied across millions of barrels of notional can generate tens of millions of dollars of P&L error.

1.2 What Makes Commodity Forward Curves Different
Commodity forward curves behave very differently from interest rate yield curves or equity dividend curves. The key differences are:

Feature	Interest Rate Curves	Commodity Forward Curves
Tenor structure	Rolling periods (1M, 3M, 6M, 1Y)	Fixed calendar dates (Jan-27, Feb-27, Mar-27)
Continuity	Near-continuous observable market	Sparse; liquid only at certain contract months
Seasonality	None or mild	Strong in gas, grains, livestock, softs
Regime changes	Rate cycle-driven	Can switch between contango and backwardation
Physical drivers	Monetary policy expectations	Storage, weather, harvest, geopolitics, supply chain
Mean reversion	Moderate	Strong (especially freight and agricultural)
Convenience yield	Not applicable	Critical for energy and metals
Carry structure	Always positive (rate > 0)	Can be negative (backwardation)
1.3 The Role: Forward Curve Methodology Lead
This role is the quantitative owner of all commodity forward curve methodologies within the bank. The responsibilities span:

Design and maintain group-wide forward curve construction methodologies
Define standards and best practices for all commodity asset classes
Challenge methodology choices made by trading desks or technology
Lead model validation including back-testing and sensitivity analysis
Assess model limitations and determine suitability for use
Govern the curve approval, update, and revalidation cycle
Interface between trading desks, risk, finance, MRM, and technology
Drive continuous improvement of quantitative frameworks
1.4 Commodity Asset Class Scope
Asset Class	Sub-Products	Primary Exchange
Energy – Crude Oil	Brent, WTI, Dubai, Oman	ICE, CME/NYMEX
Energy – Natural Gas	Henry Hub, NBP, TTF, JKM	CME, ICE
Energy – Refined Products	RBOB Gasoline, Heating Oil, Diesel, Jet Fuel	CME, ICE
Carbon	EU ETS, UK ETS, ACCU, CORSIA	ICE, CBL
Base Metals	Copper, Aluminium, Zinc, Lead, Nickel, Tin	LME, SHFE
Precious Metals	Gold, Silver, Platinum, Palladium	LBMA, COMEX
Agricultural – Grains	Corn, Wheat, Soybeans, Soybean Meal, Soybean Oil	CBOT
Agricultural – Livestock	Live Cattle, Feeder Cattle, Lean Hogs	CME
Soft Commodities	Coffee (Arabica/Robusta), Sugar (#11/#5), Cocoa, Cotton	ICE US/EU
Freight	Capesize, Panamax, Supramax, Handysize	Baltic Exchange
2. Curve Definition & Core Theory
2.1 What is a Forward Curve?
A forward curve is a mapping from a set of future delivery dates T to prices F(t, T) — where t is today. Each point on the curve represents the price at which a commodity can be bought or sold today for delivery at that future date T.

F: T → F(t, T)    where t ≤ T
The forward curve provides a complete term structure of prices across all future delivery dates. Because markets only trade at a limited number of standardised contract months, the curve must be constructed by:

Taking observable market prices at liquid contract months (pillar points)
Interpolating between pillar points to fill in all intermediate dates
Extrapolating beyond the last liquid contract for long-dated exposures
2.2 Spot Price vs. Forward Price vs. Futures Price
These three concepts are related but distinct:

Concept	Symbol	Definition	Settlement
Spot Price	S(t)	Price for immediate delivery	T+2 typically
Forward Price	F(t,T)	OTC price agreed today for delivery at T	Physically at T
Futures Price	Fut(t,T)	Exchange-standardised version of forward	Cash-margined daily
In theory, for a storable commodity with no market frictions:

F(t, T) = Fut(t, T)   [equal under no-arbitrage with daily margining]
In practice, there are differences due to:

Convexity adjustment from daily margining of futures
Physical delivery vs. cash settlement differences
Basis risk between the futures delivery point and the actual delivery location
2.3 The Cost of Carry Framework
The foundational model for commodity forward pricing is the Cost of Carry relationship:

F(t, T) = S(t) × exp[(r + s - c) × (T - t)]
Where:

Variable	Meaning	Typical Range
r	Risk-free interest rate	3%–6% p.a.
s	Storage cost (% of commodity value per annum)	0.5%–5% p.a.
c	Convenience yield (benefit of holding physical stock)	0%–20%+ p.a.
T - t	Time to delivery in years	Days to 10 years
Intuition:

If you can buy the commodity today at S(t), store it, and finance the purchase at rate r, then the break-even forward price is S(t) × exp[(r+s) × (T-t)]
If there is a benefit to holding physical inventory (convenience yield c), this reduces the forward price
When c > r + s: Backwardation — it is more valuable to hold physical stock than a forward contract
When c < r + s: Contango — the curve slopes upward with storage costs
2.4 Contango vs. Backwardation
Contango:      F(t, T₁) < F(t, T₂)    for T₁ < T₂   [upward sloping curve]
Backwardation: F(t, T₁) > F(t, T₂)    for T₁ < T₂   [downward sloping curve]
Market State	Typical Conditions	Examples
Strong contango	Ample supply, high inventories, low demand	Crude oil in 2020 COVID crash
Mild contango	Normal market; reflects storage costs	Base case for most storable commodities
Flat curve	Supply/demand broadly balanced	Transition periods
Mild backwardation	Moderate supply tightness	Copper in demand surges
Strong backwardation	Severe nearby supply squeeze	Natural gas in winter cold snaps
2.5 Convenience Yield – Deep Dive
The convenience yield c is one of the most important and difficult-to-observe inputs in commodity forward curve construction. It is not directly traded but must be implied from market prices.

Economic meaning: The convenience yield represents the flow of services that accrues to the owner of a physical inventory but NOT to the holder of a futures contract. These services include:

Ability to meet unexpected customer demand
Input into a production process without waiting for delivery
Optionality to sell into a sudden price spike
Implied convenience yield calculation:

Given the spot price and a futures price:

c(t, T) = r + s - [ln(F(t,T)/S(t)) / (T-t)]
Convenience yield properties:

Always non-negative (you cannot be worse off by holding physical stock — you can always choose not to use it)
Mean-reverting: tends to revert to a long-run level
Inversely related to inventory levels: falls as inventories rise, spikes when inventories are critically low
Stochastic in nature: varies continuously with supply/demand conditions
2.6 Calendar Spreads
A calendar spread is the difference in price between two futures contracts for the same commodity but different delivery months:

Cal_Spread(M1, M2) = F(t, M2) - F(t, M1)    where M2 > M1
Calendar spreads are important because:

They are directly traded in most liquid commodity markets (more liquid than outright prices at distant maturities)
They reflect storage economics — the cost of carrying a commodity from M1 to M2
They are used to construct the forward curve sequentially from the front month
Under cost-of-carry:

Cal_Spread(M1, M2) = F(t, M1) × [exp((r + s - c) × (M2 - M1)) - 1]
2.7 Pillar Points and Curve Construction
The observable market provides prices only at specific pillar points (also called liquid tenors or key tenors):

Observable:  F(t, T₁), F(t, T₂), ..., F(t, Tₙ)   [liquid contract months]
Required:    F(t, τ) for ALL τ ∈ [t, Tₙ]          [complete curve]
The curve construction problem is to find a function F(t, ·) that:

Passes through (or near) all observable pillar prices
Is arbitrage-free (no calendar spread arbitrage)
Is smooth (no unrealistic kinks between months)
Reflects seasonal patterns where relevant
Is computationally stable and reproducible
3. Forward Curve Modelling by Commodity Asset Class
3.1 Crude Oil – Brent (ICE)
3.1.1 Market Structure
Brent crude oil is the world's primary oil price benchmark, used to price approximately two-thirds of all internationally traded crude oil. Key characteristics:

Exchange: ICE Futures Europe (London)
Delivery: North Sea BFOE basket (Brent, Forties, Oseberg, Ekofisk, Troll)
Contract size: 1,000 barrels
Settlement: Physical (front month) / Cash (deferred)
Liquidity: Very high for 1–18 months; moderate 18M–3Y; illiquid beyond 3Y
Trading hours: 01:00–23:00 London time
EOD settlement: ICE publishes official settlement prices daily at 19:30 London time
3.1.2 Forward Curve Construction Methodology
Step 1 – Collect Input Data

Primary:   ICE settlement prices for all listed contract months
Secondary: Bloomberg live prices (intraday)
Tertiary:  Broker quotes for illiquid months (typically >18M)
Step 2 – Identify Pillar Points

The most liquid and reliable prices are used as curve anchors:

Front month (M1)
Second month (M2)
Third month (M3)
Quarterly contracts (M4, M7, M10...)
December contracts for each calendar year
Step 3 – Interpolation Between Pillars

For dates between pillar points, apply calendar spread interpolation:

F(t, τ) = F(t, T₁) + [F(t, T₂) - F(t, T₁)] × (τ - T₁) / (T₂ - T₁)
Where T₁ and T₂ are the adjacent pillar points surrounding τ.

Step 4 – Extrapolation Beyond Last Liquid Point

For tenors beyond the last liquid contract (typically >3Y):

Flat extrapolation: F(t, τ) = F(t, Tₙ) for all τ > Tₙ
Slope extrapolation: apply the slope of the last observable calendar spread
Model-based: use a mean-reversion model to extrapolate
Step 5 – Quality Checks

✓ No calendar spread arbitrage:    F(t, T₂) ≥ F(t, T₁) - ε   (contango check)
✓ No negative prices:              F(t, T) > 0   for all T
✓ Consistency with ICE settlement: |Internal(T) - ICE_Settlement(T)| < $0.10 for liquid months
✓ Spike detection:                 |F_today(T) - F_yesterday(T)| < 3σ_historical
3.1.3 Mathematical Formulas
For liquid months (direct market observation):

F_Brent(t, Tᵢ) = ICE_Settlement(Tᵢ)
For broken dates (linear interpolation):

F_Brent(t, τ) = F_Brent(t, T₁) + [(F_Brent(t, T₂) - F_Brent(t, T₁)) × (τ - T₁)/(T₂ - T₁)]
3.1.4 Worked Example
Date: 11 June 2026

ICE Settlement Prices:
  Brent Jul-26  = $78.50/bbl
  Brent Aug-26  = $77.90/bbl    (Cal spread Jul/Aug = -$0.60)
  Brent Sep-26  = $77.40/bbl    (Cal spread Aug/Sep = -$0.50)
  Brent Dec-26  = $76.00/bbl
  Brent Dec-27  = $73.50/bbl

Broken date (15 August 2026 – mid-August):
  T₁ = Aug-26 expiry date = 15 Jul 2026 → F = $77.90
  T₂ = Sep-26 expiry date = 15 Aug 2026 → F = $77.40

  Days from T₁ to target = 31 days
  Days T₁ to T₂ = 31 days

  F(15-Aug) = $77.90 + [($77.40 - $77.90) × 31/31]
            = $77.90 + (-$0.50 × 1.0)
            = $77.40/bbl
3.1.5 Key Assumptions
ICE settlement prices represent the definitive end-of-day market price
Linear interpolation accurately captures the market's pricing between pillar points
The curve may be in contango or backwardation; no structural direction is assumed
Beyond 3 years, flat extrapolation is applied unless broker quotes exist
3.2 Crude Oil – WTI (CME/NYMEX)
3.2.1 Market Structure
West Texas Intermediate (WTI) is the primary US crude oil benchmark:

Exchange: CME/NYMEX (New York)
Delivery: Cushing, Oklahoma (pipeline hub)
Contract size: 1,000 barrels
Grade: Light, sweet crude (API ~39.6°, Sulphur ~0.24%)
Historical relationship: WTI typically trades at 
5 discount to Brent (location + quality)
Exception: WTI/Brent spread can invert due to Cushing storage constraints (widened sharply in 2011–2014, went negative in April 2020)
3.2.2 Forward Curve Construction Methodology
WTI is constructed relative to Brent using the WTI/Brent spread, rather than in isolation:

Step 1 – Front Month Construction

WTI_M1 = Brent_M1 + WTI_Brent_Spread_M1
Step 2 – Subsequent Month Construction (Sequential Calendar Spread Method)

WTI_M2 = WTI_M1 + Cal_Spread(M1, M2)
WTI_M3 = WTI_M2 + Cal_Spread(M2, M3)
WTI_Mᵢ = WTI_Mᵢ₋₁ + Cal_Spread(Mᵢ₋₁, Mᵢ)    for i = 2, 3, ..., n
Step 3 – Calendar Spread Sources

Tenor	Source
M1–M6	Directly observable CME settlement prices
M6–M18	Market calendar spread quotes (brokers)
M18+	Trader judgment / linear interpolation of observable spreads
3.2.3 Mathematical Formulas
WTI(t, M1)  = Brent(t, M1) + Δ_WTI_Brent(t)

WTI(t, Mᵢ) = WTI(t, Mᵢ₋₁) + CS(Mᵢ₋₁, Mᵢ)     where CS = calendar spread

Δ_WTI_Brent(t) = observable WTI/Brent spread at time t (traded as ICE WTI/Brent swap)
3.2.4 Worked Example
Brent_Jul-26  = $78.50
WTI/Brent spread = -$2.80
WTI_Jul-26  = $78.50 - $2.80 = $75.70/bbl

CME Calendar Spreads:
  Jul/Aug = -$0.35
  Aug/Sep = -$0.30
  Sep/Oct = -$0.25

WTI_Aug-26  = $75.70 - $0.35 = $75.35/bbl
WTI_Sep-26  = $75.35 - $0.30 = $75.05/bbl
WTI_Oct-26  = $75.05 - $0.25 = $74.80/bbl
3.2.5 Key Assumptions
WTI price is fundamentally driven by Brent, adjusted for the cross-market spread
CME calendar spreads reflect the marginal cost of storage at Cushing
The WTI/Brent spread is mean-reverting but can be volatile during infrastructure events
Cushing storage utilisation is the primary driver of short-dated calendar spread shape
3.3 Natural Gas
3.3.1 Market Structure and Major Hubs
Natural gas is priced regionally, with no single global benchmark:

Hub	Region	Exchange	Unit
Henry Hub (HH)	US Gulf Coast	CME/NYMEX	$/MMBtu
NBP	UK	ICE	p/therm
TTF	Netherlands (European benchmark)	ICE	€/MWh
JKM	Japan/Korea (Asian LNG)	CME	$/MMBtu
3.3.2 Seasonality – The Defining Feature of Natural Gas Curves
Natural gas forward curves exhibit the strongest seasonality of any commodity:

Winter peak: December–February (heating demand)
Summer shoulder: April–October (lower demand; storage injection)
Summer cooling: July–August (air conditioning demand creates secondary peak)
Storage cycle: April–October = injection season; November–March = withdrawal
The seasonal shape is constructed by combining:

F_gas(t, T) = F_base(t, T) + Seasonal_Premium(T) + Storage_Adjustment(T)
3.3.3 US Natural Gas – Henry Hub Construction
Primary methodology:

NG_HH(t, T) = CME_NYMEX_Settlement(T)    for liquid months (M1–M12)

For inter-month dates:
NG_HH(t, τ) = Linear interpolation between adjacent monthly settlements
Location basis for other US hubs:

NG_Basis_Location(t, T) = NG_HH(t, T) + Basis_Spread_Location(T)

Examples:
  NG_Permian(t,T)   = NG_HH(t,T) - Waha_Basis(T)    [historically negative: pipeline-constrained]
  NG_Northeast(t,T) = NG_HH(t,T) + Algonquin_Basis(T) [positive in winter: congestion premium]
3.3.4 European Natural Gas – TTF Construction
TTF(t, T) = ICE_TTF_Settlement(T)    for liquid months
TTF(t, τ) = Linear interpolation for broken dates
The TTF curve exhibits:

Strong winter premium (typically €5–15/MWh above summer)
Summer storage injection floor (preventing extreme summer weakness)
LNG import parity acting as a ceiling in winter
3.3.5 Seasonal Factor Application
Where seasonal patterns are not fully captured by futures prices (illiquid months), a seasonal factor is applied:

Seasonal_Factor(Month) = Historical_Average_Price(Month) / Annual_Average_Price

F_adjusted(t, T) = F_base(t, T) × Seasonal_Factor(Month(T))
Example seasonal factors for Henry Hub (illustrative): | Month | Seasonal Factor | Explanation | |---|---|---| | January | 1.25 | Peak winter demand | | February | 1.20 | Peak winter demand | | April | 0.90 | Low shoulder season | | July | 1.05 | Summer cooling demand | | October | 0.88 | Pre-winter shoulder | | December | 1.18 | Early winter demand |

3.3.6 Key Assumptions
Gas markets are regionally segmented; no global arbitrage mechanism
LNG provides a loose pricing linkage between Henry Hub, NBP/TTF, and JKM
Seasonal patterns derived from historical data are representative of future patterns
Storage levels are the primary short-term driver of seasonal premium/discount
3.4 Refined Products
3.4.1 Products and Market Structure
Product	Exchange	Benchmark
RBOB Gasoline	CME/NYMEX	$/gallon
Heating Oil (HO)	CME/NYMEX	$/gallon
Diesel / ULSD	ICE, CME	
/tonne
Jet Fuel / Kerosene	OTC / broker	$/barrel
Fuel Oil (HSFO, VLSFO)	OTC / Platts	$/tonne
3.4.2 Crack Spread Methodology
Refined product forward curves are constructed relative to the crude oil benchmark using crack spreads — the processing margin of converting crude oil into refined products:

Product_Forward(t, T) = Crude_Benchmark(t, T) + Crack_Spread(t, T) + Location_Differential(t, T)
RBOB Gasoline:

RBOB(t, T) = WTI(t, T) + RBOB_Crack(t, T) + Gulf_Coast_Differential
Heating Oil:

HO(t, T) = WTI(t, T) + HO_Crack(t, T) + Location_Differential
Crack spread definition:

1-1 crack: Gasoline vs. Crude: RBOB - WTI
3-2-1 crack (refinery): (2 × RBOB + 1 × HO) / 3 - WTI
3.4.3 Seasonal Patterns in Refined Products
Product	Season	Effect
Gasoline	April–September	Summer driving season; demand rises; crack spreads widen
Heating Oil / Diesel	October–March	Winter heating/transport demand; crack spreads widen
Jet Fuel	June–August	Summer travel peak
3.4.4 Key Assumptions
Refined product prices are fundamentally derived from crude oil via crack spreads
Crack spreads reflect refinery utilisation, seasonal demand, and refinery configuration
Regulations (IMO 2020 sulphur cap, EV transition) structurally affect crack spread levels over time
3.5 Carbon Markets
3.5.1 Why Carbon Curves Are Unique
Carbon market forward curves are structurally different from physical commodity curves:

No seasonality: Entire curve moves up or down together; there is no seasonal demand pattern for the right to emit CO₂
No convenience yield: Allowances are electronic registry entries; there is no benefit from holding physical stock
No storage cost: Electronic storage is negligible
Therefore: pure cost of carry — the forward price is determined solely by the spot price and the financing rate
The fundamental pricing equation:

F(t, T) = S(t) × exp(r × (T - t))
Where r is the overnight risk-free rate for the currency of the allowance.

3.5.2 EU ETS (European Union Emissions Trading System)
Background:

World's largest carbon market by volume and value
Phase 4 (2021–2030): annual reduction in cap of 4.2% from 2024 (increased from 2.2%)
Covers power, industrial, and aviation sectors within the EU + EEA
Compliance obligation: surrender allowances by 30 April each year for prior year emissions
EUA (EU Allowance) = 1 tonne of CO₂ equivalent
Forward Curve Methodology:

F_EUA(t, T) = S_EUA(t) × exp(ESTR × (T - t))
Simplified (actual):

F_EUA(t, T) = S_EUA(t) × (1 + ESTR × (T - t) / 365)
Where:

S_EUA(t) = ICE EUA spot price or Dec-nearest-year futures price
ESTR = Euro Short-Term Rate (ECB-published overnight rate)
T - t = days to delivery / 365
Broken date pricing:

Linear interpolation between the two nearest December contract prices:

F_EUA(t, τ) = F_EUA(t, Dec_n) + [(F_EUA(t, Dec_{n+1}) - F_EUA(t, Dec_n)) × (τ - Dec_n)/(Dec_{n+1} - Dec_n)]
Asian Swap pricing:

For a calendar-year average price swap (common product):

Asian_Swap_Price = (1/N) × Σᵢ F_EUA(t, Tᵢ)    for all business days Tᵢ in the tenor period
Worked Example:

Date: 11 June 2026
EUA Dec-26 ICE = €68.50/tonne
EUA Dec-27 ICE = €71.20/tonne
ESTR = 2.65%

For 1 September 2026 (broken date):
  Days from 11-Jun to 1-Sep = 82 days
  Approx interpolation:
  
  Days in year 2026 Dec contract: Spot → Dec-26
  Days Dec-26 → Dec-27 = 365

  F(1-Sep-26) = €68.50 × (1 + 0.0265 × 82/365)
              = €68.50 × 1.00595
              = €68.91/tonne

For Asian Swap (Jul-Sep 2026 average):
  Average of F(t, Tᵢ) for each business day in Jul–Sep 2026
  = Average of approximately 66 daily forward prices
  = approximately €68.70–€68.90/tonne
3.5.3 UK ETS (United Kingdom Emissions Trading System)
Post-Brexit UK carbon market, launched January 2021:

F_UKA(t, T) = S_UKA(t) × (1 + SONIA × (T - t) / 365)
Where:

S_UKA(t) = ICE UKA spot or Dec futures price
SONIA = Sterling Overnight Index Average (Bank of England)
Coverage: UK power, industrial, aviation sectors
UKA (UK Allowance) = 1 tonne CO₂ equivalent
UK cap declining by ~4.1% per year
3.5.4 ACCU (Australian Carbon Credit Units)
F_ACCU(t, T) = S_ACCU(t) × (1 + BBSW_90d × (T - t) / 365)
Where:

BBSW_90d = 90-day Bank Bill Swap Rate (Australian benchmark)
Very limited secondary market; most pricing is OTC or bilateral
Spot price is the primary reference; forward prices are model-derived for most tenors
Australian government is active buyer (Safeguard Mechanism credits)
3.5.5 CORSIA (Carbon Offsetting and Reduction Scheme for International Aviation)
F_CORSIA(t, T) = S_CORSIA(t) × (1 + SOFR × (T - t) / 365)
Where:

SOFR = Secured Overnight Financing Rate (USD)
Very illiquid; primarily theoretical pricing
Applies to international aviation sector emissions from 2021
Eligible credits include ACCU, REDD+, VCS, Gold Standard offsets
3.5.6 Carbon Market Sensitivities
For EU ETS:

∂F/∂S    = (1 + ESTR × (T-t)/365)          [Spot Delta: ~1.0 for short dates]
∂F/∂ESTR = S × (T-t)/365                    [Rate Delta: small for < 1Y; grows for longer dates]
For a 1-year forward:

If ESTR = 3%, S = €70:
  ∂F/∂ESTR = €70 × 365/365 = €70 per 1% rate move
  = €0.70 per 10bp rate move   [immaterial for most trading purposes]
This confirms carbon forward curves are predominantly spot-driven, with interest rate sensitivity being secondary.

3.6 Base Metals (LME)
3.6.1 LME Market Structure
The London Metal Exchange (LME) is the world's premier base metals exchange:

Metals traded: Copper, Aluminium (Primary & Alloy), Zinc, Lead, Nickel, Tin, Cobalt, Molybdenum
Contract structure: Unique – daily prompt dates out to 3 months, then monthly out to 63 months (and 123 months for some contracts)
LME standard dates:
Cash (T+2)
Tom (T+1, for ring/inter-office)
1 Week, 2 Weeks
Each daily date out to 3 months
Monthly: every 3rd Wednesday out to 63 months (5.25 years)
Settlement: LME publishes official bid/ask at ring close (London 12:35 BST)
Physical delivery: Can be taken at 600+ LME-approved warehouses globally
3.6.2 Cost of Carry for Base Metals
F_Metal(t, T) = S_Metal(t) × exp[(r + s - c) × (T - t)]
For base metals:

r = USD SOFR (base rate for LME metals)
s = physical storage cost at LME warehouse (varies by metal and location)
c = convenience yield (significant when nearby supply is very tight)
Typical storage costs:

Metal	Storage Cost (% p.a.)	Notes
Copper	0.3%–0.5%	Relatively compact; low warehouse cost
Aluminium	1.0%–2.0%	Bulky; high warehouse footprint
Zinc	0.4%–0.6%	Moderate
Nickel	0.5%–0.8%	Moderate
Tin	0.3%–0.5%	Low volume
Lead	0.4%–0.6%	Moderate
3.6.3 Forward Curve Construction – LME Copper Example
Step 1: Collect LME official prices

LME Copper Cash    = $9,200/tonne
LME Copper 3M     = $9,150/tonne   (backwardation of $50)
LME Copper 15M    = $9,320/tonne   (contango of $120 from 3M)
LME Copper 27M    = $9,450/tonne
Step 2: Identify contango/backwardation structure

3M spread = Cash - 3M = $9,200 - $9,150 = +$50 backwardation
15M spread = 15M - 3M = $9,320 - $9,150 = +$170 contango
Step 3: Interpolate between standard LME dates

For any broken date τ between standard LME dates T₁ and T₂:

F_Cu(t, τ) = F_Cu(t, T₁) + [(F_Cu(t, T₂) - F_Cu(t, T₁)) × (τ - T₁)/(T₂ - T₁)]
Worked example – 9-month copper:

LME Copper 3M  = $9,150/tonne   (T₁ = 3M)
LME Copper 15M = $9,320/tonne   (T₂ = 15M)

F_Cu(9M) = $9,150 + [($9,320 - $9,150) × (9 - 3)/(15 - 3)]
           = $9,150 + [$170 × 6/12]
           = $9,150 + $85
           = $9,235/tonne
3.6.4 Warehouse Premium and Location Basis
LME prices represent delivery at any LME-approved warehouse globally. In practice, physical buyers pay a premium over LME for delivery at specific locations:

Physical_Price = LME_Price + Regional_Premium + Port_Differential + Quality_Premium

Examples:
  Copper CIF Rotterdam = LME_Cu + European_Copper_Premium  (typically $80–$180/tonne)
  Copper CIF Shanghai  = LME_Cu + Shanghai_Copper_Premium  (varies; driven by SHFE/LME arbitrage)
Regional premiums are tracked separately and overlaid on the LME forward curve for physical pricing.

3.6.5 Aluminium – Additional Complexity
Aluminium has an additional complexity: warehouse queues. During periods of LME rule manipulation (pre-2014), massive aluminium stocks were held in LME warehouses with load-out queues of 18+ months. This created:

Large super-contango in the forward curve (financing costs + rent)
Regional premium spikes as physical buyers paid large premiums to avoid the queue
Decoupling between LME forward curve and physical delivery economics
The LME introduced minimum load-out rules in 2014 to address this, but premium/discount structures remain important for aluminium curve construction.

Al_Physical(t, T) = LME_Al(t, T) + Midwest_Premium(t, T)    [US market]
Al_Physical(t, T) = LME_Al(t, T) + Rotterdam_Duty_Unpaid_Premium(t, T)   [European market]
3.6.6 Key Assumptions for Base Metals
LME settlement prices are the definitive global reference price
Standard LME dates capture the full range of market liquidity
Storage costs are approximately proportional to spot price
Regional premiums are additive to LME prices (no multiplicative interaction)
SHFE/LME arbitrage keeps Chinese and global prices broadly aligned (with exceptions during capital control events)
3.7 Precious Metals
3.7.1 Gold – Market Structure
Gold occupies a unique position: it is simultaneously a commodity and a monetary asset, used as a store of value by central banks. Key characteristics:

Benchmark: LBMA (London Bullion Market Association) AM/PM Fix
OTC market: LBMA-cleared OTC forwards and spot
Exchange: COMEX (CME Group) for futures
Unit: Troy ounce (oz) or kilograms
Purity: LBMA Good Delivery = 995 fineness minimum
Central bank gold: ~33,000 tonnes held by central banks globally; actively lent into market
3.7.2 Gold Forward Methodology – Interest Rate minus Lease Rate
Gold is unique because it can be leased (borrowed and on-lent). The gold lease rate is the interest rate paid to borrow gold from a central bank or institutional holder.

F_Gold(t, T) = S_Gold(t) × exp[(r_USD - r_Lease) × (T - t)]
Simplified:

F_Gold(t, T) = S_Gold(t) × (1 + (r_USD - r_Lease) × (T - t) / 365)
Where:

r_USD = USD SOFR (or USD overnight/LIBOR term rate)
r_Lease = Gold lease rate (GOFO – Gold Forward Offered Rate, now implied from gold forward market)
Gold Forward Rate (GFR):

GFR = r_USD - r_Lease     [the net carry of a synthetic gold forward]
When r_USD > r_Lease: gold forward curve is in contango (upward sloping) When r_USD < r_Lease: gold forward curve is in backwardation (very rare)

Worked Example:

Gold Spot         = $2,350/oz
USD Rate (SOFR)   = 5.25%
Gold Lease Rate   = 0.45%
GFR               = 5.25% - 0.45% = 4.80%

Gold_3M  = $2,350 × (1 + 0.048 × 90/365) = $2,350 × 1.01184 = $2,377.82/oz
Gold_6M  = $2,350 × (1 + 0.048 × 180/365) = $2,350 × 1.02367 = $2,405.62/oz
Gold_1Y  = $2,350 × (1 + 0.048 × 365/365) = $2,350 × 1.04800 = $2,462.80/oz
3.7.3 Silver
Silver has a higher industrial demand component (~55% of demand) than gold. Its forward curve follows the same structure but with higher and more volatile lease rates:

F_Silver(t, T) = S_Silver(t) × (1 + (r_USD - r_Silver_Lease) × (T - t) / 365)
Silver lease rates: typically 0.5%–2.5% p.a. (vs. 0.1%–1.0% for gold)

The higher lease rate means silver's forward curve carries at a lower rate than gold's, all else equal.

3.7.4 Platinum Group Metals (Platinum & Palladium)
PGM (Platinum Group Metals) have a much smaller lease market than gold or silver:

F_PGM(t, T) = NYMEX_Futures(T)    for liquid months

For illiquid months:
F_PGM(t, T) = F_PGM(t, T_last_liquid) × (1 + r_USD × (T - T_last_liquid)/365)
Palladium-specific behaviour:

Palladium has exhibited severe backwardation (2018–2022) due to supply deficit
Demand concentrated in autocatalysts (gasoline engine catalytic converters)
South African supply (Norilsk, Impala, Anglo American Platinum) is critical
EV transition creates long-run demand destruction pressure on the curve
3.7.5 Key Assumptions – Precious Metals
LBMA AM/PM Fix prices represent definitive market benchmarks for spot gold/silver
Gold lease rates are slow-moving and can be implied from the gold forward market
The USD interest rate is the dominant driver of precious metal forward curve shape
Lease rate stability is the key assumption; it breaks down during gold/silver short squeezes or banking stress
3.8 Agricultural Commodities
3.8.1 Grains – Market Structure
Grain	Exchange	Contract Months	Unit	Size
Corn	CBOT	Mar, May, Jul, Sep, Dec	$/bushel	5,000 bushels
Wheat (SRW)	CBOT	Mar, May, Jul, Sep, Dec	$/bushel	5,000 bushels
Wheat (HRW)	KCBT/CME	Mar, May, Jul, Sep, Dec	$/bushel	5,000 bushels
Soybeans	CBOT	Jan, Mar, May, Jul, Aug, Sep, Nov	$/bushel	5,000 bushels
Soybean Meal	CBOT	Jan, Mar, May, Jul, Aug, Sep, Oct, Dec	$/short ton	100 short tons
Soybean Oil	CBOT	Jan, Mar, May, Jul, Aug, Sep, Oct, Dec	cents/lb	60,000 lbs
3.8.2 Agricultural Curve Construction – Full Cost of Carry with Seasonality
The full cost of carry for grain storage:

F_Grain(t, T) = S(t) × exp[(r + s + i - c) × (T - t)]
Where:

r = financing rate
s = physical storage cost per bushel per month (~
0.05/bu/month)
i = insurance and quality deterioration (~0.5%–1.5% p.a.)
c = convenience yield (high near harvest, low at marketing year peak)
In practice, the forward curve is constructed from CBOT futures directly:

F_Grain(t, Tᵢ) = CBOT_Settlement(Tᵢ)    for all listed contract months
For inter-contract dates, linear interpolation is applied:

F_Grain(t, τ) = F(t, T₁) + [(F(t, T₂) - F(t, T₁)) × (τ - T₁)/(T₂ - T₁)]
3.8.3 The Crop Calendar and Its Impact on Forward Curves
The crop calendar drives the seasonal shape of grain forward curves. US corn example:

Event	Timing	Impact on Curve
Planting	April–May	Uncertainty about crop size; possible risk premium
Growing season	June–August	Weather risk highest; curve can spike if drought
Harvest	September–November	Supply increases; spot price weakens vs. deferred
Marketing year end	August 31	Old crop/new crop spread reflects carry and crop size
Old crop vs. New crop spread:

The most important spread in grain markets:

Old_New_Spread = F(t, Jul-current_year) - F(t, Dec-current_year)
A wide old/new spread (old crop expensive vs. new crop) indicates:

Current supplies are tight
Expectations that the new crop will relieve the tightness
High carry across the crop year boundary
3.8.4 Soybean Complex – Crush Spread
The crush spread reflects the value of processing soybeans into soybean meal and oil:

Crush_Value = (Soybean_Meal_Value + Soybean_Oil_Value) - Soybean_Cost
            = (11 × Meal_Price + 11 × Oil_Price × 0.0299) - Soybean_Price

Where:
  11 bushels of soybeans → 1 short ton of meal + 11 lbs × 0.0299 of oil (per bushel basis)
Soybean meal and oil forward curves are constructed to be internally consistent with the soybean curve via the crush spread.

3.8.5 Wheat – Multiple Grade Complexity
Wheat has multiple grades and locations, creating a complex basis structure:

Wheat_HRW(t, T) = Wheat_SRW(t, T) + HRW_SRW_Spread(T)
Wheat_SRWS(t, T) = Wheat_SRW(t, T) + Protein_Premium(T) + Location_Basis(T)
HRW (Hard Red Winter) typically trades at a premium or discount to SRW (Soft Red Winter) depending on crop quality and export demand.

3.8.6 Livestock – Biological Growth Model
Livestock cannot be stored like grain. The forward curve is driven by the biological cycle:

Live Cattle:

LV_Cattle(t, T) = Feeder_Cattle(t, T_placement) × Weight_Gain_Factor 
                + Feed_Cost(T_placement, T) 
                + Processing_Margin
                + Seasonal_Demand_Premium(T)

Where:
  Weight_Gain_Factor ≈ 1.4 (1,300lb finished weight / 900lb feeder weight)
  Feed_Cost = Corn_Forward × Feed_Conversion_Ratio (typically 6.5–7.0 lbs corn per lb gain)
Lean Hogs:

LN_Hogs(t, T) = Current_Hog_Price + Feed_Cost_Adjustment(T) 
              + Seasonal_Demand_Factor(T)
              + Packer_Margin_Adjustment

Seasonal factors for hogs:
  Spring/Summer: 1.05 (grilling season demand)
  Winter holidays: 1.08 (ham demand)
  February–March: 0.92 (seasonal trough)
3.8.7 Key Assumptions – Agricultural
CBOT futures prices are the definitive market prices for US grains
Storage costs are approximately constant per unit time (linear accumulation)
The crop calendar is stable year-on-year; weather is the primary source of deviation
Convenience yield can be accurately implied from the spread between spot and nearby futures
The crush spread relationship is stable (varies with crushing capacity and crush margin economics)
3.9 Soft Commodities
3.9.1 Coffee (Arabica and Robusta)
Market structure:

Type	Exchange	Contract Months	Unit	Currency
Arabica (Coffee C)	ICE US (New York)	Mar, May, Jul, Sep, Dec	¢/lb	USD
Robusta	ICE Europe (London)	Jan, Mar, May, Jul, Sep, Nov	$/tonne	USD
Arabica represents the premium quality market (grown at high altitude: Brazil, Colombia, Ethiopia). Robusta is the commodity-grade market (Vietnam, Indonesia, Brazil).

Forward curve construction:

Arabica(t, T)  = ICE_C_Settlement(T)                          [for liquid months]
Arabica(t, τ)  = Linear interpolation between adjacent months [for broken dates]
Brazilian Real adjustment (critical):

Brazil produces ~35% of world Arabica supply. Brazilian farmer selling behaviour is heavily influenced by BRL/USD exchange rate:

Arabica_Adjusted(t, T) = Arabica_Base(t, T) 
                        + FX_Sensitivity × ΔBRL_USD_Forward(t, T)
                        + Weather_Risk_Premium(T)
                        + Crop_Calendar_Adjustment(T)
Key weather risks:

February–March frost risk in Brazil's Minas Gerais coffee region
Flowering season (October–November) soil moisture
Arabica/Robusta differential:

The spread between Arabica and Robusta is a key market indicator:

Arabica_Robusta_Spread(t, T) = Arabica(t, T) - Robusta_Equivalent(t, T)

Typical range: 20–80 ¢/lb (Arabica premium)
Drivers: quality preference, supply imbalances, roaster blending decisions
3.9.2 Sugar
Type	Exchange	Contract Months	Unit
Sugar #11 (Raw)	ICE US	Mar, May, Jul, Oct	¢/lb
Sugar #5 (White)	ICE Europe	Mar, May, Aug, Oct, Dec	$/tonne
Raw Sugar (#11) – Ethanol Parity Model:

Brazil is the world's largest sugar producer and exporter. Brazilian mills make a dynamic allocation decision between sugar and ethanol production based on price relativities. This creates an ethanol parity price that acts as a floor for sugar:

Ethanol_Parity_Price = Ethanol_Price_Brazil × Conversion_Factor / Exchange_Rate
                      (approximately $0.12–$0.14/lb in normal conditions)

Sugar_11(t, T) = max(ICE_Futures(T), Ethanol_Parity(T)) × BRL_USD_Adjustment(T)
               + India_Export_Premium(T)                  [when India restricts exports]
               + Thai_Supply_Factor(T)
White Sugar premium (Sugar #5 over #11):

White_Premium(T) = Sugar_5(t,T) - Sugar_11(t,T)_equivalent
                 = Refining_Margin + Quality_Premium + Location_Premium

Typical white premium: $30–$80/tonne
High white premium: refinery bottleneck or EU/white-market-specific demand
Worked Example:

Sugar #11 Mar-27  = 21.50 ¢/lb
BRL/USD forward   = 5.20
Ethanol parity    = 20.80 ¢/lb  (below market; ethanol parity not binding)
White premium     = $55/tonne

Sugar #5 Mar-27   = (21.50 ¢/lb × 22.046 lb/kg × 10 kg/tonne / 100) + $55
                  = $473.99/tonne + $55
                  = $528.99/tonne
3.9.3 Cocoa
Exchange	Contract Months	Unit
ICE US (Cocoa)	Mar, May, Jul, Sep, Dec	$/tonne
ICE Europe (Cocoa)	Mar, May, Jul, Sep, Dec	£/tonne
Cocoa price is heavily influenced by West African supply (Ivory Coast + Ghana = ~60% of world production):

Forward curve construction:

Cocoa(t, T) = ICE_Settlement(T)                              [liquid months]
Cocoa(t, τ) = Linear interpolation                           [broken dates]
            + Weather_Risk_Premium(T)                        [during crop risk periods]
            + Government_Policy_Adjustment(T)                [GCC certification, SWAC scheme]
Processing spread (grind spread):

Grind_Value(T) = Butter_Price(T) × Butter_Yield + Powder_Price(T) × Powder_Yield
               - Bean_Price(T) × Input_Factor

Where:
  Butter_Yield  ≈ 0.395 tonnes butter per tonne beans
  Powder_Yield  ≈ 0.530 tonnes powder per tonne beans
  (remaining ~7.5% = shells and waste)
The grind spread reflects cocoa processor profitability and affects the demand side of the cocoa curve.

Seasonal pattern:

Crop Season	Timing	Region	Impact
Main crop	Oct–Mar	Ivory Coast / Ghana	70–75% of annual output
Mid-crop	Apr–Sep	Ivory Coast / Ghana	25–30% of annual output
Arrival data	Weekly (Ivory Coast port)	Real-time supply signal	Moves spot price
3.9.4 Cotton
Exchange	Contract Months	Unit
ICE Cotton #2	Mar, May, Jul, Oct, Dec	¢/lb
Cotton(t, T) = ICE_Settlement(T)
             + Location_Basis(T)           [US delivery point adjustments]
             + Polyester_Differential(T)   [competitive fibre: synthetic substitution]
             + China_Import_Demand_Factor(T)
China is the world's largest cotton consumer (~30% of world use). Cotton prices are highly sensitive to Chinese import policy and stockpile decisions.

3.10 Freight & Shipping
3.10.1 Market Structure
Freight rates represent the cost of transporting commodities by sea. Unlike physical commodities, freight is a service and cannot be stored. This makes freight curves strongly mean-reverting.

Key indices:

Baltic Dry Index (BDI): Composite of Capesize, Panamax, Supramax rates
Capesize (C5TC): Large vessels >100,000 DWT; carry iron ore, coal
Panamax (P5TC): Medium vessels 65,000–80,000 DWT; carry grain, coal
Supramax (S10TC): Smaller vessels 50,000–65,000 DWT; versatile bulk carriers
VLCC (TD3C): Very Large Crude Carriers; crude oil tanker rates
3.10.2 Forward Freight Agreement (FFA) Construction
Freight forward curves are constructed from FFA (Forward Freight Agreement) prices — OTC derivatives that pay the difference between agreed rate and the Baltic Exchange assessment:

FFA_Capesize(t, T) = Baltic_Capesize_FFA_Quote(T)    [liquid: M1–M6]
FFA_Capesize(t, T) = Mean_Reversion_Model(T)          [illiquid: >6M]
Mean reversion model for freight:

Freight rates exhibit strong mean reversion to long-run equilibrium (driven by vessel supply/demand balance):

dFFA(t) = κ × (θ - FFA(t)) × dt + σ × dW(t)

Forward curve shape:
F(t, T) = θ + (S(t) - θ) × exp(-κ × (T - t))

Where:
  θ = long-run equilibrium freight rate
  κ = mean reversion speed
  S(t) = current spot freight rate
For Capesize:

Long-run equilibrium (θ) ≈ 
18,000/day
Mean reversion speed (κ) ≈ 1.5–2.5 (fast reversion; ~6–9 month half-life)
Route-specific construction:

Capesize(t, T)  = C5TC_FFA(T)   [5 time-charter average: Brazil-China, Australia-China, etc.]
Panamax(t, T)   = P5TC_FFA(T)   [5 time-charter average: USG-Japan, Black Sea-Med, etc.]

Tanker (VLCC):
TD3C(t, T) = Baltic_VLCC_FFA(T) + Bunker_Adjustment_Factor(T)

Bunker_Adjustment_Factor(T) = (Bunker_Consumption × (VLSFO_Price(T) - Reference_Bunker))
3.10.3 Seasonal Patterns in Freight
Segment	Seasonal Pattern
Capesize	Q4 typically strongest (iron ore demand before Chinese New Year restocking)
Panamax	Q4 and Q1 strongest (South American grain season, Jan–Apr)
Tankers (VLCC)	Winter stronger (Northern Hemisphere heating oil demand)
Gas carriers (LNG)	Winter strongest (European/Asian heating gas)
4. Interpolation & Extrapolation Methodologies
4.1 Why Interpolation Matters
Forward curves must produce prices at any date requested — not just at exchange settlement dates. The choice of interpolation method affects:

Risk profile: Different interpolation methods create different delta profiles between pillar points
P&L smoothness: Poor interpolation creates artificial daily P&L from calendar effects
Arbitrage: Bad interpolation can create calendar spread arbitrage
Greeks: Delta and gamma change depending on interpolation
4.2 Linear Interpolation (Most Common for Commodities)
Between two pillar points T₁ and T₂:

F(t, τ) = F(t, T₁) + [(F(t, T₂) - F(t, T₁)) / (T₂ - T₁)] × (τ - T₁)

Or equivalently (using days):
F(t, τ) = F(t, T₁) + [(F(t, T₂) - F(t, T₁)) × (τ - T₁)/(T₂ - T₁)]
Pros: Simple; transparent; no spurious kinks; arbitrage-free if pillar points are arbitrage-free
Cons: Creates kinks at pillar points; forward delta is discontinuous at pillars

Appropriate for: Carbon markets, precious metals, short-dated energy

4.3 Log-Linear Interpolation
Used when forward prices are better modelled as a ratio than a difference:

ln[F(t, τ)] = ln[F(t, T₁)] + [(ln[F(t, T₂)] - ln[F(t, T₁)]) × (τ - T₁)/(T₂ - T₁)]

Equivalently:
F(t, τ) = F(t, T₁) × [F(t, T₂)/F(t, T₁)]^((τ-T₁)/(T₂-T₁))
Appropriate for: Products where percentage moves are more natural than absolute moves (e.g., long-dated energy)

4.4 Calendar Spread Interpolation (Energy Standard)
For energy products (crude oil, natural gas), interpolation is performed on calendar spreads rather than outright prices:

Step 1: CS(Mᵢ, Mᵢ₊₁) = F(t, Mᵢ₊₁) - F(t, Mᵢ)    for all adjacent liquid months
Step 2: For broken date τ between Mᵢ and Mᵢ₊₁:
        CS_τ = CS(Mᵢ, Mᵢ₊₁) × (τ - Mᵢ)/(Mᵢ₊₁ - Mᵢ)
Step 3: F(t, τ) = F(t, Mᵢ) + CS_τ
Appropriate for: Crude oil, natural gas, refined products — any market where calendar spreads are the primary traded instrument

4.5 Cubic Spline Interpolation
A smooth curve is fitted through pillar points using cubic polynomials:

Between each pair (Tᵢ, Tᵢ₊₁), a cubic polynomial is fitted:
F(t, τ) = aᵢ + bᵢ(τ - Tᵢ) + cᵢ(τ - Tᵢ)² + dᵢ(τ - Tᵢ)³

Subject to:
  - Passes through all pillar points (interpolating spline)
  - First and second derivatives are continuous at pillar points
  - Additional end conditions (natural, not-a-knot, or clamped)
Pros: Very smooth; continuous first and second derivatives; more natural forward risk profile
Cons: Can oscillate between pillar points (Runge's phenomenon); more complex to implement; may produce negative forward rates
Appropriate for: Long-dated metal curves; agricultural curves with seasonal shape

4.6 Flat Extrapolation
Beyond the last liquid pillar point Tₙ:

F(t, τ) = F(t, Tₙ)    for all τ > Tₙ
Appropriate for: Conservative default when no market information exists beyond Tₙ
Risk: Ignores term structure; may miss long-run price mean reversion

4.7 Mean-Reversion Extrapolation
For commodities with clear long-run equilibrium (freight, agricultural):

F(t, τ) = θ + (F(t, Tₙ) - θ) × exp(-κ × (τ - Tₙ))

Where:
  θ = long-run equilibrium price (estimated from historical analysis)
  κ = mean reversion speed
Appropriate for: Freight, agricultural products, potentially carbon when market prices are very far from fundamental value

5. Model Assumptions by Asset Class
5.1 Universal Commodity Assumptions
#	Assumption	Justification	Limitation
A1	No-arbitrage condition holds at all pillar points	Prevents risk-free profits; foundational to pricing theory	Breaks down in stressed or illiquid markets; exchange/OTC price divergence
A2	Observable market prices at pillar points are reliable	Exchange settlement prices are definitive; multi-party auction	Settlement manipulation possible; illiquid settlement sessions distort prices
A3	Interest rates are deterministic for cost-of-carry calculations	Adequate for short-to-medium dated curves (< 3Y)	Stochastic interest rates matter for long-dated commodity forwards
A4	Interpolation between pillar points is monotone and smooth	Prevents arbitrage between consecutive tenors	Real markets exhibit discontinuities at crop boundaries, season changes
A5	Storage is available at modelled cost	Storage markets are competitive; costs are transparent	Storage availability can be physically constrained (Cushing full, LME queues)
5.2 Energy-Specific Assumptions
#	Assumption	Implication if Wrong
E1	WTI is determined relative to Brent via a stable spread	If Cushing infrastructure changes or US export capacity grows, spread can structurally shift
E2	Calendar spreads between monthly contracts reflect storage economics	Supply disruptions can create non-economic spreads (force majeure, sanctions)
E3	Seasonal shape in natural gas is stable year-on-year	LNG import flexibility, demand response, and weather volatility make seasonal patterns unstable
E4	Location basis is additive and stable	Pipeline bottlenecks, permitting changes, or infrastructure damage create sudden basis dislocations
E5	Crack spreads are mean-reverting to historical ranges	Structural demand changes (EV transition, biofuels mandates) can permanently shift crack levels
5.3 Carbon Market Assumptions
#	Assumption	Implication if Wrong
C1	No seasonality in the forward curve	Annual compliance cycle (April surrender) creates temporary seasonal effects near year-end
C2	Cost of carry is purely interest-rate-driven	Regulatory uncertainty creates a risk premium that is not captured by the pure carry model
C3	Regulatory framework (cap, trajectory, allocation) is stable	Policy changes (REPowerEU, Fit for 55 reforms) can cause multi-standard-deviation moves overnight
C4	No convenience yield or storage cost for allowances	Physical carbon certificates (paper-based credits) do have administrative costs; electronic allowances do not
C5	Overnight rate is the correct discount rate	Market participants may use term rates (ESTR vs. EURIBOR) depending on their funding structure
5.4 Base Metal Assumptions
#	Assumption	Implication if Wrong
M1	LME settlement prices are definitive global benchmarks	SHFE (Shanghai) increasingly rivals LME for Chinese metals; price discovery shifting
M2	Storage costs are proportional to spot price	Warehouse rule changes (post-2014 LME rules) affect effective storage cost
M3	Regional premiums are additive to LME base price	Premium can become negatively correlated with LME price in extreme scenarios
M4	LME standard dates capture the full term structure	OTC bi-lateral deals beyond 27M are growing; curve needs extension methodology
M5	SHFE/LME arbitrage keeps prices aligned	Capital controls, import/export restrictions, SHFE delivery standards create persistent arbitrage
5.5 Precious Metal Assumptions
#	Assumption	Implication if Wrong
PM1	Gold lease rates are slow-moving (1–14 days half-life)	During banking stress or gold squeeze, lease rates can spike from 0.5% to 5%+ overnight
PM2	Central bank gold lending programs are stable	Coordinated central bank selling (like 1999 Washington Agreement) can flood the lease market
PM3	USD interest rate is the dominant forward curve driver	When gold is in high demand as a safe haven, lease rates may spike and override the interest rate effect
5.6 Agricultural Assumptions
#	Assumption	Implication if Wrong
AG1	Crop calendar dates are stable year-on-year	Climate change is shifting planting and harvest dates; El Niño/La Niña cycles disrupt patterns
AG2	USDA supply/demand projections are incorporated into futures prices efficiently	Government reports create instant price jumps; between reports, prices may be mispriced
AG3	Storage costs are linear over time	Elevator basis (local cash vs. nearby futures) reflects local supply/demand and transportation costs; can deviate significantly
AG4	Crop yield technology (GMOs, precision agriculture) is factored in	Long-run trend yield increases make historical yield-based models overly conservative
5.7 Soft Commodity Assumptions
#	Assumption	Implication if Wrong
SC1	Brazilian Real exchange rate is an additive adjustment to coffee and sugar	BRL can be highly volatile; nonlinear effects in crisis periods
SC2	West African cocoa supply is stable and predictable	Political instability in Ivory Coast or Ghana can cause severe supply disruptions
SC3	Chinese cotton demand is stable and price-elastic	Government stockpile programs (China bought 60% of world cotton in 2011–2012) distort the market
SC4	Ethanol parity is a reliable floor for sugar prices	Oil price changes directly affect the ethanol parity, which may not be reflected in sugar futures immediately
6. Model Governance Framework
6.1 Governance Principles
A robust governance framework for commodity forward curves must be built on five principles:

Independence: Model validation must be independent from model development and from the front office
Transparency: All methodology choices, parameter values, and override decisions must be documented with rationale
Proportionality: Governance intensity proportional to model materiality and complexity
Accountability: Named owners for every model at every stage of its lifecycle
Continuous Review: Models must be monitored and reviewed on an ongoing basis, not just at initial approval
6.2 Commodity Forward Curve Model Lifecycle
┌──────────────────────────────────────────────────────────────────────────────┐
│                  COMMODITY FORWARD CURVE MODEL LIFECYCLE                     │
│                                                                              │
│  1. PROPOSAL     → Business case for new/changed methodology                │
│  2. DEVELOPMENT  → Quant design, mathematical derivation                    │
│  3. DOCUMENTATION→ TDD (Technical Design Document) production               │
│  4. PEER REVIEW  → Internal quant review                                    │
│  5. VALIDATION   → Independent Model Validation (IMV/MRM)                   │
│  6. TVR          → Technical Validation Report issued                       │
│  7. APPROVAL     → Model Risk Committee (MRC) decision                      │
│  8. DEPLOYMENT   → IT implementation, UAT, training                        │
│  9. PRODUCTION   → Live use with daily monitoring                           │
│  10. MONITORING  → Ongoing performance tracking                             │
│  11. REVALIDATION→ Annual or trigger-based full review                      │
│                                                                              │
│  At any stage: ESCALATION → Model Risk Committee for exception decisions    │
└──────────────────────────────────────────────────────────────────────────────┘
6.3 Roles and Responsibilities
Role	Primary Responsibility	Key Deliverables
Curve Methodology Owner (this role)	Own end-to-end methodology; propose changes; ensure documentation is current	Methodology documents; parameter calibration; change proposals
Front Office / Trading Desk	Provide expert judgment; mark illiquid tenors; report anomalies	Manual marks; override requests with justification
Independent Model Validation (MRM)	Validate conceptual soundness; back-test; compare to benchmarks	Technical Validation Report (TVR); conditions and restrictions
Model Risk Committee (MRC)	Approve or reject model changes; set use conditions and restrictions	Approval minutes; conditions; escalation decisions
Quant IT / Technology	Implement approved models in production	Production code; system documentation; UAT sign-off
Finance / Product Control	IPV (Independent Price Verification); P&L use	Monthly IPV report; P&L sign-off
Risk Management	Consume curves for limits and VaR; challenge anomalies	Daily limit reports; VaR calculations
Internal Audit	Review adherence to governance framework	Audit findings; remediation tracking
6.4 Model Documentation Standards
Every commodity forward curve methodology document must include:

Section 1: Executive Summary

High-level description of methodology
Products and use cases covered
Key methodological choices and their rationale
Section 2: Mathematical Formulation

Full mathematical derivation
All formulas with precise variable definitions
Worked numerical examples
Section 3: Input Data Specification

All data inputs listed
Source for each input (primary and fallback)
Acceptable data quality standards (e.g., maximum data age)
Fallback procedures when primary source is unavailable
Section 4: Parameter Choices and Calibration

All parameters with current values
Justification for each parameter choice
How parameters are recalibrated and how frequently
Sensitivity of output to ±10% parameter changes
Section 5: Known Limitations and Conditions

Explicit list of conditions under which the model may produce unreliable output
Market conditions that would trigger a methodology review
Restrictions on use (e.g., "not to be used for maturities > 5 years")
Section 6: Alternatives Considered

Other methodologies evaluated
Why the chosen methodology was preferred
Section 7: Back-test Evidence

Historical performance of model vs. realised prices
RMSE, bias, hit rate statistics
Periods of poor performance and explanation
Section 8: Validation History

Date of initial validation and subsequent revalidations
Summary of TVR findings
Outstanding conditions and remediation status
Section 9: Change Log

Version history
All changes with dates, authors, and rationale
Impact assessment for each change
6.5 Curve Approval and Update Cycle
┌─────────────────────────────────────────────────────────────────┐
│           COMMODITY FORWARD CURVE UPDATE & APPROVAL CYCLE       │
│                                                                 │
│  DAILY:     EOD curve production run                            │
│             Automated quality checks (spike, arbitrage, gaps)   │
│             Any alerts reviewed by curve team by 5pm local      │
│                                                                 │
│  WEEKLY:    Illiquid tenor mark review by Methodology Owner     │
│             Benchmark deviation report produced                 │
│             Cross-product consistency check                     │
│                                                                 │
│  MONTHLY:   Back-test performance report                        │
│             IPV reconciliation with Finance                     │
│             Governance exception report to MRC                  │
│                                                                 │
│  QUARTERLY: Parameter recalibration review                      │
│             Seasonal factor update (where applicable)           │
│             MRC presentation on curve quality                   │
│                                                                 │
│  ANNUALLY:  Full methodology revalidation by MRM               │
│             Documentation refresh                               │
│             Regulatory alignment review                         │
│                                                                 │
│  AD HOC:    Major market structural change                      │
│             Regulatory change                                   │
│             New product onboarding                              │
│             Significant P&L unexplained variance                │
└─────────────────────────────────────────────────────────────────┘
6.6 Override Policy
Manual overrides to automated curves are a significant governance area. When the curve team or front office manually overrides an automated price:

Requirements:

Written justification provided at time of override
Override categorised by type (data quality, market dislocation, expert judgment)
Override reviewed and signed off by Methodology Owner (or delegate)
Override logged in audit trail with timestamp, user, and justification
Override reviewed in monthly governance report
Persistent overrides (>5 business days) escalated to MRC
Override categories:

Category	Definition	Example
Data quality	Primary source data is incorrect or missing	Exchange system outage; Bloomberg feed error
Market dislocation	Market price exists but is unrepresentative	Flash crash; illiquid settlement with 1 trade
Expert judgment	Model output disagrees with trader market view	Structural market change not yet in futures prices
Model limitation	Model methodology produces unreliable output for specific tenor	Extrapolation beyond last liquid point
7. Model Validation
7.1 Validation Objectives
Independent model validation (IMV) of commodity forward curves must assess:

Conceptual soundness – Is the theoretical framework appropriate for the commodity market?
Mathematical correctness – Are all formulas correctly derived and implemented?
Data quality – Are inputs reliable, timely, sourced appropriately?
Implementation accuracy – Does the production code match the documented methodology?
Performance – Does the model produce accurate, stable, unbiased prices?
Limitation transparency – Are all known limitations clearly documented?
Governance compliance – Is the model being used within approved conditions?
7.2 No-Arbitrage Testing
The most fundamental validation check: the forward curve must not contain calendar spread arbitrage — i.e., it must not be possible to lock in a risk-free profit by buying a nearby contract and selling a deferred contract (or vice versa), accounting for storage and financing costs.

Static no-arbitrage condition:

For any t₁ < t₂:
F(t, t₂) ≤ F(t, t₁) × exp((r + s) × (t₂ - t₁))    [upper bound: cost of carry]
F(t, t₂) ≥ F(t, t₁) × exp((r - c_max) × (t₂ - t₁)) [lower bound: max convenience yield]
In simplified form for short tenors:

|F(t, t₂) - F(t, t₁) × exp(r × (t₂ - t₁))| ≤ s × F(t, t₁) × (t₂ - t₁)
Validation test:

For every adjacent tenor pair (Tᵢ, Tᵢ₊₁) in the curve:
  Check: Cal_Spread(Tᵢ, Tᵢ₊₁) ≥ -(r + c_max) × F(Tᵢ) × (Tᵢ₊₁ - Tᵢ)/365
  Check: Cal_Spread(Tᵢ, Tᵢ₊₁) ≤ (r + s) × F(Tᵢ) × (Tᵢ₊₁ - Tᵢ)/365
7.3 Back-Testing
Back-testing assesses how well historical forward prices predicted future realised spot prices.

Methodology:

For each historical date t and each forward tenor T:

Back_Test_Error(t, T) = F(t, T) - S(T)    [error of the forward price vs. realised spot]
Performance metrics:

Mean Error (Bias)  = (1/N) × Σ [F(t, T) - S(T)]
                    → Should be near zero; significant bias indicates systematic model error

RMSE               = sqrt[(1/N) × Σ (F(t, T) - S(T))²]
                    → Measures overall forecast accuracy

MAE                = (1/N) × Σ |F(t, T) - S(T)|
                    → Robust to outliers

Hit Rate           = Count[|F(t,T) - S(T)| ≤ ε] / N
                    → % of forecasts within ±ε of realised price (e.g., ±5%)

Directional Accuracy = Count[sign(F(t,T) - S(t)) = sign(S(T) - S(t))] / N
                    → % of times the forward correctly predicted price direction
Interpretation guide:

Finding	Interpretation	Action
Large positive bias	Model consistently overestimates future prices	Investigate risk premium; may need to add risk premium adjustment
Large negative bias	Model consistently underestimates future prices	Review convenience yield assumption; may be too high
High RMSE for short tenors	Model is poor at predicting nearby prices	Data quality or lag issue
High RMSE for long tenors	Long-run mean reversion/extrapolation is wrong	Review long-end methodology
Low directional accuracy	Model is pricing in wrong direction	Fundamental methodology flaw; urgent review
7.4 Benchmark Comparison
Compare internal curve to independent external benchmarks:

Deviation(T) = |Internal_Curve(T) - Benchmark(T)|

Report:
  Mean Deviation  = average deviation across all tenors
  Max Deviation   = worst tenor deviation
  % Tenors within tolerance band
Benchmark sources by commodity:

Asset Class	Benchmark Source
Crude Oil (Brent, WTI)	Platts, Argus, ICE settlement
Natural Gas	Platts, ICIS
Carbon (EU ETS)	ICE, Bloomberg, Refinitiv
Base Metals	LME official prices, Metal Bulletin
Precious Metals	LBMA Fix, COMEX settlement
Agricultural	USDA, Bloomberg, Refinitiv
Soft Commodities	ICE settlement, USDA
Freight	Baltic Exchange assessments
Tolerance bands (illustrative):

Asset Class	Acceptable Deviation
Crude Oil (liquid tenors)	≤ $0.10/bbl
Natural Gas (liquid tenors)	≤ $0.05/MMBtu
EU ETS (liquid tenors)	≤ €0.20/tonne
LME Copper	≤ $5/tonne
Gold	≤ $1/oz
Agricultural Grains	≤ 0.5 ¢/bushel
7.5 Sensitivity Analysis
Assess partial derivatives of the forward curve with respect to key inputs:

For EU ETS:

∂F_EUA/∂S    = (1 + ESTR × (T-t)/365)    ≈ 1.03 for 1Y tenor (at 3% ESTR)
∂F_EUA/∂ESTR = S × (T-t)/365             = €68.50 × 1.0 = €68.50 per 100% rate move
                                           = €0.685 per 1% rate move  [small]
For Gold:

∂F_Gold/∂S        = (1 + GFR × (T-t)/365)           ≈ 1.048 for 1Y at 4.8% GFR
∂F_Gold/∂r_USD    = S_Gold × (T-t)/365               ≈ $2,350/oz per 100% rate move
∂F_Gold/∂r_Lease  = -S_Gold × (T-t)/365              ≈ -$2,350/oz per 100% lease rate move
                    (symmetric: rate and lease rate have equal and opposite effects)
For Copper (cost of carry):

∂F_Cu/∂S      = exp[(r+s-c)(T-t)]                   ≈ 1.02 for 1Y
∂F_Cu/∂s      = S × (T-t) × exp[(r+s-c)(T-t)]       ≈ $9,200 × 1.0 × 1.02 ≈ $9,384 per unit
∂F_Cu/∂c      = -S × (T-t) × exp[(r+s-c)(T-t)]      (negative: higher c → lower F)
7.6 Stress Testing Scenarios
Scenario	Description	Expected Impact
Spot price shock +20%	Instantaneous 20% rise in spot	Curve shifts up proportionally; test for any non-linear effects
Curve inversion	Forced backwardation (all calendar spreads negative)	Test that system handles backwardated curves correctly
Interest rate shock +300bps	Parallel shift in risk-free rate	Material for precious metals (gold carry), carbon markets
Primary data source outage	Bloomberg/ICE feeds unavailable for 1 business day	Test fallback to secondary sources; test staleness flagging
Extended market closure	Exchange closed for 5 consecutive business days	Test last-known-good with age flag; test extrapolation behaviour
Extreme calendar spread	Contango/backwardation at historical extreme	Test that curve remains arbitrage-free at extremes
7.7 Ongoing Monitoring Metrics
Metric	Calculation	Frequency	Alert Level
Daily curve change		F_today(T) - F_yesterday(T)	for each tenor
Calendar arbitrage violations	Count of violations of no-arbitrage condition	Daily	Any violation = immediate alert
Source deviation		Internal(T) - External_Benchmark(T)	
Data freshness	Age of most recent input data at EOD	Daily	4 hours for liquid; > 24h for illiquid
Override count	Number of manual overrides active	Daily	5 active overrides = review
Back-test RMSE trend	Rolling 12M back-test RMSE vs. prior period	Monthly	20% deterioration
Benchmark deviation trend	Average deviation over 30 days vs. prior 30 days	Weekly	50% increase
8. Challenges & Risk Factors
8.1 Data Quality and Availability Challenges
Challenge	Root Cause	Business Impact	Mitigation
Illiquid far-dated tenors	No active market beyond 1–3Y for most commodities	Model-derived prices carry significant uncertainty; Level 3 fair value	Expert judgment marks with governance sign-off; disclose uncertainty quantification
Source conflicts	Bloomberg, Platts, ICE, broker quotes can all differ for same contract	Curve level depends on source hierarchy choice	Define and document source hierarchy; monitor inter-source deviations
Stale data	Market holidays, system outages, illiquid sessions	Old data used to price live risk	Automated data freshness monitoring; staleness flags on all tenors
Settlement price errors	Fat-finger input errors at exchanges; illiquid final auction	Curve contains embedded error	Automated spike detection; crosscheck with live prices; exchange correction process
Delayed market data	Vendor normalisation and distribution delays	Curves not fully updated by trade start of business	Define mandatory data cutoffs; escalation process for major data delays
OTC price opacity	Bilateral OTC trades not reported in real-time	Illiquid broker quotes may be indicative, not firm	Require multiple broker quotes; use median of quotes
8.2 Structural Market Challenges
Challenge	Description	Impact on Curves	Mitigation
Contango-to-backwardation regime shifts	Supply disruption or demand surge can flip curve structure overnight	Model calibrated in contango regime may misprice in backwardation	Regime-aware methodology; test model in both regimes
Seasonal pattern instability	Climate change, LNG imports, demand response alter seasonal shapes	Historical seasonal factors become misleading	Annual seasonal factor recalibration; real-time weather monitoring
New market development	New trading hubs emerge (e.g., TTF replacing NBP as European gas benchmark)	Existing methodology may not apply to new hub	Rapid onboarding process; methodology template for new hubs
Regulatory market design changes	ETS cap changes, MIFID II reporting, FRTB capital rules	Methodology changes required at short notice	Regulatory horizon scanning; pre-built methodology frameworks
Physical infrastructure disruptions	Pipeline outages, LNG terminal fires, mine closures	Spot/forward price relationships break down	Robust fallback data sources; model override capability
Geopolitical events	Sanctions (Russian oil/gas), export bans (Indonesian palm oil, Indian sugar)	Market structure fundamentally disrupted	Scenario libraries; rapid methodology review process
8.3 Modelling Challenges
Challenge	Description	Mitigation
Interpolation method choice	Different methods produce different delta risk profiles and intraday P&L	Standardise by asset class; document rationale; validate against market practice
Long-end extrapolation uncertainty	No market evidence for prices beyond 3–5 years	Use mean-reversion models; disclose model uncertainty; restrict long-dated use cases
Convenience yield estimation	Convenience yield is unobservable; must be implied from prices	Back-calibrate from futures strip; cross-validate with inventory data
Seasonal factor calibration	Seasonal factors derived from historical data may be stale	Annual recalibration; track changes in seasonal patterns systematically
Cross-product consistency	Crude, refined products, and natural gas curves must be internally consistent	Daily cross-product consistency checks; crack spread and basis monitoring
Curve granularity vs. stability	Daily curve tenors create noise; monthly tenors lose precision	Risk-based choice of granularity; daily for front (M1-M6), monthly beyond
Holiday calendar edge cases	Commodity markets have complex multi-jurisdiction holiday calendars	Standardised holiday calendar library; automated testing of edge cases
8.4 Governance and Operational Challenges
Challenge	Description	Mitigation
Decentralised curve marking	Front office marks illiquid tenors; conflict of interest	Independent oversight; limit front office marking to defined tenors; document all marks
Model creep / undocumented changes	Small changes accumulate over time without formal approval	Version control for all methodology documents; mandatory change management process
Key person dependency	Methodology knowledge concentrated in one or two individuals	Full methodology documentation; cross-training program; succession planning
Legacy system constraints	Older systems limit interpolation method choices or real-time capability	System upgrade roadmap; interim compensating controls
Multiple use case conflicts	Same curve used for trading P&L, risk limits, regulatory capital, and accounting	Define the primary use case; document differences in use; coordinate with downstream users
Speed of market vs. governance	Market structure changes faster than governance cycle allows	Streamlined fast-track approval for minor changes; escalation path for urgent changes
8.5 Risk Factors Specific to Commodity Curves
Risk Factor	Description	Severity
P&L misstatement	Incorrect curve level produces incorrect P&L; affects trader bonuses, reported results	Very High
Collateral disputes	Counterparty uses different curve; generates margin call disputes	High
Risk limit breaches	Stale or incorrect curve understates exposures; breaches go undetected	High
Regulatory capital error	Incorrect VaR from bad curves leads to capital under/over-statement	High
FRTB NMRF penalty	Inadequate price observations makes risk factor non-modellable; punitive capital charge	Medium-High
Audit finding	Level 3 fair value methodology not adequately documented or validated	Medium
Model demotion	Persistent performance failure triggers MRM to restrict model use	Medium
9. Stakeholder Map & Responsibilities
9.1 Internal Stakeholders
Stakeholder	Role	Frequency of Interaction	Key Needs from Curve Team
Commodity Trading Desks	Primary users of curves for pricing and hedging	Daily	Accurate, timely EOD curves; ability to provide expert judgment marks for illiquid tenors
Commodity Risk	VaR, limit monitoring, exposure reporting	Daily	Complete, arbitrage-free curves at all required tenors; history for VaR calibration
Independent Valuations Group (IVG)	Validates independence of data sources used	Monthly / quarterly	Evidence that sources are independent and not trader-influenced
Model Risk Management (MRM)	Independent model validation	At approval; annual revalidation; trigger-based	Comprehensive methodology documentation; back-test results; access to production system
Finance / Product Control	IPV; official P&L production	Monthly (IPV); Daily (P&L use)	Independent price benchmark for each curve tenor; understanding of Level 1/2/3 classification
Quant IT / Technology	Production implementation and maintenance	When methodology changes; ongoing support	Clear mathematical specification; test cases; requirements for system changes
Compliance / Legal	Regulatory adherence	When regulations change	Impact assessment of regulatory changes on methodology
Internal Audit	Framework adherence review	Annually	Evidence of governance process; documentation; sign-offs; exception reports
Senior Management	Strategic oversight; resource decisions	Quarterly governance reports	Curve quality summary; key risks; outstanding issues
9.2 External Stakeholders
Stakeholder	Role	Interaction Type
ICE (Intercontinental Exchange)	Settlement prices for Brent, EU ETS, UK ETS, Cocoa, Coffee, Sugar, Cotton	Daily data feed; pricing queries
CME Group / NYMEX	Settlement prices for WTI, Natural Gas, Grains, Livestock, Metals	Daily data feed
LME (London Metal Exchange)	Definitive settlement prices for all base metals	Daily data feed; LME RIC feeds
LBMA (London Bullion Market Association)	Gold and silver benchmark prices (AM/PM Fix)	Daily data feed
Baltic Exchange	Freight rate assessments (BDI, route rates)	Daily data feed
Bloomberg / Refinitiv (LSEG)	Aggregated market data, live prices, broker consensus	Real-time and EOD data feeds
Platts / Argus / ICIS	Commodity price reporting; OTC market assessments	Daily; used as benchmark
Brokers (OTC)	Quote provision for illiquid tenors	As needed for illiquid marks
Regulators (PRA, FCA, CFTC)	Model risk and fair value regulatory standards	During examinations; new rule implementation
External Auditors	Fair value methodology review	Annually; interim if required
10. Key Controls & Quality Metrics
10.1 Daily Production Controls
Control	Definition	Failure Threshold	Action on Failure
Curve completeness	All required tenors have a valid price	Any missing tenor	Immediate escalation; use prior day's price with staleness flag
Data freshness at EOD	All input data is dated within acceptable window	Liquid: >4 hours; Illiquid: >24 hours	Flag as stale; use fallback source or prior day
Calendar arbitrage check	No tenor-to-tenor calendar spread arbitrage	Any single violation	Alert to Methodology Owner within 1 hour; investigate and correct
Spike detection	Daily change > 3σ of historical daily changes	3σ = alert; >5σ = hard block	Auto-alert; human review required before curve published
Source reconciliation	Internal curve vs. external benchmark within tolerance	Defined tolerance band	Alert; review and document explanation
Negative price check	No commodity forward price ≤ 0	Any single violation	Immediate investigation (note: crude oil was negative in April 2020)
Cross-product consistency	Crack spreads, basis, and cross-market spreads within reasonable ranges	2× historical 30-day range	Alert; review with trading desk
10.2 Weekly Controls
Control	Frequency	Owner	Output
Illiquid tenor review	Weekly	Methodology Owner	Confirmed or revised marks for tenors >18 months
Benchmark deviation report	Weekly	Methodology Team	Report of all tenors outside tolerance vs. all benchmarks
Override log review	Weekly	Methodology Owner	Review of all active overrides; confirm continued validity
Data source health check	Weekly	Quant IT / Data Team	Confirm all primary and secondary sources are functioning
10.3 Monthly Controls
Control	Frequency	Owner	Output
Back-test performance report	Monthly	Methodology Owner	RMSE, bias, hit rate for all asset classes; trend analysis
IPV reconciliation	Monthly	Finance / Product Control	Confirmed or challenged Level 1/2/3 values; IPV adjustments
Governance exception report	Monthly	Methodology Owner	All exceptions to normal process; overrides; escalations
MRC reporting	Monthly	Methodology Owner + MRM	Curve quality dashboard; outstanding model conditions
10.4 Quality Metrics Dashboard
The following metrics should be tracked in the daily/weekly/monthly governance dashboard:

Curve Quality Metrics:

1. Completeness Rate:        (Tenors with valid prices / Total required tenors) × 100%
2. Staleness Rate:           (Tenors with stale data / Total tenors) × 100%
3. Arbitrage Violation Rate: Count of calendar spread violations (target: 0)
4. Override Rate:            (Overridden tenors / Total tenors) × 100%
5. Source Deviation Count:   Number of tenors outside tolerance vs. benchmark
Model Performance Metrics:

6. Rolling 12M Back-test RMSE:   by asset class and tenor bucket
7. Rolling 12M Back-test Bias:   by asset class (positive/negative)
8. Benchmark Deviation Mean:     average deviation across all tenors
9. Benchmark Deviation Max:      worst single tenor deviation
10. Directional Accuracy:        % of times forward price predicted direction correctly
Governance Metrics:

11. Open Model Conditions:       Count of outstanding MRC conditions
12. Overdue Revalidations:       Count of models past annual review date
13. Override Duration:           Average age of active overrides
14. Documentation Currency:      % of methodology docs reviewed within 12 months
11. Regulatory Considerations
11.1 IFRS 13 Fair Value Hierarchy – Commodity Application
IFRS 13 requires fair value measurements to be classified into a three-level hierarchy based on the observability of inputs:

Level	Description	Commodity Forward Curve Application
Level 1	Quoted prices in active markets for identical assets; no adjustment	Front-month exchange futures prices (ICE Brent M1, CME WTI M1, LME 3M Copper)
Level 2	Observable inputs other than Level 1; may require adjustment	Interpolated prices between liquid futures; broker-quoted OTC prices for deferred months; basis-adjusted prices
Level 3	Significant unobservable inputs; model-based	Long-dated tenors (>3–5Y) with no market quotes; illiquid market prices (CORSIA, ACCU long-dated); convenience yield assumptions for long-dated agricultural
Practical implications:

The proportion of fair value attributed to Level 3 inputs is disclosed in financial statements
Level 3 fair values require additional validation and documentation
Regulators and auditors scrutinise Level 3 more closely than Level 1/2
High Level 3 proportion may attract provisioning (Day 1 P&L reserves)
Day 1 P&L (Inception P&L) restriction:

When a commodity derivative is priced using Level 3 inputs, any profit at inception must be deferred and recognised only as the inputs become observable:

Day 1 P&L Reserve = Trade Value(Model) - Trade Value(Observable_Inputs_Only)
This creates a strong incentive to maximise observable tenor range and minimise model-based extrapolation.

11.2 FRTB – Risk Factor Eligibility Test (RFET)
Under the Fundamental Review of the Trading Book (FRTB), a risk factor (e.g., the 2-year tenor of the copper forward curve) is modellable only if it has sufficient real price observations.

Modellability requirement:

A risk factor is modellable if:
  1. ≥ 24 verifiable real price observations in the past 12 months
     (approximately one observation every 2 weeks)
  AND
  2. Observations span at least 12 months of history
  AND
  3. Observations are from real arm's-length transactions or firm bids/offers
If a risk factor fails the RFET, it becomes a Non-Modellable Risk Factor (NMRF) with punitive capital treatment:

NMRF capital charge is calculated using a stress scenario
NMRF charges are not diversifiable with IMA charges
Typically results in 5–10× higher capital for that risk factor
Implication for commodity curve management:

The curve team must:

Track the RFET status of every tenor in every curve
Document and archive the price observations used for RFET
Alert the risk team when tenors are at risk of becoming NMRF
Work with trading desks to source price observations for borderline tenors
RFET tracking example:

Curve	Tenor	Observations (12M)	RFET Status
ICE Brent	M1–M12	Daily (250+)	✅ Modellable
ICE Brent	M13–M24	Weekly (~48)	✅ Modellable
ICE Brent	M25–M36	Monthly (~12)	⚠️ Borderline
ICE Brent	M36	Quarterly (4)	❌ NMRF
EU ETS	Dec-26	Daily (250+)	✅ Modellable
EU ETS	Dec-30	Monthly (~12)	⚠️ Borderline
ACCU	All tenors	Sporadic (<10)	❌ NMRF
11.3 Model Risk Management Standards
Standard	Issuer	Application to Commodity Curves
SR 11-7	US Federal Reserve (2011)	Gold standard for model risk globally; defines model, validation, use, governance requirements
SS1/23	PRA (UK Prudential Regulation Authority, 2023)	UK-specific MRM requirements; applies to UK-regulated entities
BCBS 239	Basel Committee	Data quality and aggregation; affects input data standards for curves
EMIR	European Regulation	Derivatives reporting; curves used for trade valuation in reported data
MiFID II	European Regulation	Best execution; price transparency; curves used in transaction cost analysis
12. Role Competency Framework
12.1 Technical Competencies
Competency Area	Specific Skills Required	Proficiency Level
Mathematical Finance	Cost of carry theory; no-arbitrage pricing; stochastic calculus; derivatives pricing	Expert
Commodity Markets Knowledge	In-depth knowledge of market structure, fundamentals, seasonality, and physical delivery for all commodity asset classes	Expert
Statistics & Econometrics	Time-series analysis; mean-reversion estimation; regression; volatility modelling; copulas	Advanced
Interpolation & Numerical Methods	Linear, log-linear, cubic spline, calendar spread interpolation; extrapolation	Advanced
Programming (Python)	Pandas, NumPy, SciPy for data analysis; matplotlib for visualisation; SQLAlchemy for database; CI/CD for model deployment	Advanced
Model Validation	Back-testing; benchmark comparison; sensitivity analysis; no-arbitrage testing; documentation review	Advanced
Market Data Systems	Bloomberg Terminal, Bloomberg API, Refinitiv Eikon, exchange data APIs	Intermediate–Advanced
Risk Systems	Understanding of how curves feed VaR, stressed VaR, FRTB SA/IMA calculations	Intermediate
12.2 Governance & Business Competencies
Competency	Detail
Methodology Ownership	Ability to own end-to-end methodology: design, document, defend, and evolve it over time
Independent Challenge	Willingness and ability to challenge front office marks, model choices, and governance decisions
Stakeholder Management	Ability to manage multiple demanding stakeholders (trading desks, MRM, Finance, technology) simultaneously
Communication & Presentation	Ability to explain complex quantitative topics to non-technical senior management in clear, simple terms
Documentation Quality	Ability to write comprehensive, precise, and clear methodology documents that satisfy regulatory standards
Decision-Making Under Uncertainty	Ability to make sound governance decisions when market data is incomplete or ambiguous
Regulatory Awareness	Maintain current knowledge of IFRS 13, FRTB, SR 11-7, SS1/23, and their commodity-specific implications
Project Management	Ability to manage multiple methodology review and onboarding projects simultaneously
12.3 Day-in-the-Life of a Commodity Forward Curve Methodology Lead
Daily (08:00–09:00):

Review overnight automated quality check results for all commodity curves
Investigate any spike alerts, arbitrage violations, or source deviations flagged
Review any manual overrides submitted by trading desks overnight
Check data freshness for all input sources
Confirm all curves are published and available to downstream systems by 09:00
Daily (09:00–12:00):

Liaise with trading desks on any illiquid tenor marks requiring expert judgment
Respond to ad hoc queries from risk, finance, or technology on curve behaviour
Monitor intraday market movements for any unusually large moves requiring investigation
Review new broker quotes for illiquid tenors; update where appropriate
Daily (14:00–17:00):

Monitor EOD settlement price ingestion for all exchanges
Confirm final EOD curves are produced and validated
Review any late market developments that may affect curve quality
Document any anomalies or exceptions in the daily log
Weekly:

Produce benchmark deviation report (internal curves vs. Platts, Bloomberg, Baltic)
Review all active overrides; confirm continued validity or remove
Attend cross-functional governance call (Risk, Finance, IT, Trading)
Review curve methodology for any new products or market structure changes
Monthly:

Produce back-test performance report across all asset classes
Prepare and present monthly governance report to Model Risk Committee
Review IPV reconciliation with Finance / Product Control
Update seasonal factors for any asset class where recalibration is triggered
Quarterly:

Conduct full parameter recalibration review (seasonal factors, mean reversion parameters, storage cost assumptions)
Present curve quality update to senior management
Identify any methodology improvements needed for the next quarter
Review any regulatory changes that may require methodology adjustments
Annually:

Coordinate full methodology revalidation with MRM team
Refresh all methodology documentation
Review model conditions and track remediation progress
Conduct training sessions for new model users (risk, finance, trading)
Present annual curve quality review to governance committee
13. Glossary of Commodity Forward Curve Terms
Term	Definition
ACCU	Australian Carbon Credit Unit – voluntary and compliance offset credit
Asian Swap	Commodity derivative where payoff is based on the average price over a period
Backwardation	Forward curve structure where F(t,T₁) > F(t,T₂) for T₁ < T₂; spot price above forward
Baltic Dry Index (BDI)	Composite index of bulk shipping freight rates
Basis	Difference between spot and futures price, or between two related futures prices
BBSW	Bank Bill Swap Rate – Australian short-term interest rate benchmark
Calendar Spread	Price difference between two futures contracts for same commodity, different delivery months
Capesize	Large bulk carrier vessels >100,000 DWT; primarily carries iron ore and coal
Carry	The cost (or benefit) of holding a commodity position over time
CBOT	Chicago Board of Trade – exchange for agricultural commodity futures
Contango	Forward curve structure where F(t,T₁) < F(t,T₂) for T₁ < T₂; forward above spot
Convenience Yield	Implicit benefit of holding physical inventory; reduces forward price below cost-of-carry
CORSIA	Carbon Offsetting and Reduction Scheme for International Aviation
Cost of Carry	Total cost of holding a commodity: financing + storage + insurance − convenience yield
Crack Spread	Processing margin: price of refined products minus cost of crude oil inputs
Crush Spread	Processing margin: value of soybean meal + oil minus cost of soybeans
Day 1 P&L	Profit at trade inception from Level 3 inputs; must be deferred under IFRS 13
EUA	EU Allowance – permits to emit 1 tonne CO₂ in the EU ETS
ESTR	Euro Short-Term Rate – ECB-published overnight reference rate for EUR
EU ETS	European Union Emissions Trading System – largest cap-and-trade carbon market
FFA	Forward Freight Agreement – OTC derivative on Baltic Exchange freight rates
FRTB	Fundamental Review of the Trading Book – Basel IV capital framework
Grind Spread	Cocoa processor margin: value of cocoa butter + powder minus bean input cost
Henry Hub	Primary US natural gas pricing hub; benchmark for CME natural gas futures
IFRS 13	International Financial Reporting Standard on Fair Value Measurement
IMV	Independent Model Validation – function that validates models without reporting to model owners
IPV	Independent Price Verification – Finance function's independent validation of fair values
JKM	Japan Korea Marker – LNG price benchmark for East Asian buyers
LBMA	London Bullion Market Association – sets gold and silver market standards
Level 1/2/3	IFRS 13 fair value hierarchy: L1 = quoted market; L2 = observable; L3 = model-based
LME	London Metal Exchange – primary exchange for base metals globally
Mean Reversion	Statistical tendency of commodity prices to revert to a long-run equilibrium
MRC	Model Risk Committee – governance body approving and monitoring model usage
MRM	Model Risk Management – function responsible for model validation and governance
NBP	National Balancing Point – UK natural gas pricing hub
NMRF	Non-Modellable Risk Factor – FRTB term for risk factors with insufficient price observations
Pillar Points	Market-observable price tenors used as anchors in curve construction
Prompt Date	LME term for the delivery date of a specific contract
RFET	Risk Factor Eligibility Test – FRTB modellability assessment for each risk factor
SHFE	Shanghai Futures Exchange – primary Chinese metals exchange
SOFR	Secured Overnight Financing Rate – USD risk-free rate replacing LIBOR
SONIA	Sterling Overnight Index Average – GBP overnight benchmark rate
SR 11-7	US Federal Reserve model risk management supervisory guidance (2011)
SS1/23	PRA (UK) supervisory statement on model risk management (2023)
TCE	Time Charter Equivalent – standardised daily freight rate metric
Term Structure	The relationship between price and time to delivery across all tenors
TTF	Title Transfer Facility – primary European natural gas pricing hub (Netherlands)
UK ETS	United Kingdom Emissions Trading System – post-Brexit UK carbon market
UKA	UK Allowance – permit to emit 1 tonne CO₂ in the UK ETS
VaR	Value at Risk – statistical measure of potential portfolio loss
VLCC	Very Large Crude Carrier – oil tanker vessel >200,000 DWT
White Premium	Price difference between white refined sugar and raw sugar
