# 📋 Project Overview

 This project implements a comprehensive Credit Risk Expected Loss (EL) model using the IFRS 9 / Basel framework. The model calculates Probability of Default (PD), Loss Given Default (LGD), and Expected Loss (EL) at both loan and portfolio levels, complete with stress testing capabilities.


# Key Features

* PD Modeling: Logistic regression with 0.8352 AUC score

* Risk-Sensitive LGD: Grade-based recovery rates (A through G)

* Expected Loss Calculation: EL = PD × LGD × EAD

* Portfolio Analytics: Aggregated risk metrics and loss ratios

* Stress Testing: Scenario analysis with PD (+20%) and LGD (+10%) shocks

# 📊 Dataset Features

The model uses the following borrower and loan characteristics:
| Feature	            |            Description          |
| ---------------------    | --------------------------- |
| person_age	               |     Borrower's age |
| person_income	            |    Annual income |
| person_home_ownership	     |   Home ownership status (RENT/MORTGAGE/OWN)|
| person_emp_length	        |    Employment length in years |
| loan_intent	                |    Purpose of loan |
| loan_grade	                |    Internal risk grade (A through G). |
| loan_amnt	                |    Loan amount (used as EAD).  |
| loan_int_rate	            |    Interest rate |
| loan_status                  |	Default status (target variable) |
| loan_percent_income	         |   Loan amount as % of income |
| cb_person_default_on_file	 |   Historical default flag |
| cb_person_cred_hist_length	  |  Credit history length |





# 🧮 Methodology
## 1. Probability of Default (PD)


### Model Performance:

* AUC: 0.8352 (Excellent discriminatory power)

* Gini Coefficient: 0.6703 (Strong model performance)

ROC Curve

Figure 1: ROC Curve showing model performance
    
## 2.   Loss Given Default (LGD)

* Risk-sensitive LGD based on loan grades:

  | Loan Grade   |	Recovery Rate | LGD |
  |------------  |----------------|-----|
  | A	         |     70%	      | 30% |
  | B	         |     60%	      | 40% |
  | C	         |     50%	      | 50% |
  | D	         |     40%	      | 60% |
  | E 	         |     30%	      | 70% |
  | F	         |     20%	      | 80% | 
  | G	         |     10%	      | 90% |

## 3. Exposure at Default (EAD)

* Proxy: Loan amount (loan_amnt)

* Rationale: Suitable for term loans where exposure is known at origination

## 4. Expected Loss Calculation

* EL = PD × LGD × EAD 

### 📈 Portfolio Results 
Baseline Metrics 
| Metric	      |           Value  |
|---------------|----------------|    
| Total Portfolio EL |	$34,378,150 |
| Average EL per Loan |	$1,200.44 |
| Portfolio Expected Loss Ratio   |	12.43% |
|  Total Exposure	|  ~$276.6 million  |

## Interpretation

* Loss Ratio: For every $100 lent, the model expects to lose $12.43

* Risk Profile: This indicates a high-yield/high-risk portfolio(subprime/near-prime lending)

* Business Implication: Interest rates must exceed 12.43% + operating  costs for profitability

# 📊 Model Validation Confusion Matrix text

| Actual:         |       Good       |         Bad      |
|------------|----------------|-------------------|
| Predicted: Good  |      4,237       |        1,781  |
| Predicted: Bad    |     206        |         504     |       

#  Key Metrics

* Total Population: 6,728 loans
* Default Rate: ~34%
* False Negatives: 1,781 (Type II error)
* False Positives: 206 (Type I error)

# 🔬 Stress Testing Scenario Parameters

* PD Shock : +20% (economic downturn, rising unemployment)

* LGD Shock : +10% (falling collateral values)

    | Stressed Results |
    | Metric	          |           Value	              |    Change |
    |-------------------|-----------------------|---------------------|
    | Stressed EL	        |         $45,379,158	       |   +32% |
    | Additional Loss	     |        $11,001,008	-      |          |
    | Stressed Loss Ratio	  |       16.4%	               |   +4 pp   |

#  Why 32% > 20% + 10%?

* The shocks compound multiplicatively:

* New EL = (1.2 × PD) × (1.1 × LGD) × EAD = 1.32 × Original EL

# Capital Implications

* Baseline Capital Required: $34.4M

* Stress Capital Buffer: $11.0M

* Total Risk Capital: $45.4M

# 🔍 Future Enhancements

### Advanced PD Modeling

*   Include categorical variables (one-hot encoding)
*   Test non-linear relationships
*   Implement XGBoost/Random Forest for comparison

### LGD Calibration

* Validate recovery rates against historical data

* Add collateral-type specific LGDs

* Consider economic cycle adjustments

### EAD Modeling

* Incorporate credit conversion factors for undrawn commitments

* Model prepayment behavior

### Advanced Stress Testing

* Macroeconomic scenario integration

* Reverse stress testing

* Sector/segment-specific shocks

# 📚 References

   *  Basel Framework: IRB Approach for Credit Risk

   *  IFRS 9: Expected Credit Loss Model

   *  Bank for International Settlements: Stress Testing Principles

# ⚠️ Disclaimer

###  This model is for educational and demonstration purposes. Real-world credit risk modeling requires:

   * Rigorous model validation

   *  Regulatory approval

   *  Ongoing performance monitoring

   *  Comprehensive documentation


Built with ❤️ using Python and statistical rigor


