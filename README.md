# COVID-19 SIR mathematical model for Spain

SIR mathematical model for infectious diseases optimized for COVID-19 using Spanish Ministry of Health public available data.

-----

![sir-cases](https://github.com/agastalver/sir-covid-19-spain/raw/master/images/generated-sir-cases.png "SIR Model Cases")

![sir](https://github.com/agastalver/sir-covid-19-spain/raw/master/images/generated-sir.png "SIR Model")

**Note**: 

* `susceptible`, `infected`, and `recovered`, stand for the observable population; thus, the ones that can be detected. The actual values could be higher.
* `susceptible` is an estimated value calculated from `N` with respect to the `infected` and `recovered`, the actual value is not provided by the government.
* `recovered` stands for people who has recovered from the virus or has died; as considered in the SIR model.

-----

## Last optimization

### Case forecasting table

| Date           | Infected  | Cases      |
|:--------------:|:---------:|:----------:|
| **2020-04-07** | **81841** | **140595** |
| 2020-04-08     | 81389     | 144543     |
| 2020-04-09     | 80502     | 148021     |
| 2020-04-10     | 79247     | 151071     |
| 2020-04-11     | 77687     | 153741     |
| 2020-04-12     | 75880     | 156073     |
| 2020-04-13     | 73880     | 158108     |
| 2020-04-14     | 71732     | 159885     |
| 2020-04-15     | 69479     | 161437     |
| 2020-04-16     | 67153     | 162793     |

### Optimized SIR parameters

```
N = 175721.17668819404
beta = 0.39475271388987254
gamma = 0.05338543894267407
delta = 0.6439852526869312
delay = 0
```

* `delta` stands for a factor of reduction of `beta` during the lockdown.
* All results are available in the folders `images` and `data`.

-----

## Last data information

### Spanish total cases

![total](https://github.com/agastalver/sir-covid-19-spain/raw/master/images/generated-total.png "Total cases")

### Spanish cases per region

![ccaa](https://github.com/agastalver/sir-covid-19-spain/raw/master/images/generated-ccaa.png "CCAA cases")

-----

## Methodology

### Data sources

Main data source:

* Spanish government: https://www.mscbs.gob.es/profesionales/saludPublica/ccayes/alertasActual/nCov-China/situacionActual.htm
  * https://covid19.isciii.es/
  * https://covid19.isciii.es/resources/serie_historica_acumulados.csv

* Github: https://github.com/datadist/datasets
  * https://raw.githubusercontent.com/datadista/datasets/master/COVID%2019/nacional_covid19.csv

### Epidemiology model

This is based on the SIR epidemiology model proposed by W. O. Kermack and A. G. McKendrick in:

```
Kermack, W. O.; McKendrick, A. G. (1927). "A Contribution to the Mathematical Theory of Epidemics". Proceedings of the Royal Society A: Mathematical, Physical and Engineering Sciences. 115 (772): 700. Bibcode:1927RSPSA.115..700K. doi:10.1098/rspa.1927.0118. JSTOR 94815.
```

You can find the description on wikipedia: https://en.wikipedia.org/wiki/Mathematical_modelling_of_infectious_disease#The_SIR_model

### Optimization

The parameters `N`, `beta`, and `gamma`, are unknown. Additionally, a `delay` parameter is considered; defined as a time synchronization parameter in case the available data is not adjusted to day 0.

The optimization method is Nendel-Mead, adjusting mean squares on `I(t)` and `R(t)` to the available data. `S(t)` and `N` are calculated backwards.

```
Nelder, John A.; R. Mead (1965). "A simplex method for function minimization". Computer Journal. 7 (4): 308–313. doi:10.1093/comjnl/7.4.308.
```

## Usage

Execute:

```
$ python main.py
```

## Important note

The mathematical model could not adjust to the real behaviour of the virus. Furthermore, the data can have errors, delays, or be incomplete, so the adjustment can vary in the future.
