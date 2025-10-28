<p align="center">
  <img src="Logo.png" alt="Description" width="30%">
</p>

# Coordinating Multi-Market Participation, Power Purchase Agreements, and Geo-Distributed Site Operations in Hydrogen Enterprises: An Equilibrium-Based ADMM

This repository contains the implementation of the optimization framework developed for the paper “**Valuing Coordinated Scheduling, Risk Management, and Power Purchase Agreements for Industrial Hydrogen Enterprises in the Hydrogen, Electricity, and Green Certificate Markets**”. It has been developed as part of the **WinHy** project, funded by the Dutch Research Council (NWO) and Repsol S.A.

## 📝 Description

The work introduces a portfolio-level optimization model for hydrogen enterprises, i.e., multi-site, multi-asset agents actively participating in electricity, hydrogen, and green certificate markets, while also managing both physical and virtual Power Purchase Agreements (PPAs). These enterprises face the dual challenge of optimizing their geographically distributed operations and aligning their strategies with evolving green hydrogen policy requirements. The framework integrates four main dimensions:

### 1. Operational Coordination
- Portfolio-level scheduling of decentralized sites, each comprising electrolyzers, Steam Methane Reforming (SMR) technologies, renewable generation units, and electrical energy storage (EES) systems.  
- Management of flexible downstream processes (DSPs) with hydrogen demand shifting.  

### 2. Multi-Market Participation
- Joint clearing of electricity, hydrogen (bundled/unbundled), and green certificate markets.  
- Explicit modeling of interdependencies between market prices and contractual arrangements.  

### 3. Contractual Engagement
- Incorporation of both physical and virtual PPAs as capacity-based agreements.  
- Analysis of how PPAs influence and are influenced by market-clearing dynamics.  

### 4. Risk and Policy Compliance
- Integration of Conditional Value at Risk (CVaR) to evaluate portfolio-level vs. site-level risk hedging strategies.  
- Implementation of EU green hydrogen standards (RED III), ensuring temporal alignment between renewable electricity consumption and hydrogen production through Guarantee of Origin (GO) certificates.  
##
The problem is formulated as a Generalized Nash Equilibrium (GNE) to capture the strategic interactions among multiple self-interested agents, each optimizing its own objectives while being interconnected through shared markets and contracts. This formulation is particularly suited to modeling hydrogen enterprises and other agents (renewables, thermal units) that must balance cost efficiency, contractual obligations, and policy compliance in multi-market environments.
##
To solve this complex decentralized problem, the framework employs an adaptive Alternating Direction Method of Multipliers (ADMM). Unlike standard ADMM, which uses fixed penalty parameters and may converge slowly, the adaptive approach dynamically updates penalty factors during iterations. This adaptive tuning accelerates convergence, reduces computation time, and ensures stable outcomes even under uncertainty. Importantly, the ADMM-based coordination mechanism enables privacy-preserving interactions, since each agent solves its own local optimization problem and only exchanges aggregated information with market settlers rather than full internal data.
##
### Agents Considered in the Framework

**1. Type A Hydrogen Enterprises**  
Operate multiple decentralized sites with electrolyzers, SMR units, renewable generation, energy storage, and flexible DSPs. They participate in electricity, bundled and unbundled hydrogen, and green certificate markets, as well as in physical and virtual PPAs. They employ the CVaR method to manage PPA-related uncertainties.  

**2. Type B Hydrogen Enterprises**  
Operate a single electrolyzer with inflexible DSP. They participate in electricity, hydrogen, and green certificate markets, and in both physical and virtual PPAs, but do not apply risk management strategies.  

**3. Type C Hydrogen Enterprises**  
Do not own hydrogen production units and act solely as consumers. They procure hydrogen from bundled and unbundled hydrogen markets and comply with clean sourcing requirements through the green certificate market.  

**4. Type A Renewable Units**  
These units sell electricity through physical PPAs and issue GOs for the buyer.  

**5. Type B Renewable Units**  
These units sell electricity through physical PPAs and issue GOs for the buyer.  

**6. Type C Renewable Units**  
Sell electricity in the electricity market and trade GOs in the green certificate market.  

**7. Type D Renewable Units**  
Flexibly allocate capacity between physical PPAs and the electricity market, while issuing and trading GOs accordingly.  

**8. Thermal Units**  
Provide dispatchable electricity generation and participate exclusively in the electricity market.  

---

## ✨ Key Features
1. **Operational Coordination**
   - Portfolio-level scheduling of decentralized sites, each comprising electrolyzers, Steam Methane Reforming (SMR) technologies, renewable generation units, and electrical energy storage (EES) systems.  
   - Management of flexible downstream processes (DSPs) with hydrogen demand shifting.  
2. **Multi-Market Participation**
   - Joint clearing of electricity, hydrogen (bundled/unbundled), and green certificate markets.  
   - Explicit modeling of interdependencies between market prices and contractual arrangements.  
3. **Contractual Engagement**
   - Incorporation of both physical and virtual PPAs as capacity-based agreements.  
   - Analysis of how PPAs influence and are influenced by market-clearing dynamics.  
4. **Risk and Policy Compliance**
   - Integration of Conditional Value at Risk (CVaR) to evaluate portfolio-level vs. site-level risk hedging strategies.  
   - Implementation of EU green hydrogen standards (RED III), ensuring temporal alignment between renewable electricity consumption and hydrogen production through Guarantee of Origin (GO) certificates.   


<!-- ## ⚙️ Model Highlights -->

---

## 🧪 Case Study
- **Case A**: The model is formulated in a deterministic single-scenario setting, where the Type A hydrogen enterprise operates without applying any risk management strategy.  
- **Case B**: The model is formulated in a scenario-based framework, where the Type A hydrogen enterprise applies a Conditional Value-at-Risk (CVaR) strategy at the portfolio level.   
- **Case C**: The model is also scenario-based, but the CVaR risk management strategy is applied individually at each site. This localized approach increases conservatism, leading to higher daily operating costs and more unused contracted PPA capacity compared to the portfolio-level strategy.
 

---

## 📊 Key Results
- **Value of PPAs**: Incorporating physical PPAs reduced daily operating costs for Type A, B, and C hydrogen enterprises by **24.27%**, **23.85%**, and **10.01%**, respectively.  
  Adding virtual PPAs achieved further reductions of **16.2%**, **15.51%**, and **0.77%** for the same enterprises.  
- **Impact on Market Prices**: The inclusion of PPAs lowered electricity market clearing prices by reducing reliance on expensive thermal units.  
  Green certificate market prices declined by up to **40.6%** (from €3.2 to €1.9 per GO) due to reduced demand from hydrogen enterprises.  
- **Operational Flexibility Benefits**: Activating EES systems reduced daily operating costs for Type A enterprises by **1.75%**, while enabling flexible DSPs increased cost reductions to **3.42%**.  
  The combination of EES and flexible DSPs allowed hydrogen enterprises to exploit hourly price variations, shifting demand and storage operation between peak and off-peak periods.  
- **Risk Management Insights**: Portfolio-level CVaR-based risk aversion reduced enterprise costs by up to **1.89%** compared to site-level risk aversion, while also improving PPA capacity utilization and flexibility.  
  Site-level risk aversion was more conservative, leading to **higher costs and greater unused PPA capacity**.  
- **Policy Impacts**: Increasing the green hydrogen target from **42% to 90%** raised daily costs by **3.46% (Type A)**, **2.25% (Type B)**, and **4.29% (Type C)**, mainly due to higher GO requirements and constrained scheduling flexibility.  
  Green certificate prices increased by **92%**, and hydrogen prices rose by up to **5.06%** in bundled markets and **2.08%** in unbundled markets.  
- **Algorithmic Performance**: The adaptive ADMM achieved significant improvements in computational efficiency, reducing convergence time by **237 seconds with 192 fewer iterations** in deterministic cases and by **2277 seconds with 452 fewer iterations** in scenario-based cases.  
---

## 📂 Repo Structure

```
├─ H2Enterprises.ipynb           # Main Jupyter Notebook with the optimization model
├─ SimData.xlsx                  # Excel file containing the input simulation data
└─ requirements.txt              # List of required Python packages
├─ Cases/                    
│  ├─ Case_A.ipynb               # Risk-neutral (deterministic) scheduling
│  ├─ Case_B.ipynb               # Portfolio-level risk-averse scheduling
│  └─ Case_C.ipynb               # Site-level risk-averse scheduling
```

---

## 🚀 Requirements

Install the necessary Python libraries using:

```bash
pip install -r requirements.txt
```

---

## 📈 How to Run

1. Open `H2Enterprises.ipynb` in Jupyter Notebook or JupyterLab.
2. Ensure `SimData.xlsx` is in the same directory as the notebook.
3. Run all cells in the notebook to execute the model and generate results.

---

## 📦 Dependencies

The code uses the following libraries:
- `pyomo`
- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `tabulate`
- `ipython`
- `jupyter`
- `openpyxl`

You also need a solver like GUROBI for Pyomo.

<!-- ## 📚 Citations
If you use this repository in your work, please cite: -->

---

## 📝 License

MIT License.
