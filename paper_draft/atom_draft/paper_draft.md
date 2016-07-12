# Measurements of protein expression and thermal stability for 128 single mutants of a glycoside hydrolase allows evaluation of stability predictions

## Author contributions (alphabetical by last name)

+ Dylan Alexander Carlin [2]: molecular cloning, designed experiments, wrote software used in analysis, analyzed data, Rosetta modeling, FoldX modeling, machine learning, wrote paper
+ Ryan Caster [1]: characterized expression for mutants
+ Bill Chan [1]: characterized Tm for mutants, analyzed data, contributed to paper
+ Natalie Damrau [1]: characterized mutants
+ Siena Hapig-Ward [1]: characterized Tm and kinetic constants, analyzed data, drew figures, contributed to paper
+ Mary Riley [1]: characterized mutants
+ Justin B. Siegel [1,3,4]: PI

## Author affiliations:

1. Genome Center, University of California, Davis CA, USA
2. Biophysics Graduate Group, University of California, Davis CA, USA
3. Department of Chemistry, University of California, Davis CA, USA
4. Department of Biochemistry & Molecular Medicine, University of California, Davis CA, USA

**Subject areas**: biochemistry, computational biology, machine learning

**Keywords**: enzyme, Rosetta, thermal stability

---

### Outline

+ Introduction

  + background
  + current data sets and problems gathering them
  + current computational approaches
  + summary of what we did
  + **Figure 1**: all positions selected in study


+ Methods

  + cloning and mutagenesis
  + production and purification
  + assay and data analysis
  + computational modeling and machine learning


+ Results

  + summary of all mutants, wild type values, limits of detection
  + mutants less thermostable, mutants more thermostable
  + **Figure 2**: heatmap with expression, Tm, kcat, km, kcat/km for each mutant
  + **Figure 3**: drawings of discussed mutants W120F, N404C, H178A, E222H
  + **Figure 4**: crystal structure with residues colored per change in Tm compared to wild type
  + Rosetta structural features predict expression, but not Tm
  + **Figure 5**: machine learning model evaluation


+ Discussion

  + summary of what we showed and connections to background
  + implications for biotechnology
  + implications for human health
  + conclusion


+ Supporting information

  1. Table of protein expression, melting temperature, kinetic constants, and statistical analysis for each of 125 mutants (CSV)
  1. Michaelis-Menten plots for each mutant for which kinetic constants are reported (ZIP file containing images)
  1. Plot of protein melting for each mutant for which Tm is reported (ZIP file containing images)
  1. Images of gel band for each protein used in this study (TIFF images)
  1. Additional information about experimental procedures (text)
  1. Additional information about machine learning (text)
  1. Rosetta input files (ZIP containing text files)

---

# Abstract

The importance of enzymes in biotechnology and human disease makes the accurate modeling of enzyme stability an important goal in biochemistry. Previous efforts to build predictive models of enzyme mutants have either suffered from inconsistent data sets, or data sets which are too small to enable evaluation of current predictive methods. Here, we present a large, self-consistent data set of protein soluble expression and melting temperature for a large (128 mutants) library of a family 1 glycoside hydrolase mutants. We then show the use of the experimental data to build a predicitve model of soluble enzyme expression and melting temperature. We show that, while models for predicting melting temperature require largeer data sets to become feasible, we are able to apply our model to a blind test set of 10 mutants, on which we achiveed practivcie acttauct of 0. percenty. We shown that automated molecuyalr biloogy compbined with highpthorughpout open sourced protyocols screning oif glycoside hydrolase nutants prives a path forward in the prediciton of the gunctional effects of single pioint mutants in enzymes. We show how this methodoloy could be used to design novel thermostable mutants. We show how this approach could be used to detect disease-causing missense mutations from gene sequence.

# Introduction

## Background

Enzymes' key roles in biotechnology and human disease make the accurate modeling of enzyme stability an important goal of the protein modeling community. Accurate prediction of a point mutation's effect on enzyme stability would unlock rational protein engineering approaches, where the information could be used immediately to rationally engineer an enzyme's functional envelope for a desired situation as has been previously explored \cite{22575958}. Furthermore, understanding the changes in enzyme stability that occur upon point mutations would provide huge insight into understanding inherited diseases of metabolism [cite], cancer [cite], as well as mechanisms by which bacteria become resistant to antibiotics, which is lately a public health menace [cite].  

## Enzyme stability data sets

Previous attempts to predict stability changes in proteins conferred by point mutations have not considered enzymes \cite{18632749} specifically, and have suffered by decades-old low-throughput molecular biology and biochemistry techniques. Thus, the largest data sets for which melting temperature $Tm$ is explicitly measured have been around 30 mutants [cite]. Other studies have collected large amounts of undata, but it suffers from convolution of separate/othoganal [we will show that kcat and tm are not correlated] parameters/fuzzy measuremetns [cite: Romero and others]. Large data sets of thermal stabilities also exist, yet the data sets collected there were created without regard for standardization for varying experimental conditions \cite{14681373} and so suffer from a lack of comparability between measurements. The result is that existing data sets either contain specific measurements for a small number of enzymes, or fuzzy measurements of large numbers of variants. This is likely due to the immense cost and outdated techniques of enzymology.

## Computational approaches to predicting the stability of point mutants

A number of computational approaches to predict the stability of enzyme mutations have in turn relied on these far from ideal data sets as training data. No study, that I can find, has combined both a standardized approach to experimental characterization, and produced enough mutants to allow a sufficiently large training set to evaluate predictive ability. Previous attempts to predict the effect of point mutations on antibodies (~100 residues) have used primary sequence and amino acid properties as features \cite{21710487}.

## Proposed approach to predicting the stability of point mutants of a family 1 glycoside hydrolase

We have previously shown the ability to select informative features from a set generated by Rosetta for the prediction of kinetic constants \cite{26815142} using structural features calculated from molecular models of BglB, a family 1 glycoside hydrolase. We hypothesized that a subset of Rosetta's feature set could be used to predict protein soluble expression as well as change in thermal stability conferred by point mutations to the BglB structure.

Here, we present protein soluble expression and thermal stability data for 115 single point mutants of BglB. In order to construct this data set, we relied on students learning about molecular modeling to design mutations predicted to be compatible with a model of the enzyme-substrate complex. High-thoughput robot automation was used to perform the molecular cloning, and open-source lab protocols, released on GitHub, were used to experimentally characterize 115 enzyme mutants. The experimental measurements were combined with ~30 structural features calculated from full-atom moelcular models of the enzyme-substrate complex and used to train machine learning classifiers to predict Tm and soluble expression. Model performance was evaluated ...

![](figure_1.png)

**Figure 1**: (A) PyMOL rendering of modeled BglB (yellow) in complex with pNPG (green) showing the Cɑ of the 60 sequence positions selected for this study (purple). (B) Reaction scheme of the hydrolysis of pNPG by BglB.

# Methods

## Mutant selection via molecular modeling in Foldit

The crystal structure of recombinant BglB in complex with the substrate analog 2-deoxy-2-fluoro-α-D-glucopyranose was used to identify the substrate binding pocket and the catalytic residues, and a macromolecular model of BglB was created using Rosetta. Functional constraints were used to define catalytic distances, angles, and dihedrals among 4-nitrophenyl-β-D-glucoside, E164, E353, and Y295. The structure was then loaded into Foldit, a graphical user interface to Rosetta. Point mutations to the protein were modeled, and a subset were chosen by students learning about molecular modeling. Generally, the designs had energies no more than 5 Rosetta energy units higher than the native structure.

## Molecular cloning and mutagenesis

A gene coding for BglB was codon-optimized for *Escherichia coli* and synthesized as linear dsDNA (Life Technologies). The construct was cloned into a pET29b+ vector using Gibson assembly using a commercial reagent mixture (NEB) and verified by Sanger sequencing (Genscript). Kunkel mutagenesis was used to generate designed variants of BglB via an automated cloud laboratory (Transcriptic).

## Protein production and purification

Sequence-verified constructs were transformed into *Escherichia coli* BL21(DE3). Single colonies were used to inoculate 5 mL TB in 50 mL Falcon tubes. After incubation at 37 C with shaking at 300 RPM for 24 hours, cells were pelleted and media replaced with 5 mL TB containing 1 mM IPTG. After incubation at 18 C with shaking at 300 RPM for 24 hours, cells were pelleted and lysed with BugBuster (Novogen).

His-tagged BglB proteins were purified via immobilized metal ion affinity chromatography using 50 µL bed volume of Ni-NTA resin (Thermo) and eluted in 300 µL assay buffer (50 mM HEPES, 150 mM sodium chloride, 25 mM EDTA, pH 7.50). Protein expression was assessed using SDS-PAGE (4-12% gradient gels from Life Technologies).

## Thermal stability assay and data analysis

Triplicate aliquots of mutant proteins in assay buffer at concentrations ranging from 0.01 to 0.3 mg/mL (10x diluted from eluate) were incubated at 8 temperatures in evenly-spaced increments between at 30 C and 50 C for 30 minutes in a thermal cycler (BioRad). After incubation, 100 mM pNPG in assay buffer was added, and the rate of pNP production at each temperature was determined by linear fit to data taken at 1 min intervals over 1 hour.  

For each BglB variant, triplicate rates at 8 temperatures were normalized to the [0,1] interval and fit to the logistic equation using least squares (SciPy) to determine the parameters Tm (midpoint) and k (kurtosis).

## Computational modeling and machine learning

One hundred molecular models of each mutant enzyme were generated using the Rosetta Molecular Modeling Suite by Monte Carlo optimization of total system energy and the lowest 10 of total system energy were selected for feature generation. A total of 50 features were calculated for each protein model [which ones?].

The features were used to train a SVM classifier. We assessed model performance using 10-fold cross-validation. First we performed 10-fold cross-validation (CV) and evaluated the predicted performance on the left-out samples (generalization error) at each of the 10 runs. Then we repeated this procedure 1,000 times to randomize the sample distribution among the folds. That way, we reduce the effect of any bias for evaluating left-out prediction performance. More information about the optimization and statistical procedure followed is available [Supp].

# Results

A total of 128 proteins, not including batched replicates of wild type BglB produced with each batch, were produced, purified, and characterized in this study. Of 128 proteins synthesized and assayed, 86 (67%) express and purify as soluble protein. The remaining 42 mutants did not appear on a gel after at least 2 independent production attempts.

Of the 86 solubly-expressed mutants, melting temperature for 62 was determined by fitting rate data collected at 8 temperatures from 30 to 50 C to the logistic equation. Data from the remaining 24 mutants that expressed as soluble protein could not be used to determine Tm because the kinetic constants for these mutants are below our limit of detection.

The wild type BglB 8 replicates had an average melting temperature of 39.6 C across assay data from 8 biological replicates. In the data set reported here, representing Tm for 62 mutants, the average melting temperature was 39.0±1.7 C, with a range of 32.9 C to 45.3 C. Of 62 mutants for which Tm was determined, Tm for 37 of them falls within 1 degree C of the wild type Tm (58%). Of the remaining 49 Tm values, 18 exhibited a lower melting temperature than that of native BglB and 7 displayed a higher melting temperature. The hottest Tm observed in this data set is N404C, which increased the Tm of BglB to 45.3 C (dTm=+5.4 ˚C). The mutation that decreased the thermal stability of BglB the most was H178A (dTm=-7.0 ˚C).

In addition to expression and thermal stability data, we also report kinetic constants for 12 mutants whose kinetic constants had not previously been determined \cite{26815142}. Together, data for soluble expression, kinetic constants (kcat, km, kcat/km), and melting temperature are reported for 128 mutants of BglB (Supporting Information). **Figure 2** depicts the data set as a heat map, with values relative to native BglB.

![](figure_2.png)

**Figure 2: heatmap depiction of the entire dataset**. Depiction of expression, Tm, KM, kcat, kcat/KM and conservation for each of the 128 mutants used in this study. For Tm, red boxes indicate a higher Tm, and blue boxes indicate a lower Tm (see legend). For expression, a black box indicates soluble expression, and a white box indicates no expression for this mutant. For kcat, KM, and kcat/km, a diverging colormap is used, with purple values indicating lower values, and green indicating higher values.

## Sequence-stability relationships in BglB

A novel finding was a nearly six degree increase in melting temperature by single point mutant N404C. The BglB crystal structure reveals a weak hydrogen bond between N404 and the backbone of a L402. Molecular modeling of N404C predicts the loss of this hydrogen bond to the protein's alpha helix, in which the protein is allowed to repack into more energetically favorable states.

Similarly, the point mutation W120F resulted in a delta Tm of +1.6 C. The BglB crystal structure indicates a weak hydrogen bond between W120 and the backbone of N163, which could be construed as an unsatisfied polar interaction. The mutation to Phe maintains the structural integrity at the mutation site as well as removes the unsatisfied hydrogen bond donor to the neighboring alpha helix. The increased stability is then due to destabilization of the unfolded state, which exposes a hydrophobic Phe to bulk solvent. It is also worth noting that the mutant W120A results in no soluble protein production after 3 independent attempts, indicating that W120 plays a key role in stabilizing the protein. Previous studies have shown a similar increase in stability upon Trp to Phe point mutations \cite{12600203}. Analysis of a multiple sequence alignemnt of 5,000 proteins from the Pfam database reveals approximately equal probablity of finding Trp, Phe, or Tyr here, and less than 1% representation of all of the other amino acids combined. Thus, the experimental measurements and the evolutionary record agree that W120 plays a key role in stabilizing BglB. No major structural changes are predicted via Rosetta modeling.  

Additionally, we have additional information about R240. The mutation R240E, which plates a glutamate near the existing glumatate at E222 that forms two hydrogen bonds to R240. The substittuion R240E, which plates two negativly-charged residues in close proximity, results in no soluble protein under our experimental conditions after at least 2 repeated attempts to produce and purify the protein (one of many mutants done this way), providing evidence for the belief that the mutation R240E is massively destabilitizing. Whereas Rosetta modeling predicts no change in deltaG (within 1 REU) for this mutation, and example of a mutation that would have been missed using Rosetta to scan for mutations. However, FoldX assigns a ddG of 3.78, (compare to its score for R240A, which is 1.71) highlighting the importance of a diverse set of estimates chosen by machine learning on experimental data to train algorithms. Of course, it’s unclear then why mutation R240D, which places a carboxylate only 1.54 A further away, would then result in a soluble protein.

Point mutation E222H had a melting temperature of 34.7 C, a nearly five degree decrease than that of native BglB. Previous studies show strong hydrogen bond interaction, 2.6 and 3.1 Å, between E222 and its neighboring R240 residue (Carlin 2016). The introduction of histidine at the mutation site causes the loss of these strong hydrogen bonds as well as the creation of electrostatic repulsion between the partially positively charged and positively charged amino acids. The cumulative effect of this mutation results in the protein's decreased stability at lower temperatures.

Mutants that did not express followed rules broadly consistant with previous work and sequence conservation, such as the large destabilizing effect of any substitation W407X and XXX. Other mutants that did not express mostly followed well-established observations of destabilizing effects, such as the introduction of proline into an alpha helix (Y166P, Q19P), the mutation of topology-defining/helix-ending proline residues (P329N), mutations to and from glycine (), the introduction of charged residues into the hydrophobic core (A236E, F72H), and extreme small-to-large mutations (A227W).

It is interesting to note that all the mutations we made in our study to the catalyic nucelophile (E353) and acid-base (E164) polar residues resulted in soluble protein, consistent with the idea that enzymes must trade structural stability for function in placing these two negatively-charged groups less than 5 Å apart (the sole exception, E164G, could be the result of an altered folding trajectory due to the conformational freedom of glycine). Notable is that all the catalytic knockouts, E164A, E164R, E353A, Y295A, Y295G, except for E164G, where a glycine is intersted in an alpha helix, result in protein that is solubly expressed in our system, supporting the belief that these mutations are beneficial to protein stability as detremental as they are to enzyme function. It would be interesting to think of high-throughput ways to measure enyme stability for mutants such as these whose Tm cannot be captured by enzyme assay because they exhibit catalytic rates below the limit of detection of those assays.

![](figure_3.img)

**Figure 3**: Topmost panel: sequence logo of the local area of the residue of interest. Bottom panels: top subpanel: the native protein structure. Bottom subpanel: a Rosetta model of the mutant structure. From left to right, mutants N404C) which increased Tm by X degrees; W120F) which increased melting temperature X degrees; Q19S) which X; and E222H) where an unfavorable Coliumbic interaction leads to a delta-Tm of -5.2 deg C.


## Generation of Rosetta structural features from molecular models and machine learning

The Rosetta Molecular Modeling suite was used (code in Supplemental) to generate 100 molecular models of each mutant protein. The lowest 10 models based on total system energy score were used to calculate a set of 50 structural features, and these features were averaged to give 50 features per mutant protein. The 50 features were normalized by subtracting the mean and dividing by the variance.

Protein expression based on SDS-PAGE was assessed (2 biological replicates per protein sample) and a 0 was assigned to proteins that did not express solubly, and a 1 was assigned to expressed proteins. A classifier based on support vector machines (SVM classifier) was trained on the features for the mutants with experimental data (scikit-learn). We used 10-fold cross validation repeated 1000 times with the results averaged over the 1000 trials. Figure 4 shows the receiver operating characteristic (ROC) curve for the cross-validated predictions.

# Discussion (needs a complete rewrite)

## Summary of our findings

Here, we report the thermal stability and soluble protein expression for 120 mutants of BglB. This data set was enabled by the use of high-throughout roboticly automated molecular biology tools for site-directed mutagenesis as well as open-sourced laboratory protocols. We described the use of this data set to train machine learning algorithms to develop a classifier that was able to predict the soluble protein expression with an accuracy of X, and the thermal melting temperature with a PCC of X.

Tradiitonally, [cite] studies of this type have sought to design more thermostable mutants. However, we are interested more in less thermostable mutants in the context of human disease. Since it is accepted that a number of human diseases are caused by defects in particular enzymes of metabolism, It would be interesting to investigate whether the opposite is true: whether mutations that increase turnover number or decrease dissociation constants also result in diseases. Perhaps diseases of excess are as common as diseases where a defective enzyme is to blame.

In any case, our previous work sampled functional space in a way that captured almost entirely constants of lower magnitude than the natural sequence chosen as our baseline (it cannot be helped to think that if we had instead begun with a mutant of approximately half the kcat of the WT, we should have been able to see many mutations that increase the kcat). However, in the set of protein melting temperatures reported here, 25 mutants have a Tm that is greater than WT (39.6 C), while 32 have a Tm that is lower (0.78:1 ratio).

![](figure_4.png)

**Figure 4: statistical independence of protein melting temperature (Tm) and kinetic constants.** Plots of Tm versus kinetic constant for each of kcat, KM, and kcat/km. Tm values are on a linear scale (C) and kinetic constant values are on a log scale.

## Implications of our findings to biotechnology

In biotechnology applications, it is enough to generate hypotheses with a distrubution around the correct mutaion, as long as these mutations are accurate enough so that they are better than random. - in biotechnology, it is OK to have mild predictive power, as large numbers of mutations are tried. Still, the best we can do is better than current approaches X, Y, and Z. Describe how what we did is better.

## Implications of our findings to human health

In the prediction of disease state from genomic sequcne, of relevance to human health, it is advisable to have the fewest number of false positives, which create unnecessary  cost and scare patients, as well as low false negatives, which result in important diagnose to be missed. Unfortunately, our current approach falls short, but we propose that this approch could be expanded in the future for more accurate predictions, through larger data sets. And improved predictive modeling.

---

BibTex biblio:

@article{21710487,
  title = {{High-throughput measurement, correlation analysis, and machine-learning predictions for pH and thermal stabilities of Pfizer-generated antibodies.}},
  date = {2011 Sep},
  source = {Protein Sci},
  authors = {King, AC and Woods, M and Liu, W and Lu, Z and Gill, D and Krebs, MR},
  author = {King, AC and Woods, M and Liu, W and Lu, Z and Gill, D and Krebs, MR},
  year = {2011},
  month = {Sep},
  journal = {Protein Sci},
  volume = {20},
  number = {},
  pages = {1546-57},
  pubmed_id = {21710487},
}


@article{18632749,
  title = {{Accurate prediction of stability changes in protein mutants by combining machine learning with structure based computational mutagenesis.}},
  date = {2008 Sep 15},
  source = {Bioinformatics},
  authors = {Masso, M and Vaisman, II},
  author = {Masso, M and Vaisman, II},
  year = {2008},
  month = {Sep},
  journal = {Bioinformatics},
  volume = {24},
  number = {},
  pages = {2002-9},
  pubmed_id = {18632749},
}


@article{14681373,
  title = {{ProTherm, version 4.0: thermodynamic database for proteins and mutants.}},
  date = {2004 Jan 1},
  source = {Nucleic Acids Res},
  authors = {Bava, KA and Gromiha, MM and Uedaira, H and Kitajima, K and Sarai, A},
  author = {Bava, KA and Gromiha, MM and Uedaira, H and Kitajima, K and Sarai, A},
  year = {2004},
  month = {Jan},
  journal = {Nucleic Acids Res},
  volume = {32},
  number = {},
  pages = {D120-1},
  pubmed_id = {14681373},
}


@article{26815142,
  title = {{Kinetic Characterization of 100 Glycoside Hydrolase Mutants Enables the Discovery of Structural Features Correlated with Kinetic Constants.}},
  date = {2016},
  source = {PLoS One},
  authors = {Carlin, DA and Caster, RW and Wang, X and Betzenderfer, SA and Chen, CX and Duong, VM and Ryklansky, CV and Alpekin, A and Beaumont, N and Kapoor, H and Kim, N and Mohabbot, H and Pang, B and Teel, R and Whithaus, L and Tagkopoulos, I and Siegel, JB},
  author = {Carlin, DA and Caster, RW and Wang, X and Betzenderfer, SA and Chen, CX and Duong, VM and Ryklansky, CV and Alpekin, A and Beaumont, N and Kapoor, H and Kim, N and Mohabbot, H and Pang, B and Teel, R and Whithaus, L and Tagkopoulos, I and Siegel, JB},
  year = {2016},
  month = {},
  journal = {PLoS One},
  volume = {11},
  number = {},
  pages = {e0147596},
  pubmed_id = {26815142},
}


@article{22575958,
  title = {{Engineering the third wave of biocatalysis.}},
  date = {2012 May 9},
  source = {Nature},
  authors = {Bornscheuer, UT and Huisman, GW and Kazlauskas, RJ and Lutz, S and Moore, JC and Robins, K},
  author = {Bornscheuer, UT and Huisman, GW and Kazlauskas, RJ and Lutz, S and Moore, JC and Robins, K},
  year = {2012},
  month = {May},
  journal = {Nature},
  volume = {485},
  number = {},
  pages = {185-94},
  pubmed_id = {22575958},
}


@article{12600203,
  title = {{Energetic and structural analysis of the role of tryptophan 59 in FKBP12.}},
  date = {2003 Mar 4},
  source = {Biochemistry},
  authors = {Fulton, KF and Jackson, SE and Buckle, AM},
  author = {Fulton, KF and Jackson, SE and Buckle, AM},
  year = {2003},
  month = {Mar},
  journal = {Biochemistry},
  volume = {42},
  number = {},
  pages = {2364-72},
  pubmed_id = {12600203},
}