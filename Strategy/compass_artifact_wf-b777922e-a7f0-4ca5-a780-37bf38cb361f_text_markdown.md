# Unified Fingerprint + Iris Multimodal Biometric Datasets: A Research-Project Survey

## TL;DR

- **SDUMLA-HMT (Shandong University, 2011) is the most widely-used, free, publicly available "homologous" (same-subject) database that contains BOTH real fingerprint and real iris data from the same 106 individuals — and it is the de-facto choice in 2020–2025 literature for fingerprint+iris feature-level fusion experiments such as the PCA + PSO-SVM (RBF) pipeline you describe.** Other true unified options (WVU BIOMDATA, BioSecure BMDB-DS2, BIOSEC, BiosecurID, Children Multimodal Biometric Database, NIST SD 301) exist but require institutional license agreements and/or are partially restricted.
- **The "Virtual Multimodal Database" (VMD) approach — pairing CASIA-Iris with FVC fingerprints to create chimeric/virtual subjects — is widely used in the literature but is methodologically controversial.** It rests on a strong (and increasingly challenged) assumption of statistical independence between modalities, and reviewers in top-tier biometrics venues now expect either (a) corroboration on a real homologous dataset like SDUMLA-HMT or (b) a principled chimera-construction protocol (e.g., Doddington-Zoo-based).
- **For a feature-concatenation → PCA → PSO-tuned RBF-SVM pipeline, the recommended primary dataset is SDUMLA-HMT, optionally supplemented by a virtual database (CASIA-IrisV4 + FVC2002/2004/2006) for cross-database validation.** This dual-database approach is exactly what reviewers expect in 2024–2025 multimodal biometric papers.

---

## Key Findings

### 1. Unified (same-subject) fingerprint + iris databases that exist and are usable

| Database | Subjects | Fingerprint | Iris | Public / Access | Notes for your project |
|---|---|---|---|---|---|
| **SDUMLA-HMT** (Shandong U., 2011) | 106 (61 M / 45 F, ages 17–31) | 6 fingers × 8 impressions × **5 sensors** (1 swipe, 3 optical, 1 capacitive) | NIR, **5 images per eye × 2 eyes = 10 images/subject (1,060 total)** | **Free** for research/non-commercial via http://mla.sdu.edu.cn/sdumla-hmt.html | The standard choice; native fingerprint+iris+face+finger-vein+gait |
| **WVU BIOMDATA (CITeR), Releases 1 & 2** | ~270 subjects total; **219 have both iris and fingerprint** (Patel et al., ECCV 2012) | Up to 4 fingerprint instances per subject | 2 iris instances per subject | License agreement; e-mail WVUBiometricData@mail.wvu.edu via citer.clarkson.edu/research-resources/biometric-dataset-collections-2/ | Real challenging-quality data (sensor noise, blur, occlusion); requires application |
| **BioSecure Multimodal Database (BMDB) — Dataset 2 ("DS2 / Desktop")** | ~667 of the ~1,000 subjects in DS2 contain iris + fingerprint together (DS2 is the only subset with iris) | 2 sensors (optical + thermal sweep), 2 sessions | Iris (one sensor), 2 sessions | License via BioSecure Association / Télécom SudParis (biosecure.wp.imtbs-tsp.eu) | Largest real cohort with iris+fingerprint; somewhat hard to obtain today |
| **BiosecurID** (Spain, 2010) | 400 | 2 sensors (optical + sweeping thermal), 4 sessions | Iris sensor, 4 sessions | License via UAM/ATVS group | Strong unified dataset; active maintenance |
| **BIOSEC baseline corpus** (FP6 EU project) | 200 (baseline) / 250 (extended) | 3 sensors | Iris sensor | License via UAM/ATVS | Predecessor of BiosecurID/BMDB |
| **Children Multimodal Biometric Database (CMBD)** (IIT-D / WVU, Yadav et al., IJCB 2017) | 106 children, ages 18 mo – 4 yr, 2 sessions | Cross-Match L-scan slap | Cross-Match iris scanner | License via databases@iab-rubric.org (iab-rubric.org/index.php/wvu) | Published as iris+fingerprint only (face withheld); ideal if your population is children |
| **NIST Special Database 301 (SD 301)** | Multi-hundred (numbers vary by partition) | Multiple FP sensors | Iris | Free download from NIST | First NIST multimodal release with FP + face + iris; extracted from IARPA Nail-to-Nail collection (2019) |
| **MBioID** (FP6) | ~120 | Fingerprint | Iris | Limited availability | Designed for ID-document studies (face + 3D-face + FP + iris + signature + speech) |
| **MyIDEA** | ~70 | Fingerprint | Iris | Restricted | Older European multimodal effort |

**Datasets that are sometimes mentioned but do NOT contain both fingerprint and iris from the same subjects:** MCYT (FP + signature only), XM2VTS (face/voice only), MOBIO (face/voice only), IV² (iris + face/3D, no FP), D4FLY (3D face + iris + somatotype, no FP), MobiBits (face/voice/hand/signature, no FP+iris pairing), FYO (vein only).

### 2. Is SDUMLA-HMT publicly available with both fingerprint and iris?

**Yes.** SDUMLA-HMT (Yin, Liu & Sun, *CCBR 2011*, LNCS 7098, pp. 260–268) is a **homologous** (true same-subject) multimodal database released by the Machine Learning and Applications group at Shandong University. It is downloadable free of charge after a simple license acknowledgment for research and non-commercial use only. Commercial redistribution is prohibited. The official landing page is http://mla.sdu.edu.cn/sdumla-hmt.html (mirrored at https://time.sdu.edu.cn/kycg/gksjk.htm). Both the iris subset (1,060 NIR images, 5 per eye for 106 subjects, captured with an intelligent iris device built by USTC, capture distance 6–32 cm) and the fingerprint subset (6 fingers × 8 impressions × 5 sensors per subject — including a swipe scanner, three optical scanners, and one capacitive scanner; images stored as BMP) are part of the same release and can be associated by the subject ID. This makes SDUMLA-HMT the natural primary dataset for a fingerprint+iris feature-concatenation → PCA → PSO-SVM(RBF) study.

### 3. Virtual Multimodal Database (VMD) / "chimeric" approach

**What it is.** Because true multimodal datasets are scarce, researchers commonly create *chimeric* or *virtual* subjects by randomly pairing the *i*-th fingerprint subject in a fingerprint-only database (e.g., FVC2002, FVC2004, FVC2006, CASIA-FingerprintV5) with the *i*-th iris subject from an iris-only database (e.g., CASIA-IrisV1/V2/V3/V4, IITD Iris, UBIRIS, UPOL). The justification offered in the literature is that the two traits are assumed statistically independent given identity, so any pairing is as valid as any other.

**Is it scientifically accepted?** Conditionally — and increasingly less so.

- **Pro-acceptance literature.** Chimeric pairings have been used since at least the 2003 Workshop on Multimodal User Authentication and remain common (e.g., Benaliouche & Touahria 2014 on CASIA-IrisV1/V2 + FVC2004; Radha & Kavitha 2012; Abdolahi et al. 2013; Jagadeesan et al.; many MDPI/Hindawi papers 2014–2023).
- **The seminal critique.** Poh & Bengio, "Can Chimeric Persons Be Used in Multimodal Biometric Authentication Experiments?" (*ICB / AVBPA 2006*, Springer LNCS 3546, pp. 88–94), formally tested the independence assumption and concluded that for many experiments the practice is *questionable*; performance variability on chimeric users can differ meaningfully from that on real bimodal users.
- **Subsequent refinements.** A "cluster-based chimeric" protocol that preserves the dependency structure (Khoury et al., "A new protocol for multi-biometric systems' evaluation maintaining the dependencies between biometric scores") and the Doddington-Zoo-based chimerical protocol of Pinto, Pedrini, Schwartz et al. (Sensors 2019, 19(13):2968) are now considered best practice when chimeras are unavoidable.
- **Recent empirical evidence against pure independence.** Guo et al. (2024) showed statistically significant intra-subject patterns across different fingerprints of the same person, and So, Lis, Goldfeder & Lipson, "Bi-Encoder Contrastive Learning for Fingerprint and Iris Biometrics" (arXiv:2510.22937, 2025), trained on 274 WVU subjects with paired FP+iris and reported that left/right irises of the same person are correlated and that there is even slight cross-modal (FP↔iris) signal — directly undermining the strong independence assumption.
- **Practical reviewer expectation (2023–2025).** Reviewers in IEEE TBIOM, PR, IJCB, and Sensors generally accept VMD/chimeric experiments **only** as a *secondary* sanity check or for scaling-up experiments, and require the *primary* results to be on a true homologous dataset (SDUMLA-HMT, BMDB, WVU BIOMDATA, BiosecurID, etc.).

**Bottom line for your project:** Using CASIA-IrisV4 (54,607 images / >1,800 genuine subjects, 6 subsets; free download from CBSR/BIT) paired with FVC2004/FVC2006/FVC2002 is acceptable as a *supplementary* experiment but should not be your only evaluation.

### 4. Recommended fingerprint + iris datasets in recent (2020–2025) literature

The dominant choice in current literature is **SDUMLA-HMT**, frequently augmented with chimeric pairings:

- Vyas, Gupta & Pal, "Iris-Fingerprint multimodal biometric system based on optimal feature level fusion model," *AIMS Electronic & Electrical Eng.* 5(1), 2021, doi:10.3934/electreng.2021013 — uses left/right iris + both thumb fingerprints from **SDUMLA-HMT**, CCA-based feature fusion.
- Vyas et al., "Feature level fusion framework for multimodal biometric system based on CCA with SVM classifier and cosine similarity measure," *Australian J. Electrical & Electronics Eng.* 20(2), 2022, doi:10.1080/1448837X.2022.2129147 — **SDUMLA-HMT iris + fingerprint** with SVM classifier (very close in spirit to your pipeline).
- Sujatha, Sundar, Deivendran & Indumathi, "Multimodal Biometric Algorithm Using IRIS, Finger Vein, Finger Print with Hybrid GA, PSO for Authentication," *Lecture Notes on Data Eng. & Comm. Tech.* vol. 54, Springer 2021, doi:10.1007/978-981-15-8335-3_22 — **SDUMLA-HMT**; uses **GA + PSO** for parameter optimization (the closest published method to your PSO-SVM proposal).
- Soleymani, Dabouei, Kazemi, Dawson, Nasrabadi (WVU group), 2020 onwards — multimodal CNN fusing iris+face+fingerprint on **BIOMDATA / WVU**.
- Alay & Al-Baity, "Deep Learning Approach for Multimodal Biometric Recognition System Based on Fusion of Iris, Face, and Finger Vein Traits," *Sensors* 20(19):5523, 2020 — **SDUMLA-HMT**, feature- and score-level fusion, accuracy 99.39 % / 100 %.
- Ammour et al., "Biometric template protection based on a cancelable convolutional neural network over iris and fingerprint," *Biomedical Signal Processing & Control*, 2024 — uses **CMBD + CASIA-Iris V3 + FVC 2002 DB2** (a hybrid real/chimeric protocol) reporting EERs of 0.073 % and 0.038 %.
- Singh & Kant, "Optimized hybrid SVM-RF multi-biometric framework for enhanced authentication using fingerprint, iris, and face recognition," *PeerJ Computer Science* 11:e2699, 2025 — SVM + RF with BFO/GA optimization, fingerprint+iris+face.
- "A Deep Learning-Based Multimodal Biometric Authentication Framework Using Fingerprint and Iris with Score-Level Fusion," *Ingénierie des Systèmes d'Information* 30(12), 2025, doi:10.18280/isi.301214.
- "Multimodal Biometric System Fusion Using Fingerprint and Iris with Convolutional Neural Network," *Engineering and Technology Journal* 9(9), 2024 (Everant) — fingerprint + iris CNN fusion.
- "Multimodal Biometric Revolution: VGG-16 and VGG-19 for Masked Face, Fingerprint and Iris Recognition," *Revue IRS*, 2024 — uses **FVC2002 + UBIRIS.v2 + Masked Face-Net** (chimeric).
- Yuvasri, Soundarya Devi, Alwin Infant & Jainish, "Multi-Modal Biometric Authentication System using Hybrid CNN based on Face, Finger Vein and Iris Fusion," *ICMCSI 2025*, pp. 1071–1077.

### 5. Pros and cons: unified vs. virtual multimodal database

**Unified / homologous dataset (e.g., SDUMLA-HMT, BIOMDATA, BMDB)**

*Pros*
- Captures any real intra-subject statistical dependency between modalities (now proven non-zero by So et al. 2025 and Guo et al. 2024).
- Reflects the same population, demographics, and acquisition conditions for both modalities.
- Permits genuine cross-modality quality analysis (e.g., a subject with poor fingerprints may also have poor iris due to age/cataract).
- Required by reviewers as the primary evaluation set in top-tier venues.
- Allows session/time-based protocol design (e.g., enroll session 1, test session 2).

*Cons*
- Small (SDUMLA-HMT only 106 subjects; BMDB-DS2 ~667; BIOMDATA fingerprint+iris subset 219).
- Often requires a license agreement (BMDB, BIOMDATA, BiosecurID, CMBD).
- Limited demographic diversity (SDUMLA-HMT subjects are 17–31 y/o Chinese students).
- Single iris sensor in SDUMLA-HMT — no cross-sensor iris generalization study possible.
- Some unified datasets (SDUMLA-HMT) are single-session, preventing studies of temporal robustness.

**Virtual / chimeric / VMD (e.g., CASIA-IrisV4 + FVC2004)**

*Pros*
- Effectively unlimited "subjects" via combinatorial pairing (CASIA-IrisV4 alone has 1,800+ genuine + 1,000 virtual subjects; FVC databases give thousands of fingers).
- Both source databases are free and easy to download (no IRB/license bottleneck).
- Lets you stress-test scalability and class-balance.
- Useful when evaluating cancelable templates or template-protection schemes that don't need true intra-subject correlation.

*Cons*
- Implicitly assumes complete statistical independence between FP and iris — an assumption that is empirically wrong (left/right iris correlated; cross-FP/iris weak signal exists; Guo 2024, So 2025).
- Pairing is non-unique: 100 different random pairings may give 100 different EERs, making results irreproducible unless the seed/protocol is published.
- Cannot capture realistic correlated nuisance factors (age-related skin moisture affecting both FP quality and accommodation; ethnic distribution; environment).
- Modern reviewers often demand confirmation on a real homologous dataset; chimeric-only evaluations are increasingly returned with major revisions.
- Does not align FP and iris sensor demographics — a CASIA Asian-Chinese iris cohort paired with European-FVC2002 fingers introduces unintentional confounding.

**Recommended hybrid strategy for your study (PCA + PSO-RBF-SVM, feature concatenation):**

1. *Primary evaluation* — **SDUMLA-HMT**, choosing a fixed protocol (e.g., right thumb optical fingerprint + left iris, 5 train / 3 test for FP, 3 train / 2 test for iris per subject; report 5- or 10-fold CV).
2. *Scalability / sanity check* — A chimeric VMD built from **CASIA-IrisV4 (Interval or Thousand subset) + FVC2004 DB1_A or FVC2006 DB2_A**, with seeded pairing and a published random seed for reproducibility.
3. *Optional* — Apply for **WVU BIOMDATA** (Crihalmeanu et al., WVU Lane Dept Tech Report 2007) for an independent test set of 219 paired subjects. This is the test set used by Patel, Haghighat & Aghagolzadeh in their Discriminant Correlation Analysis ICASSP 2016 paper.
4. *Cite your dataset choices to* Yin, Liu & Sun (2011) for SDUMLA-HMT; Ortega-Garcia et al., *IEEE TPAMI* 32(6), 2010, pp. 1097–1111 for BMDB; Fierrez et al., *Annals of Telecommunications*, 2010 for BiosecurID; CASIA Center for Biometrics & Security Research for CASIA-IrisV4; Maio, Maltoni, Cappelli, Wayman & Jain for FVC2004/2006; Poh & Bengio (2006) when justifying or critiquing chimeric data; and Pinto et al. *Sensors* 19(13):2968, 2019 if you adopt a Doddington-Zoo chimeric protocol.

---

## Details

### SDUMLA-HMT — full specification (most relevant to your project)

- **Reference:** Yilong Yin, Lili Liu, Xiwei Sun, "SDUMLA-HMT: A Multimodal Biometric Database," *6th Chinese Conference on Biometric Recognition (CCBR 2011)*, LNCS vol. 7098, Springer, pp. 260–268, 2011. DOI: 10.1007/978-3-642-25449-9_33.
- **Access URL:** http://mla.sdu.edu.cn/sdumla-hmt.html (Machine Learning and Data Mining Lab, Shandong University). Alternative landing: https://time.sdu.edu.cn/kycg/gksjk.htm. Catalogued by NIST at https://tsapps.nist.gov/BDbC/Search/Details/420.
- **License:** Free for academic / non-commercial research; user must cite the CCBR 2011 paper. Commercial redistribution prohibited.
- **Population:** 106 subjects — 61 male / 45 female; ages 17–31; predominantly Chinese.
- **Iris subset:** 1,060 grayscale NIR images = 106 subjects × 2 eyes × 5 images. Captured by an "intelligent iris capture device" developed by University of Science and Technology of China; capture distance 6–32 cm.
- **Fingerprint subset:** 6 fingers (left thumb, left index, left middle, right thumb, right index, right middle) × 8 impressions × 5 sensors per subject. The 5 sensors comprise 1 swipe scanner, 3 optical scanners, and 1 capacitive scanner. Files are named `fingeridx_n.bmp` where idx ∈ {1..6}, n ∈ {1..8}, stored as BMP.
- **Other modalities (optional for ablation studies):** face (7 view angles, 8,904 images), finger vein (3,816 images, Wuhan Univ. device), gait (6,996 videos at 6 view angles).
- **Recommended split for your PSO-SVM(RBF) study:** Per common SDUMLA practice (e.g., Vyas 2021, Alay & Al-Baity 2020) — 60/20/20 train/val/test split or 5-fold cross-validation, balanced across 106 classes. For feature concatenation: extract iris features (e.g., 1D Log-Gabor → bitwise template, or CNN embedding), extract fingerprint features (Gabor / minutiae-cylinder-code / CNN), concatenate, run PCA to retain 95–98 % variance, then PSO-tune (C, γ) of an RBF SVM using 5-fold CV inside training.

### CASIA-Iris V4 (for the virtual database)

- 54,607 images, > 1,800 genuine subjects + 1,000 synthetic.
- Six subsets: Interval (~395 subjects, 2,639 images, NIR close-up, very clean), Lamp, Twins, Distance, Thousand (1,000 subjects, 20,000 images), Syn (synthetic).
- Free upon agreement at http://www.cbsr.ia.ac.cn/english/IrisDatabase.asp / http://english.ia.cas.cn/db/201610/t20161026_169399.html.

### FVC fingerprint databases (for the virtual database)

- FVC2002 / FVC2004 / FVC2006 — each has 4 sub-databases (DB1–DB4), 100 subjects × 8 impressions in the "A" set, 10 subjects × 2 in the "B" set. Free for research at the BioLab Bologna / FVC-onGoing site.
- For a 1:1 pairing with CASIA-Iris-Interval (≈395 subjects), CASIA-Iris-Thousand allows a much larger virtual cohort (1,000 subjects) — researchers commonly subsample to match the 100-subject FVC "A" set or mix multiple FVC editions.

### WVU BIOMDATA (CITeR)

- Crihalmeanu, Ross, Schuckers & Hornak, "A Centralized Web-Enabled Multimodal Biometric Database," *Biometric Consortium Conference 2004*; technical report 2007.
- Six modalities (iris, face, voice, fingerprint, hand geometry, palmprint) in Release 1; in Release 2 face video and voice are added.
- Of the full subject pool, **219 subjects have both iris and fingerprint** (per Patel et al., "Joint Sparsity-Based Robust Multimodal Biometrics Recognition," ECCV 2012); each subject contributes 2 iris instances and 4 fingerprint instances.
- Access via license: WVUBiometricData@mail.wvu.edu (https://citer.clarkson.edu/research-resources/biometric-dataset-collections-2/multimodal-biometric-dataset-collection-biomdata-release-2/).
- A larger de-identified WVU/Clarkson cohort with 274 subjects (~100 k FP, ~7 k iris) was used by So et al. (arXiv 2510.22937, 2025).

### BioSecure Multimodal Database (BMDB)

- Ortega-Garcia et al., "The Multiscenario Multienvironment BioSecure Multimodal Database (BMDB)," *IEEE TPAMI* 32(6):1097–1111, 2010.
- Three datasets: DS1 (Internet — voice + face only), **DS2 (Desktop — voice, FP × 2 sensors, face still + talking, iris, signature, hand)**, DS3 (Mobile — signature, FP, voice, face).
- DS2 is the **only** dataset with paired fingerprint + iris; ~667 subjects in DS2; 2 sessions one month apart.
- Acquired by 11 European institutions; access via BioSecure Association (https://biosecure.wp.imtbs-tsp.eu/biosecure-database/). Modern obtain-ability is uneven; license fees may apply.

### BiosecurID

- Fierrez, Galbally et al., "BiosecurID: a multimodal biometric database," *Annals of Telecommunications* (preprint arXiv:2111.03472).
- 400 subjects, 4 sessions, includes fingerprint (2 sensors: optical 569 dpi + thermal sweep 500 dpi), iris (CCD with infrared illumination), face, signature, handwriting, hand, keystroking, speech.
- Designed with cross-compatibility with BIOSEC and BIOSECURE so a combined ~650-subject multimodal pool can be built.
- License via UAM/ATVS (Madrid).

### Children Multimodal Biometric Database (CMBD)

- Basak, De, Agarwal, Malhotra, Singh & Vatsa, "Multimodal Biometric Recognition for Toddlers and Pre-School Children," *IJCB 2017*.
- 106 children (18 mo – 4 yr), 2 sessions, iris + fingerprint released (face withheld).
- Access: databases@iab-rubric.org (https://iab-rubric.org/index.php/wvu).

### NIST Special Database 301 (SD 301)

- Released December 2019 alongside SD 300 and SD 302. SD 301 is NIST's first multimodal biometric dataset — fingerprint + face + iris, partially derived from the IARPA Nail-to-Nail Fingerprint Challenge.
- Free download from NIST (search "NIST Special Database 301").
- Useful as a U.S.-population complement to SDUMLA-HMT.

### Recent (2020–2025) iris+fingerprint works that mirror your pipeline

- Vyas, Gupta & Pal (2021, 2022): SDUMLA-HMT, CCA feature fusion + SVM, EER reduction vs. unimodal/score-level fusion. Closest published analogue to your concatenation+SVM idea.
- Sujatha et al. (Springer LNDECT-54, 2021): SDUMLA-HMT, hybrid GA + PSO, score-level normalization — the only published work I located that uses **PSO** on SDUMLA-HMT for iris+FP+finger-vein.
- Ammour et al. (Biomedical Signal Processing & Control 2024): cancelable CNN over iris+FP, EER 0.038 %, on CMBD/CASIA-IrisV3/FVC2002 DB2.
- Singh & Kant, "Optimized hybrid SVM-RF multi-biometric framework," *PeerJ CS* 11:e2699, 2025 — SVM (RBF), Random Forest, BFO + GA, Gabor features, FP + iris + face. Clear precedent for SVM(RBF) + meta-heuristic optimization on this task.
- Soleymani et al. (WVU): multimodal CNN with multi-abstract / weighted feature fusion on **WVU BIOMDATA**.
- "Latent fingerprint and iris biometric fusion using product / sum rule," *IRJSE* 2024.
- Yuvasri et al., ICMCSI 2025: hybrid CNN on iris + finger-vein + face.
- So, Lis, Goldfeder & Lipson, "Bi-Encoder Contrastive Learning for Fingerprint and Iris Biometrics," arXiv:2510.22937, 2025 — uses 274 paired WVU subjects to challenge the independence assumption.

---

## Caveats

- The SDU lab page (mla.sdu.edu.cn) sometimes blocks robotic fetches; you must email the maintainers (yinyl@sdu.edu.cn historically) and supply a brief description and signed undertaking. This is the most common path actually used in 2024–2025 papers.
- A few publications loosely (and incorrectly) describe SDUMLA-HMT as a "chimeric" database (e.g., the Sujatha et al. 2021 chapter). It is NOT — it is a homologous, real, same-subject database. This terminology slip is a known issue in the literature; do not propagate it.
- BIOMDATA and BMDB access has become somewhat slower in 2023–2025 because of GDPR and CITeR-membership policy updates; build at least 6–8 weeks into your timeline if you need them, and be prepared with SDUMLA-HMT as your primary fallback.
- Subject counts in BMDB-DS2 are reported variably across sources (550–712); the canonical Ortega-Garcia 2010 IEEE TPAMI paper states "more than 600 individuals" overall and ~667 in the desktop dataset. Always cite exactly the number you actually obtain after attrition in your own download.
- Iris sensor specifics for SDUMLA-HMT: the database paper credits an "intelligent iris capture device developed by USTC"; it is **not** an OKI IrisPass (despite occasional misattributions). The fingerprint sensors are five but their exact brand/model list is not always quoted consistently across secondary sources — verify against the README distributed with the data.
- The Poh & Bengio (2006) finding that chimeric pairing is "questionable" is moderate, not absolute: for *score-level* fusion of weakly-correlated modalities, results on chimeras and on real bimodal users were *similar in many but not all* trials. The recent ResNet-based evidence (Guo 2024 for FP, So 2025 for iris and FP↔iris) is what has shifted reviewer sentiment more decisively against chimera-only evaluations.
- For a fingerprint+iris **feature-concatenation** pipeline, the curse of dimensionality is severe (a Gabor iris template alone can be 9,600 bits; a fingerprint texture vector can be several hundred dimensions). PCA before SVM is standard; in the SDUMLA-HMT literature, retaining 95–99 % cumulative variance typically reduces dimensionality by 1–2 orders of magnitude with negligible accuracy loss. Confirm by ablation in your own experiments rather than copying values from prior papers — preprocessing pipelines differ.
- Some "VMD" papers do not publish their random pairing seed, making exact replication impossible. If you adopt a virtual database, fix and publish the seed and pairing function (or follow Pinto et al.'s Doddington-Zoo protocol from *Sensors* 19(13):2968, 2019) so reviewers can reproduce your results.
- Recent regulatory note (unrelated to data acquisition but worth flagging): "BIOSECURE" is also the name of a 2024 U.S. legislative act about Chinese biotechnology — searches for "BIOSECURE" can surface unrelated policy results. The biometrics dataset is the BioSecure / BMDB resource by Ortega-Garcia et al.; always include "multimodal database" in queries to disambiguate.