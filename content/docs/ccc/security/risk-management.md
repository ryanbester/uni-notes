---
title: "4. Risk Management"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 4. Risk Management

[🔒 Recording](https://github.com/ryanbester/uni-resources/tree/main/ccc/y1/security/4-risk-management)

## Risk = Likelihood X Impact

A componenent-driven approach requires the risk analyst to assess three elements of risk: threat, vulnerability, and impact.

Threat is the individual, group, or circumstance which causes a given impact to occur, e.g. lone hacker, state-sponsered group, staff member who has made a mistake, or high-impact weather.

The purpose of assessing threat is to improve the assessment of how likely a given risk is to be realised.

## IS Risk Methods and Frameworks

Risk Assessment Methods/Frameworks:

- [NIST 800-3](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-30r1.pdf)
- ISO/IEC 27005
- ISACA COBIT
- ISF IRAM 2
- HMG Information Assurance Standard 1 2
- Octave Allegro
- ISACA COBIT 5

IS Management Frameworks:

- [NIST CSF](https://www.nist.gov/cyberframework)
- ISO/IEC 27000 series

### NIST Cyber Security Framework

![NIST Cyber Security Framework](/img/ccc/y1/security/nist-cyber-security-framework.png)

## Risk Assessment Steps

- **Identify**:
    - Assets
    - Threats
    - Existing Controls
    - Vulnerabilities
    - Consequences
- **Analyse**:
    - Assessment of consequences
    - Assessment of incident likelihood
    - Level of risk determination
- **Treat**:
    - Risk modification
    - Risk retention
    - Risk avoidance
    - Risk sharing
- **Monitor**:
    - Monitoring and review

### Qualitative Risk Analysis

Uses scale of qualifying attributes to describe magnitude of consequences/likelihood.

- **Advantage**: Ease of understanding by all relevant personnel
- **Disadvantage**: Dependence on subjective choice of the scale
- **May be used**:
    - As initial screening, to identify risks requring detailed analysis
    - Where the analysis is sufficient for decisions
    - Where numerical data/resources inadequate for quantitative analysis

### Quantitative Risk Analysis

Uses scale of objective numerical values for consequences/likelihood.

- Uses data from a variety of sources
- Quality of analysis depends on accuracy/completeness of numerical data
- Typically uses historial incident data:
    - **Advantage**: Related directly to IS objectives/concerns of organisation
    - **Disadvantages**: Lack of data on new risks, accurate/missing data in general could create illusion of worth/accuracy of risk assessment
- Uncertainty and variability of consequences/likelihood are to be considered and communicated

## Cost Benefit Analysis

- **CBA**: Cost Benefit Analysis
- **ACS**: Annualised Cost of Safeguard
- **ALE**: Annualised Loss Expectancy
- **SLE**: Single Loss Expectancy
- **ARO**: Annualised Rate of Occurence

CBA = ALE(prior) - (ALE(post) + ACS)

ALE = SLE x ARO

| Risks | ALE (prior) | SLE | ARO | ALE (post) | ACS | CBA |
|:-----:|:-----------:|:---:|:---:|:----------:|:---:|:---:|
| A | $26k | $500 | 12x | $6k | $3k | $17k |
| C | $25k | $75k | 0.1x | $7.5k | $5k | $12.5k |

## Risk Treatment Options

- **Retain/Accept**: Organisation may tolerate (but not ignore) risk
- **Avoid/Terminate**: Organisation may decide nto to do the thing that incurs risk
- **Share/Transfer**: Transfer risk via an insurance policy or a third party
- **Modify/Reduce**: Adopt controls to lower the current level of risk
    - by reducing likelihood
    - by reducing impact

## Critical Appraisal of Risk Methods and Frameworks

[This](https://serviceteamit.co.uk/news/a-critical-appraisal-of-risk-methods-and-frameworks/) was originally produced by NCSC so practioners and decision makers can better understand and work with the approaches available.

- Limits of a 'reductionist' approach
- Lack of variety
- Limits of a 'fixed state' approach
- Lack of feedback and control
- Losing risk signals in the 'security noise'
- System operation
- Information opacity
- Noise from misguided analysis
- Noise from bias
- Assumed determinability
- Abstraction through labelling
- The limits of using matrices
- Limits in the way uncertainty is presented
- The effect risk relationships have on impact
- The adverse effect of intervention
- Impacts are not limited to the scope of assessment
- The effect of time on risk
