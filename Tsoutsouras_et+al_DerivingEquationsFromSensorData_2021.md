[[Tsoutsouras_et+al_DerivingEquationsFromSensorData_2021]]

# [Deriving equations from sensor data using dimensional function synthesis](https://dx.doi.org/10.1145/3465216)

## [[Vasileios Tsoutsouras]]; [[Sam Willis]]; [[Phillip Stanley-Marbell]]

### 2021

## Abstract
==We present a new method for deriving functions that model the relationship between multiple signals in a physical system==. The method, which we call dimensional function synthesis , applies to data streams where the dimensions of the signals (e.g., length, mass, etc.) are known. The method comprises two phases: a compile-time synthesis phase and a subsequent calibration using sensor data. We implement dimensional function synthesis and use the implementation to demonstrate efficiently summarizing multimodal sensor data for two physical systems using 90 laboratory experiments and 10,000 synthetic idealized measurements. ==The results show that our technique can generate models in less than 300 ms on average across all the physical systems we evaluated==. This is a marked improvement when compared to an average of 16 s for training neural networks of comparable accuracy on the same computing platform. When calibrated with sensor data, our models outperform traditional regression and neural network models in inference accuracy in all the cases we evaluated. In addition, our models perform better in training latency (up to 1096X improvement) and required arithmetic operations in inference (up to 34X improvement). These significant gains are largely the result of exploiting information on the physics of signals that has hitherto been ignored.

## Key concepts
#claim/synthesis; #claim/physical_system; #dimensional_analysis; #register_transfer_level; #physics; #predictive_model; #discrete_fourier_transform; #claim/physical_dimension; #neural_network_model; #reduced_row_echelon_form; #linear_feedback_shift_registers; #arithmetic_operations

## Quote
> Evaluation on a physical pendulum We evaluate our method in the presence of nonsynthetic data where the underlying relationship is more complex than a simple closed-form equation


## Figures
![Figure 1. Dimensional function synthesis uses information about physical dimensions to generate a family of candidate equations. It then uses sensor measurements to calibrate the set of candidate equations](https://engine.scholarcy.com/images/full_text.pdf_attq2rfh_images_m8wf4d13/img-001.png)
![Figure 2. A glider of mass m launched with initial velocity v moves through space with velocity v under gravitational acceleration g. 0](https://engine.scholarcy.com/images/full_text.pdf_attq2rfh_images_m8wf4d13/img-002.png)
![Figure 3. a) A simple pendulum with mass m, rod of length l, period of swing t, and with the component of the acceleration due to gravity in its plane of motion being g. (b) Physical description for the ideal pendulum written in Newton](https://engine.scholarcy.com/images/full_text.pdf_attq2rfh_images_m8wf4d13/img-003.png)
![Figure 4. Prediction error versus computational requirements for predicting the trajectory of a glider. Our model uses linear regression for fitting function Φ′ of Equation (11) (denoted as “our model” in the lower left corner). It Pareto-dominates all the neural network variants (891 different network topologies), which are used for fitting function Ψ of Equation (10)](https://engine.scholarcy.com/images/full_text.pdf_attq2rfh_images_m8wf4d13/img-004.png)
![Figure 5. Prediction error versus computational requirements for predicting the trajectory of a glider. Subfigure (a) corresponds to the straightforward application of neural networks for fitting function Ψ of Equation (10). Subfigure (b) corresponds to our approach using a neural network for fitting function Φ′ of Equation (11). We train all models against a set of 20 input data points. Our method achieves prediction error of 0.17% via an approximately 2.5× less computationally demanding model](https://engine.scholarcy.com/images/full_text.pdf_attq2rfh_images_m8wf4d13/img-005.png)
![Figure 6. a) Our experimental setup for the variable-g pendulum. (b) Data collected from the 3-axis accelerometer over time using the wireless sensor on the pendulum. The largest component of oscillation is due to the motion of the pendulum. (c) Discrete Fourier Transform (DFT) of 10 s windows of the sampled acceleration data. Despite the variation of signal properties over time, the dominating frequency remains around 2 Hz. (d) The time period of the pendulum, calculated according to the dominating frequency in each time window of DFT, exhibits a small variation of about 20 ms over a 1-minute interval](https://engine.scholarcy.com/images/full_text.pdf_attq2rfh_images_m8wf4d13/img-006.png)
![Figure 7. Percentage error of the predicted period of the variable-g pendulum, t for a given length l and gravitational acceleration, g. Subfigure (a) includes all experimental instances in a subset of which the ideal pendulum model assumptions are violated leading to high deviations. Subfigure (b) zooms in the region, where the error of synthesized dimensional functions is minimized](https://engine.scholarcy.com/images/full_text.pdf_attq2rfh_images_m8wf4d13/img-007.png)
![Figure 8. Percentage error of the predicted period of the variable-g pendulum, t for a given length l, and gravitational acceleration, g. We predict using neural networks and regression models](https://engine.scholarcy.com/images/full_text.pdf_attq2rfh_images_m8wf4d13/img-008.png)
![Figure 9. The hardware generated by dimensional circuit synthesis preprocesses k sensor signals to calculate N < k dimensionless products Π1... ΠN. A predictive model takes the calculated product values as input and generates an inference output](https://engine.scholarcy.com/images/full_text.pdf_attq2rfh_images_m8wf4d13/img-009.png)

## Key points
- Physical systems instrumented with sensors can generate large volumes of data
- We examine the ability of our method to find the relation between trajectory height and the rest of the physical parameters of the glider
- Dimensional function synthesis provides two options for the calibration phase: (1) performing calibration on the target embedded system; and (2) performing calibration offline on a computing system that is not constrained by resources
- Evaluation on a physical pendulum We evaluate our method in the presence of nonsynthetic data where the underlying relationship is more complex than a simple closed-form equation
- We present an automated method for generating the family of functions from which to learn a model, based on information about the physical dimensions of the signals in the system
- We implement dimensional function synthesis and evaluate the execution cost and accuracy of the models our method generates compared against regression models and neural networks

## Synopsis

### Introduction
Physical systems instrumented with sensors can generate large volumes of data.
These data are useful in understanding previous behaviors of the systems that generate them as well as in predicting future behaviors of those systems.
Unlike data sources such as speech or text, data from sensors of physical phenomena must obey the laws of physics.
Existing methods for constructing predictive models from sensor data do not fully exploit prior knowledge of the physical interpretation of sensor data.
We use information about physical dimensions of sensor signals to synthesize compact predictive models from sensor data.
The state of the art in deriving models from such data streams is to apply some dimensions (e.g., LMT-2)

### Objectives
Our goal is to obtain a model relating t, the length of the rod l, and the component g of the acceleration due to gravity in the plane of rotation of the pendulum.
This simpler form is valuable when our goal is to perform the final calibration on a resource-constrained embedded system

### Methods
Despite its use in programming languages for tasks such as extending type systems with units of measure,[^1], [^2], [^3], [^5], [^8], [^12], [^10], [^14], [^17], [^23] physical information in the form of dimensions has seen limited use in building models of physical systems from data.
Dimensional function synthesis Dimensional function synthesis is a new method to efficiently derive functions relating the values from multiple streams of data from physical systems with known physical dimensions.
The insight behind the method is that any equation relating physical quantities must obey the principle of dimensional homogeneity from dimensional analysis[^6]: the two sides of an equation, an addition, or a subtraction, must have the same physical dimensions

### Results
**Evaluation for synthetic data**<br/><br/>We first compare dimensional function synthesis to regression and neural networks using synthetic idealized data.
The parameters used to describe the glider result in multiple Π groups, each of which includes multiple Π products
In this case, the form of the function Φ′ for combining the Π products into an equational model is unknown and we must use a data-driven approach to find its form.
We perform a series of experiments in our laboratory using an apparatus known as a variable-g pendulum (Figure 6a)
This apparatus uses a mass on a stiff rod swinging about a pivot which is at an angle that is not perpendicular to the horizon.
We instrument this apparatus with a wireless sensor containing a 3-axis accelerometer at the “bob” end of the pendulum to provide a data stream from which we automate measuring the period of oscillation, t.

### Conclusion
Existing methods for constructing retrospective or predictive models for data from physical systems do not fully exploit information about the physics of the systems in question.
We present an automated method for generating the family of functions from which to learn a model, based on information about the physical dimensions of the signals in the system.
We implement dimensional function synthesis and evaluate the execution cost and accuracy of the models our method generates compared against regression models and neural networks.
When calibrated with sensor data, our models outperform traditional regression and neural network models in inference accuracy in all the cases we evaluated.
Our models perform better in training latency and required arithmetic operations in inference.
These s­ignificant gains are largely the result of exploiting information on the physics of signals that has hitherto been ignored

## Data analysis
- #method/quadratic_regression
- #method/linear_regression

## Findings
- Linear regression on Φ′ outperforms the same technique on Ψ by more than 12%, although having similar computational requirements
- For pendulum lengths greater than 20 cm, the prediction error is always less than 15% even though each prediction requires only four floating-point operations

##  Builds on previous research
- The number of linearly independent columns of the dimensional matrix A is equal to rank(A). Thus, to find all possible solutions to Ak = 0 and hence all possible groups of dimensionless products, ==we can rearrange the n columns of A in ways to yield different null space solutions==.[^6], [^13]

## Contributions
- Existing methods for constructing retrospective or predictive models for data from physical systems do not fully exploit information about the physics of the systems in question. In this work, we present an automated method for generating the family of functions from which to learn a model, based on information about the physical dimensions of the signals in the system. The method, which we call dimensional function synthesis, applies to data streams where the dimensions of the signals are known.<br/><br/>We implement dimensional function synthesis and evaluate the execution cost and accuracy of the models our method generates compared against regression models and neural networks. When calibrated with sensor data, our models outperform traditional regression and neural network models in inference accuracy in all the cases we evaluated. In addition, our models perform better in training latency (up to 1096× improvement) and required arithmetic operations in inference (up to 34× improvement). These s­ignificant gains are largely the result of exploiting information on the physics of signals that has hitherto been ignored.


## References
[^1]: Allen, E., Chase, D., Luchangco, V., Maessen, J.-W., Steele, G.L., Jr. Object-oriented units of measurement. In Proceedings of the 19th Annual ACM SIGPLAN Conference on Object-oriented Programming, Systems, Languages, and Applications, OOPSLA’04 (2004), ACM, New York, NY, USA, 384–403. [[Allen_et+al_ObjectorientedUnitsMeasurement_2004]] [OA](https://engine.scholarcy.com/oa_version?query=Allen%2C%20E.%20Chase%2C%20D.%20Luchangco%2C%20V.%20Maessen%2C%20J.-W.%20Object-oriented%20units%20of%20measurement%202004) [GScholar](https://scholar.google.co.uk/scholar?q=Allen%2C%20E.%20Chase%2C%20D.%20Luchangco%2C%20V.%20Maessen%2C%20J.-W.%20Object-oriented%20units%20of%20measurement%202004) [Scite](https://engine.scholarcy.com/scite_url?query=Allen%2C%20E.%20Chase%2C%20D.%20Luchangco%2C%20V.%20Maessen%2C%20J.-W.%20Object-oriented%20units%20of%20measurement%202004)

[^2]: Antoniu, T., Steckler, P.A., Krishnamurthi, S., Neuwirth, E., Felleisen, M. Validating the unit correctness of spreadsheet programs. In Proceedings of the 26th International Conference on Software Engineering, ICSE’04 (2004), IEEE Computer Society, Washington, DC, USA, 439–448. [[Antoniu_et+al_ValidatingUnitCorrectnessSpreadsheetPrograms_2004]] [OA](https://engine.scholarcy.com/oa_version?query=Antoniu%2C%20T.%20Steckler%2C%20P.A.%20Krishnamurthi%2C%20S.%20Neuwirth%2C%20E.%20Validating%20the%20unit%20correctness%20of%20spreadsheet%20programs%202004) [GScholar](https://scholar.google.co.uk/scholar?q=Antoniu%2C%20T.%20Steckler%2C%20P.A.%20Krishnamurthi%2C%20S.%20Neuwirth%2C%20E.%20Validating%20the%20unit%20correctness%20of%20spreadsheet%20programs%202004) [Scite](https://engine.scholarcy.com/scite_url?query=Antoniu%2C%20T.%20Steckler%2C%20P.A.%20Krishnamurthi%2C%20S.%20Neuwirth%2C%20E.%20Validating%20the%20unit%20correctness%20of%20spreadsheet%20programs%202004)

[^3]: Babout, M., Sidhoum, H., Frecon, L. Ampere: A programming language for physics. European J. Phys. 11, 3 (1990):163. [[Babout_et+al_AmpereProgrammingLanguagePhysics_1990]] [OA](https://engine.scholarcy.com/oa_version?query=Babout%2C%20M.%20Sidhoum%2C%20H.%20Frecon%2C%20L.%20Ampere%3A%20A%20programming%20language%20for%20physics%201990) [GScholar](https://scholar.google.co.uk/scholar?q=Babout%2C%20M.%20Sidhoum%2C%20H.%20Frecon%2C%20L.%20Ampere%3A%20A%20programming%20language%20for%20physics%201990) [Scite](https://engine.scholarcy.com/scite_url?query=Babout%2C%20M.%20Sidhoum%2C%20H.%20Frecon%2C%20L.%20Ampere%3A%20A%20programming%20language%20for%20physics%201990)

[^4]: Barber, D. Bayesian Reasoning and Machine Learning. Cambridge University Press, Cambridge, 2012. [[Barber_BayesianReasoningMachineLearning_2012]] [OA](https://scholar.google.co.uk/scholar?q=Barber%2C%20D.%20Bayesian%20Reasoning%20and%20Machine%20Learning%202012) [GScholar](https://scholar.google.co.uk/scholar?q=Barber%2C%20D.%20Bayesian%20Reasoning%20and%20Machine%20Learning%202012) 

[^5]: Biggs, G., Macdonald, B.A. A pragmatic approach to dimensional analysis for mobile robotic programming. Auton. Robots 25, 4 (Nov. 2008), 405–419. [[Biggs_PragmaticApproachDimensionalAnalysisMobile_2008]] [OA](https://scholar.google.co.uk/scholar?q=Biggs%2C%20G.%20Macdonald%2C%20B.A.%20A%20pragmatic%20approach%20to%20dimensional%20analysis%20for%20mobile%20robotic%20programming.%20Auton.%20Robots%2025%2C%204%202008-11) [GScholar](https://scholar.google.co.uk/scholar?q=Biggs%2C%20G.%20Macdonald%2C%20B.A.%20A%20pragmatic%20approach%20to%20dimensional%20analysis%20for%20mobile%20robotic%20programming.%20Auton.%20Robots%2025%2C%204%202008-11) 

[^6]: Buckingham, E. On physically similar systems; Illustrations of the use of dimensional equations. Phys. Rev. 4, 4 (1914), 345–376. [[Buckingham_PhysicallySimilarSystemsIllustrationsDimensional_1914]] [OA](https://engine.scholarcy.com/oa_version?query=Buckingham%2C%20E.%20On%20physically%20similar%20systems%3B%20Illustrations%20of%20the%20use%20of%20dimensional%20equations%201914) [GScholar](https://scholar.google.co.uk/scholar?q=Buckingham%2C%20E.%20On%20physically%20similar%20systems%3B%20Illustrations%20of%20the%20use%20of%20dimensional%20equations%201914) [Scite](https://engine.scholarcy.com/scite_url?query=Buckingham%2C%20E.%20On%20physically%20similar%20systems%3B%20Illustrations%20of%20the%20use%20of%20dimensional%20equations%201914)

[^7]: Carlson, D.E. A mathematical theory of physical units, dimensions, and measures. Arch. Rational Mechanics Anal. 70, 4 (1979), 289–305. [[Carlson_MathematicalTheoryPhysicalUnitsDimensions_1979]] [OA](https://engine.scholarcy.com/oa_version?query=Carlson%2C%20D.E.%20A%20mathematical%20theory%20of%20physical%20units%2C%20dimensions%2C%20and%20measures%201979) [GScholar](https://scholar.google.co.uk/scholar?q=Carlson%2C%20D.E.%20A%20mathematical%20theory%20of%20physical%20units%2C%20dimensions%2C%20and%20measures%201979) [Scite](https://engine.scholarcy.com/scite_url?query=Carlson%2C%20D.E.%20A%20mathematical%20theory%20of%20physical%20units%2C%20dimensions%2C%20and%20measures%201979)

[^8]: Cmelik, R.F., Gehani, N.H. Dimensional analysis with C++. IEEE Softw. 5, 3 (1988), 21–27. [[Cmelik_DimensionalAnalysisWithC_1988]] [OA](https://engine.scholarcy.com/oa_version?query=Cmelik%2C%20R.F.%20Gehani%2C%20N.H.%20Dimensional%20analysis%20with%20C%2B%2B%201988) [GScholar](https://scholar.google.co.uk/scholar?q=Cmelik%2C%20R.F.%20Gehani%2C%20N.H.%20Dimensional%20analysis%20with%20C%2B%2B%201988) [Scite](https://engine.scholarcy.com/scite_url?query=Cmelik%2C%20R.F.%20Gehani%2C%20N.H.%20Dimensional%20analysis%20with%20C%2B%2B%201988)

[^9]: Carlson, D.E. On some new results in dimensional analysis. Arch. Ration. Mech. Anal. 68, 3 (1978), Springer, 191–210. [[Carlson_SomeResultsDimensionalAnalysisArch_1978]] [OA](https://engine.scholarcy.com/oa_version?query=Carlson%2C%20D.E.%20On%20some%20new%20results%20in%20dimensional%20analysis.%20Arch.%20Ration%201978) [GScholar](https://scholar.google.co.uk/scholar?q=Carlson%2C%20D.E.%20On%20some%20new%20results%20in%20dimensional%20analysis.%20Arch.%20Ration%201978) [Scite](https://engine.scholarcy.com/scite_url?query=Carlson%2C%20D.E.%20On%20some%20new%20results%20in%20dimensional%20analysis.%20Arch.%20Ration%201978)

[^10]: Hilfinger, P.N. An ada package for dimensional analysis. ACM Trans. Program. Lang. Syst. 10, 2 (Apr. 1988), 189–203. [[Hilfinger_PackageDimensionalAnalysis_1988]] [OA](https://engine.scholarcy.com/oa_version?query=Hilfinger%2C%20P.N.%20An%20ada%20package%20for%20dimensional%20analysis%201988-04-02) [GScholar](https://scholar.google.co.uk/scholar?q=Hilfinger%2C%20P.N.%20An%20ada%20package%20for%20dimensional%20analysis%201988-04-02) [Scite](https://engine.scholarcy.com/scite_url?query=Hilfinger%2C%20P.N.%20An%20ada%20package%20for%20dimensional%20analysis%201988-04-02)

[^11]: Hills, D.J.A., Grütter, A.M., Hudson, J.J. An algorithm for discovering Lagrangians automatically from data. PeerJ Comput. Sci. 1, (Nov. 2015), e31. [[Hills_et+al_AlgorithmDiscoveringLagrangiansAutomaticallyFrom_2015]] [OA](https://engine.scholarcy.com/oa_version?query=Hills%2C%20D.J.A.%20Gr%C3%BCtter%2C%20A.M.%20Hudson%2C%20J.J.%20An%20algorithm%20for%20discovering%20Lagrangians%20automatically%20from%20data%202015-11-01) [GScholar](https://scholar.google.co.uk/scholar?q=Hills%2C%20D.J.A.%20Gr%C3%BCtter%2C%20A.M.%20Hudson%2C%20J.J.%20An%20algorithm%20for%20discovering%20Lagrangians%20automatically%20from%20data%202015-11-01) [Scite](https://engine.scholarcy.com/scite_url?query=Hills%2C%20D.J.A.%20Gr%C3%BCtter%2C%20A.M.%20Hudson%2C%20J.J.%20An%20algorithm%20for%20discovering%20Lagrangians%20automatically%20from%20data%202015-11-01)

[^12]: Hills, M., Chen, F., Rosu, F. A rewriting logic approach to static checking of units of measurement in C. Electron. Notes Theor. Comput. Sci. 290, (Dec. 2012), 51–67. [[Hills_et+al_RewritingLogicApproachStaticChecking_2012]] [OA](https://engine.scholarcy.com/oa_version?query=Hills%2C%20M.%20Chen%2C%20F.%20Rosu%2C%20F.%20A%20rewriting%20logic%20approach%20to%20static%20checking%20of%20units%20of%20measurement%20in%20C%202012-12) [GScholar](https://scholar.google.co.uk/scholar?q=Hills%2C%20M.%20Chen%2C%20F.%20Rosu%2C%20F.%20A%20rewriting%20logic%20approach%20to%20static%20checking%20of%20units%20of%20measurement%20in%20C%202012-12) [Scite](https://engine.scholarcy.com/scite_url?query=Hills%2C%20M.%20Chen%2C%20F.%20Rosu%2C%20F.%20A%20rewriting%20logic%20approach%20to%20static%20checking%20of%20units%20of%20measurement%20in%20C%202012-12)

[^13]: Jonsson, D. Dimensional analysis: A centenary update. arXiv preprint arXiv:1411.2798 (2014). [[Jonsson_DimensionalAnalysisCentenaryUpdate_2014]] [OA](https://arxiv.org/pdf/1411.2798)  

[^14]: Kennedy, A. Dimension types. In Proceedings of the 5th European Symposium on Programming: Programming Languages and Systems, ESOP’94 (1994), SpringerVerlag, London, UK, 348–362. [[Kennedy_DimensionTypes_1994]] [OA](https://engine.scholarcy.com/oa_version?query=Kennedy%2C%20A.%20Dimension%20types%201994) [GScholar](https://scholar.google.co.uk/scholar?q=Kennedy%2C%20A.%20Dimension%20types%201994) [Scite](https://engine.scholarcy.com/scite_url?query=Kennedy%2C%20A.%20Dimension%20types%201994)

[^15]: Lim, J., Stanley-Marbell, P. Newton: A language for describing physics. CoRR, abs/1811.04626 (2018). [[Lim_NewtonLanguageDescribingPhysics_2018]] [OA](https://arxiv.org/pdf/1811.04626)  

[^16]: Rayleigh, L. The principle of similitude. Nature 95 (Dec. 1915), 66–68. [[Rayleigh_PrincipleSimilitude_95 (Dec.]] [OA](https://engine.scholarcy.com/oa_version?query=Rayleigh%2C%20L.%20The%20principle%20of%20similitude%2095%20%28Dec.) [GScholar](https://scholar.google.co.uk/scholar?q=Rayleigh%2C%20L.%20The%20principle%20of%20similitude%2095%20%28Dec.) [Scite](https://engine.scholarcy.com/scite_url?query=Rayleigh%2C%20L.%20The%20principle%20of%20similitude%2095%20%28Dec.)

[^17]: Rittri, M. Dimension inference under polymorphic recursion. In Proceedings of the Seventh International Conference on Functional Programming Languages and Computer Architecture, FPCA’95 (1995), ACM, New York, NY, USA, 147–159. [[Rittri_DimensionInferenceUnderPolymorphicRecursion_1995]] [OA](https://engine.scholarcy.com/oa_version?query=Rittri%2C%20M.%20Dimension%20inference%20under%20polymorphic%20recursion%201995) [GScholar](https://scholar.google.co.uk/scholar?q=Rittri%2C%20M.%20Dimension%20inference%20under%20polymorphic%20recursion%201995) [Scite](https://engine.scholarcy.com/scite_url?query=Rittri%2C%20M.%20Dimension%20inference%20under%20polymorphic%20recursion%201995)

[^18]: Rudy, S.H., Brunton, S.L., Proctor, J.L., Kutz, J.N. Data-driven discovery of partial differential equations. Sci. Adv. 3, 4 (2017), e1602614. [[Rudy_et+al_DatadrivenDiscoveryPartialDifferentialEquations_2017]] [OA](https://engine.scholarcy.com/oa_version?query=Rudy%2C%20S.H.%20Brunton%2C%20S.L.%20Proctor%2C%20J.L.%20Kutz%2C%20J.N.%20Data-driven%20discovery%20of%20partial%20differential%20equations%202017) [GScholar](https://scholar.google.co.uk/scholar?q=Rudy%2C%20S.H.%20Brunton%2C%20S.L.%20Proctor%2C%20J.L.%20Kutz%2C%20J.N.%20Data-driven%20discovery%20of%20partial%20differential%20equations%202017) [Scite](https://engine.scholarcy.com/scite_url?query=Rudy%2C%20S.H.%20Brunton%2C%20S.L.%20Proctor%2C%20J.L.%20Kutz%2C%20J.N.%20Data-driven%20discovery%20of%20partial%20differential%20equations%202017)

[^19]: Schmidt, M., Lipson, H. Distilling freeform natural laws from experimental data. Science 324, 5923 (2009), 81–85. [[Schmidt_DistillingFreeformNaturalLawsFrom_2009]] [OA](https://engine.scholarcy.com/oa_version?query=Schmidt%2C%20M.%20Lipson%2C%20H.%20Distilling%20freeform%20natural%20laws%20from%20experimental%20data%202009) [GScholar](https://scholar.google.co.uk/scholar?q=Schmidt%2C%20M.%20Lipson%2C%20H.%20Distilling%20freeform%20natural%20laws%20from%20experimental%20data%202009) [Scite](https://engine.scholarcy.com/scite_url?query=Schmidt%2C%20M.%20Lipson%2C%20H.%20Distilling%20freeform%20natural%20laws%20from%20experimental%20data%202009)

[^20]: Simon, V., Weigand, B., Gomaa, H. Dimensional Analysis for Engineers. Springer, Gewerbestrasse, Cham, Switzerland, 2017. [[Simon_et+al_DimensionalAnalysisEngineers_2017]] [OA](https://scholar.google.co.uk/scholar?q=Simon%2C%20V.%20Weigand%2C%20B.%20Gomaa%2C%20H.%20Dimensional%20Analysis%20for%20Engineers%202017) [GScholar](https://scholar.google.co.uk/scholar?q=Simon%2C%20V.%20Weigand%2C%20B.%20Gomaa%2C%20H.%20Dimensional%20Analysis%20for%20Engineers%202017) 

[^21]: Sonin, A.A. A generalization of the P-theorem and dimensional analysis. Proc. Natl. Acad. Sci. 101, 23 (2004), 8525–8526. [[Sonin_GeneralizationPtheoremDimensionalAnalysis_2004]] [OA](https://engine.scholarcy.com/oa_version?query=Sonin%2C%20A.A.%20A%20generalization%20of%20the%20P-theorem%20and%20dimensional%20analysis%202004) [GScholar](https://scholar.google.co.uk/scholar?q=Sonin%2C%20A.A.%20A%20generalization%20of%20the%20P-theorem%20and%20dimensional%20analysis%202004) [Scite](https://engine.scholarcy.com/scite_url?query=Sonin%2C%20A.A.%20A%20generalization%20of%20the%20P-theorem%20and%20dimensional%20analysis%202004)

[^22]: Strang, G. Introduction to Linear Algebra, 5th edn. WellesleyCambridge Press, Wellesley, MA, 2016. [[Strang_IntroductionLinearAlgebra_2016]] [OA](https://scholar.google.co.uk/scholar?q=Strang%2C%20G.%20Introduction%20to%20Linear%20Algebra%202016) [GScholar](https://scholar.google.co.uk/scholar?q=Strang%2C%20G.%20Introduction%20to%20Linear%20Algebra%202016) 

[^23]: Umrigar, Z.D. Fully static dimensional analysis with C++. SIGPLAN Not. 29, 9 (Sept. 1994), 135–139. This work is licensed under a http://creativecommons.org/licenses/by/4.0/ [[Umrigar_FullyStaticDimensionalAnalysisWith_1994]] [OA](http://creativecommons.org/licenses/by/4.0/)  

