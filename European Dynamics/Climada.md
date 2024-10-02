CLIMate ADAptation 
is a probabilistic natural catastrophe impact model thath also calculates averted damage

https://climada-python.readthedocs.io/en/latest/index.html


**Features:**
- Create probabilistic impact data from event sets
- Effects of climate change
- Effects of measures 

*Highly customizable*

Statistical risk could be referring to any number or things:
- Expected losses due to flood
- Number of people displaced
- Annual disruption to a railway

Climada's Impact object is used to analyse events and event sets

Split into 2 parts (repos)

1. Core climada_python: Contains all the modules for the probabilistic impact, averted damage, etc. Litpop is included as a demo **Exposure** module, Tropical cyclones is included as a demo **Hazard** module.
2. Petals climada_petals: contains all the modules for **generating** data. Is build upon the core and does not work alone

**Core**
1. Hazard: Stores geographical hazard footprints (water lever, wind speed, drought), metadata (frequency). There are predefined extensions for creating hazards from dataset/models: 
	- Tropical cyclone wind: calculates wind fields
	- European windstorms: 

2. Entity: Container for socio-economic mode, holding exposures and Impact functions for risk analysis.
	- Exposures: Geolocated data representing assets, population.
		- LitPop: Economic model using nightlight and population maps
		- Polygon_Lines: Exposure data in the form of shapes/lines
	- ImpactFuncSet: Describes how hazards affect exposures. Includes functions like:
		- IFTropCyclone: Tropical cyclones
		- IFRiverFloof: river floods
		- IFStormEurope: European windstorms
	- DiscRates: Annual discount rates
	- MeasureSet: Collection of adaptation measures that affecte exposure, hazzards and impacts
3. Preforms main model calculations combining Hazard and Entinty objects
	- Impact: Calculates the impact of hazards on exposures
	- Impact_data: Reads disaster impact data
	- CostBenefit. Apraises adaptation measures by comparing the costs and impacts
4. Unsequa: Uncertenty and sensitivity analysis module
	- helper: provides tools for generating uncertainty variables
5. Forecast: Handles weather forecasts, predicsts impacts

**Climada_petals**

1. Hazzard:
	- Storm surge: tropical cyclones
	- River flooding
	- Crop modeling
	- WildFires
	- Landslide
	- TCForecast
	- Emulator: Sample events from hazard dbs
	- Drought
2. Entity
	- Exposures:
		- Black Marblel :Economic model
		- Open streetmap: Utilizes open streetmap for risk modeling
3. Engine:
	- Supply Chain: Assesss indirect impacts using Input/Output modeling
	


**UseCase**
1. Define Hazard:
	- Select type of hazard
2. Define exposures:
	- Define assets that will be exposed to hazard (humans, crops,buildings)
3. Define Impact Function:
	 - Specify how the hazard affects the exposure
		E.g For a tropical cyclone use according classs which models the % of damage based on windspeed
		