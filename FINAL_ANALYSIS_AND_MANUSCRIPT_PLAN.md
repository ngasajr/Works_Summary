# Final analysis and manuscript plan

> Study edition · 24 November 2026

## Evidence and scope

The source reports 198 main runs, 3 DoRL pipelines and 276 recomputed prediction sets, not 276 independent models. Its conclusion is conditional external-transfer benefit, not universal superiority.

## Comparison checklist

- [ ] Same task/classes, evaluation images and metric. MacroF1 differs from weightedF1/accuracy.
- [ ] Source access: source-accessible versus source-free; no source-onlymethod receives target training images.
- [ ] Target supervision:0classlabels versus100classlabels versus1427additionalsegmentation masks.
- [ ] Unseen external transfer versus unlabeled adaptation to each external test batch.
- [ ] Encoder/pretraining resources:ImageNetR50,CLIP,SAM,StableDiffusion; additional annotation/pretraining exposure.
- [ ] Training steps, sampler, augmentation, checkpoint selection and actual compute. Same nominalbudget is not equalFLOPs; SWAD can stop early.
- [ ] Inference1/5/15views, diffusionnoise trials, and whether parameters/anchors update on the testbatch.
- [ ] Threeindependent trainingseeds versus batch permutations versus deterministic singlefit; aggregate domains withinseed beforeSD.
- [ ] Fidelity:author-codeport versus independentpaper-basedimplementation versus diagnosticextension; deviations explicit.
- [ ] Provenance:retained checkpoint/predictions versus reported primary results without a linked checkpoint.

## Contents

- [1. Recent common-cohort UDA](#1-recent-common-cohort-uda)
- [2. Wen 2025](#2-wen-2025)
- [3. DoRL classifier heads](#3-dorl-classifier-heads)
- [4. CytoDiffusion](#4-cytodiffusion)
- [5. Source-only WBC DG](#5-source-only-wbc-dg)
- [6. Natural-image DG](#6-natural-image-dg)
- [7. Supervised 100-label adaptation](#7-supervised-100-label-adaptation)
- [8. Test-time settings](#8-test-time-settings)
- [9. Historical baselines](#9-historical-baselines)
- [10. Controlled component evidence](#10-controlled-component-evidence)
- [11. Morphology, backbones and cost](#11-morphology-backbones-and-cost)
- [12. Provenance and manuscript action](#12-provenance-and-manuscript-action)

## 1. Recent common-cohort UDA

**Interpretation:** The recent proposed model improves AML macro-F1 by 7.45 percentage points over its source architecture control, but loses 4.17 on Acevedo and 2.79 on Raabin. MIC leads Acevedo, PLUE leads AML, and the source control leads Raabin.

**Study question:** Compare the proposed method against its architecture control before comparing unrelated systems. Why is AML improvement not a universal win?


## 2. Wen 2025

**Interpretation:** Wen full improves over its distillation baseline on Acevedo and Raabin but loses 2.16 points on AML. The proposed UDA model exceeds Wen on Raabin only; target access differs.

**Study question:** Compare Wen full with its own distillation baseline. Which domain loses performance?


## 3. DoRL classifier heads

**Interpretation:** The proposed model exceeds every tested DoRL head in mean macro-F1 across the three domains. ANN is the closest head; AML monocyte and lymphocyte F1 favor ANN. Extra masks and implementation deviations limit attribution.

**Study question:** Compare all five heads, not just RF. Why can accuracy and macro-F1 disagree?


## 4. CytoDiffusion

**Interpretation:** The budgeted source-only CytoDiffusion port has lower mean F1, but resolution, EMA, noise trials and target access differ. No general generative-classifier or efficiency conclusion follows.

**Study question:** Identify the differences in target access and inference budget.


## 5. Source-only WBC DG

**Interpretation:** VL2V-SD leads all three WBC source-only DG means. The proposed variant is only 0.67 points behind on Raabin, but this is not the full UDA method.

**Study question:** Why does the source-only variant not isolate the effect of target access?


## 6. Natural-image DG

**Interpretation:** The proposed source-only variant loses 17.30 accuracy points against plain ERM on OfficeHome. Wen leads the three recovered datasets; VL2V leads the two earlier datasets among tested methods. Missing runs must remain missing.

**Study question:** Compare source validation with held-out accuracy. What additional controls would isolate the cause?


## 7. Supervised 100-label adaptation

**Interpretation:** The color/few-shot system uses 100 labels; the proposed model uses zero. KDE replay improves source retention relative to fine-tuning but reduces target and AML F1.

**Study question:** Why does a shared holdout not make different label budgets equivalent?


## 8. Test-time settings

**Interpretation:** StatA batch adaptation accesses each test domain, unlike unseen external transfer. FOODS/SEC results show that more views do not consistently improve performance.

**Study question:** Distinguish training seeds from stream permutations and test-batch access.


## 9. Historical baselines

**Interpretation:** Historical results have their own protocol. The proposed one-view model improves AML by 6.01 points versus source but loses 3.57 on target.

**Study question:** Why must historical one-view and five-view results remain separate?


## 10. Controlled component evidence

**Interpretation:** Orthogonality has the most consistent removal effect. Independent views and agreement favor external transfer at a target-performance cost. Adaptive weights do not isolate learned policy from heuristic prior.

**Study question:** A positive full-minus-removal difference favors the full configuration. Why are these effects not additive?


## 11. Morphology, backbones and cost

**Interpretation:** Grayscale and tile permutation support spatial discrimination, but domain probe accuracy of 89.17% and CKA of 0.95–0.98 do not establish domain-free disentanglement. Training costs increase; latency superiority is unsupported.

**Study question:** What do the domain probe and CKA results imply about claims of disentanglement?


## 12. Provenance and manuscript action

**Interpretation:** Keep unlinked primary numbers separate from verified comparisons. Prioritize checkpoint recovery, faithful ports, class-level diagnosis, controlled optimization and patient-level independence checks.

**Study question:** Which results can be linked to retained checkpoints, and which are only reported?

## Original detailed evidence (verbatim)

The source contains compressed spacing; retained here to preserve every detail and numerical qualification.

```text
FINAL COMPLETED-COMPARISON ANALYSIS —24November2026

EVIDENCE AUDIT
The latest recovered suite completed198mainruns plus3DoRLpipelines. Recomputed276saved prediction sets, checking label/folder mapping, metric agreement, image-ID counts and finite normalized probabilities. All checks passed. Smoke/pilot outputs are excluded from publication aggregates. Earlier verified studies are retained with their original protocol labels. These counts are not276independent trained models: multiple datasets/classifier heads can come from the same trained pipeline.

OVERALL SCIENTIFIC CONCLUSION
The supported contribution is a WBC source-accessible UDA recipe with dataset-dependent external-transfer benefits and useful component regularization. There is no universal advantage across target adaptation, all external datasets, source-only DG, annotation budgets or inference settings. Specific weaker ports do not establish general superiority over their original published methods. The stronger new Wen and VL2V results must remain visible.

COMPARISON CRITERIA
Use comparison_criteria.csv and criteria.tex. A fair comparison has multiple dimensions, not a single yes/no property:
- Same task/classes, evaluation images and metric. MacroF1 differs from weightedF1/accuracy.
- Source access: source-accessible versus source-free; no source-onlymethod receives target training images.
- Target supervision:0classlabels versus100classlabels versus1427additionalsegmentation masks.
- Unseen external transfer versus unlabeled adaptation to each external test batch.
- Encoder/pretraining resources:ImageNetR50,CLIP,SAM,StableDiffusion; additional annotation/pretraining exposure.
- Training steps, sampler, augmentation, checkpoint selection and actual compute. Same nominalbudget is not equalFLOPs; SWAD can stop early.
- Inference1/5/15views, diffusionnoise trials, and whether parameters/anchors update on the testbatch.
- Threeindependent trainingseeds versus batch permutations versus deterministic singlefit; aggregate domains withinseed beforeSD.
- Fidelity:author-codeport versus independentpaper-basedimplementation versus diagnosticextension; deviations explicit.
- Provenance:retained checkpoint/predictions versus reported primary results without a linked checkpoint.

1.COMMON-COHORT RECENT UDA
F1Acevedo/Raabin/AML(mean+-sampleSD,3seeds):
Source architecture control85.54+-5.00/66.14+-10.74/58.20+-7.27.
MIC97.06+-1.97/28.55+-13.92/58.02+-19.82.
PLUE92.62+-1.26/59.47+-1.87/70.18+-3.96.
DIFO54.12+-4.74/16.20+-1.94/23.85+-12.64.
CRPL50.71+-1.84/34.41+-3.08/36.45+-3.05.
Proposed81.37+-10.90/63.35+-3.17/65.65+-2.71.
Strongest within-architecture result:AML+7.45pp,positiveall3seeds and improved mean F1for all5classes. Recentadaptedportcomparison:Raabin+34.80vsMIC(all3),+3.88vsPLUE(2/3). Ours higherthanDIFO/CRPLinallthree domains undertheselocalrecipes.
Limits:MICtargetwinner;PLUEAMLwinner;sourcecontrolRaabinmeanwinner. Oursminuscontroltarget-4.17/Raabin-2.79. LowerRaabinSD3.17vs10.74isdescriptive;targetSDhigher10.90vs5.00. Exploratoryequal-domainexternalaverageours64.50vsPLUE64.82;notanoveralladvantage. Do notreplaceourswithahigher-rowconfigurationfromanotherstudy.
PLUEsourcehead-reference41.35/10.45/38.61improvesto92.62/59.47/70.18withadaptation:strongpositivetransferwithinthisport. Bankrefreshandneighborrefinedinference deviations remain. DIFOreference49.97/13.84/44.74becomes54.12/16.20/23.85:negativeAMLtransferinthisport. CRPLhasnodirectmatchedsource-referencehere,so causeoflowperformanceisunisolated.

2.WEN2025—NOWCOMPLETE
Source-onlyWenfullF1:84.64+-2.05/56.69+-5.78/66.97+-1.01.
Matched80promptdistillationbase:82.59+-1.10/54.84+-3.52/69.13+-2.11.
Fullminusbase:+2.05target(2/3seeds),+1.85Raabin(2/3,SD8.58),-2.16AML(1/3positive). Additionalobjectiveshelp somedomains,notall.
OursrelativeWenfull:-3.27Acevedo,+6.66Raabin,-1.32AML. OursusesunlabeledAcevedo;Wendoesnot. Sameevaluationimages permit system-levelcomparisonbutnotmatchedalgorithmcausalattribution. SourceonlyWen/CLIPresultsalso refuteblanketclaimsthatvision-languagemodelsfailonWBC.
Independentimplementationfrompaper,notauthorcode;Eqinterpretationsandnumericalchecksinremaining_experiments. Exactpublishedbenchmarkreproductionnotclaimed.

3.DORL—ALLHEADSAND3PIPELINESEEDS
F1Acevedo/Raabin/AML:
RF(primarypredeclared)59.11+-8.87/26.31+-7.45/46.68+-8.39.
ANN71.35+-8.74/28.82+-12.18/62.24+-4.69.
LR64.43+-22.28/21.67+-14.52/61.53+-8.62.
SVMlinear63.16+-17.92/25.56+-15.69/58.12+-9.25.
SVMpoly57.02+-7.69/26.59+-5.37/45.49+-4.39.
OursbetterallthreeF1means thanalltestedheads. ANNclosestoverall;oursminusANN+10.03/+34.53/+3.42pp. Reportallheads,nopost-hocprimaryheadselection. RFaloneexaggeratesthegap.
Importantclass-levelqualification:AMLANNmonocyteF174.20vsours56.25;lymphocyte61.75vs60.04. Oursstrongeronbasophil52.29vs33.26,eosinophil75.56vs64.70,neutrophil84.11vs77.27. ThusmacroF1advantageisnotclasswiseuniversal. Accuracyalmostsame65.67oursvs65.59ANN,whilemacroF1differs3.42pp:balancedclassperformanceisimportant.
DoRLuses1427auxiliarypublicsegmentationmasksafteroverlapexclusion,SAMLoRA85epochs,CAE10epochs(source+unlabeledAcevedo),fixedsourceclassifiers. Input/maskpreprocessing,microbatchandoriginalthree-domainprotocoldiffer. SVMprobabilityargmaxdiffersfromauthorhardpredictconvention. NoSAM-only/CAE-removalcontrols;cannotattributeanygap toonecomponentorclaimoriginalDoRLisinferior. Patient-levelindependenceofauxiliaryassetsunverified.

4.CYTODIFFUSION
Budgetedsource-onlyportF144.01+-25.06/32.79+-2.54/45.07+-6.03;sourceF192.67+-.50.
Oursstrongermeansunderretainedrecipes,butoursusesunlabeledAcevedoandCytoonlylabeledsource. Lower224resolution,noEMA,8noise-trialinference,fixedfinalcheckpoint arematerialchanges. LargeAcevedovariabilitysuggestsinstabilitybutcausenotisolated. Do notclaimallgenerativeclassifiersinferiororthatoursismatched-computefasterwithoutmatchedprofiling.

5.SOURCE-ONLYWBCDG
CLIPERM75.08/21.18/65.41;VL2VSD81.89/53.33/68.53;proposedsource-only77.59/52.66/55.42.
VL2VSDwinsallmeans;proposedvariantcloseRaabin(.67ppbehind),weakerelsewhere. Thisstudyusesitsownsourcebudget/geometry,notmain80epochcontrol;differencefromfullUDAdoesnotisolate targetaccess.

6.ALLCOMPLETEDNATURALDG
AccuracyPACS/VLCS/OfficeHome:
PlainR50ERM70.33+-.86/75.65+-.78/61.58+-.32.
Proposedsource-only69.02+-.87/75.93+-.20/44.28+-4.32.
CLIPERM88.61+-.34/74.92+-3.19/75.47+-.09.
VL2VSD93.90+-.42/82.58+-.50/83.60+-.23.
Wenfull94.90+-.65/82.71+-.16/84.61+-.10.
WenbasePACS93.97+-.42;notrunVLCS/OfficeHome.
Oursminusplain:-1.31PACS(all3negative),+.28VLCS(2/3positive,SD.85),-17.30Office(all3negative). TheVLCSdifferenceistoosmallforasuperiorityclaim.
WenminusVL2V:+1.01PACS(all3),+.13VLCS(2/3),+1.01Office(all3). Descriptive3seedresults,nosignificanceclaim. PACSfullWenvsitsbase+.93pp;mostimprovementoverCLIPERMalsocomesfromthestrongdistillationbaseline.
EarlierTerraaccuracy:CLIPERM26.73+-4.15,VL2V51.09+-.61,ours24.93+-.74.
EarlierDomainNet:CLIPERM51.93+-.19,VL2V58.38+-.20,ours3.74+-.66.
Weaksource-onlygeneralizationisaclear limitationofthisconfiguration,notanevaluationofthecompleteUDAmethod. OnOfficeoursbestsourceval55.83vsplain79.59;lowersourcelearningcontributes,andthegapcannotbeascribedsolelytoheldoutshift. PACSsourceval93.77oursvs94.68plain;VLCS84.06vs84.58. DomainNetinspectedsourceval2.55. Source-learningproblemsgrowwithtaskcomplexityunderthisrecipe,butwhichfactorcausesitrequirescontrolledtrainingchanges.
Resource/fairnessqualification:KerasR50systemsversusCLIPViTB16arenotidenticalbackbones. EvenplainR50andoursdiffersinheads,objectivesandpooledversusdomain-balancedsampling;system-levelgapnotisolatedmorphologyloss effect.
Recoveredcohorts:PACS9991;VLCS10720after9duplicatecopiesexcluded;OfficeHome15089after499duplicate/conflictingfilesquarantined. Rawarchivespreserved;cleanedcohortsnotexactpublishedbenchmarkversions. Source80/20splitandheldoutINevaluationused;noheldouttuning. EarlierTerra/DomainNetareaseparatecohortversion. Nofive-datasetaverageforWen/plainbecausemissingTerra/DomainNetruns.

7.SUPERVISED100LABELADAPTATION
Same650Acevedoholdout:color/fewshot96.31+-.41with100labels;MIC97.02+-1.82,PLUE92.10+-1.30,ours81.31+-10.86with0labels. ColorportisstrongrelatedWCBevidence,notabeatenbaseline. Annotationbudgetandencoderdiffer.
KDEindependenttwoepisodeport:sourcehead83.73source/59.72target;fine-tune78.94source/76.64target;KDE+KD83.31source/73.06target. Replayretention+4.37ppversusfine-tune,buttarget-3.58/AML-6.14. Raabin28.37vs25.07. Noformalprivacyguarantee,nooriginalfourdomaincontinuallearningclaim. FrozenCLIP+MLPresourcesand100targetlabelsseparatethisfromUDA.

8.TEST-TIMESETTINGSCANNOTBEPOOLED
StatAfixedpromptzero-shotF110.66/7.26/8.88;authorbatchsolver6.76/2.85/7.31. SDacross3streampermutations,nottrainedseeds. Batchsolveraccesseseachtestdomainunlabeled;doesnotevaluateunseenexternaltransfer. FrozenAcevedoGaussianextension7.81/1.28/14.04;sourceprototypeextension41.91/4.93/24.60;sourceCLIPlinear41.62/35.96/40.52. ExtensionnamesnotoriginalpublishedStatA. Poorfixedpriorisnotall-VLMfailure.
FOODS/SEC:original58.61/29.24/56.45;uniform15views60.54/27.25/56.60;filteredidenticaltooriginal(allaugmentedexternalviewsrejected). Diagnosticfallback,notdefinitivepaperreproduction. MoreTTAviewsarenotuniformlybeneficial.

9.HISTORICALBASELINES—OWNPROTOCOL
SingleviewF1target/Raabin/AML:source77.49/61.50/57.12;CORAL76.39/57.81/52.83;DANN23.41/21.99/26.52;MCD36.02/38.79/43.01;ours73.92/62.30/63.13.
OursAML+6.01vssource,buttarget-3.57. LowDANN/MCDdescribeunstablelocalimplementations,notgeneralmethodlimits. FiveviewresultsarealsoinmasterCSV. Do notmixwithrecentproposedrows.

10.COMPONENTEVIDENCE—MATCHEDCONTROLLEDSTUDY
Fullreference81.88/68.47/69.68,notrecent81.37/63.35/65.65.
Fullminusremovalmeanpp(target/Raabin/AML):orthogonality+13.20/+8.73/+11.23(all3each);contrastive+3.46/+1.58/+4.39(positive1/3,2/3,3/3);independentviews-7.35/+10.80/+8.35;agreement-7.79/+4.23/+7.69;adaptiveweights+6.88/+5.29/+6.27(externalall3).
Orthogonalityisthemostconsistentremovaleffect. Independentviews/agreementtradecleantargetfor externalperformance. Adaptiveweightssupportexternalbenefits,butfixedweightsablationdoesnotisolatelearnedpolicyfromheuristicprior. Removalsaffectcoupledoptimization/selection,notanadditivecausaldecomposition.

11.MORPHOLOGY,FEATURESEMANTICS,BACKBONES,COST
Balanced160imagepanels:grayscale62.52/41.22/41.09fullvssource40.80/40.38/33.64. RemovingcontrastivereducesgrayF1by16.27/5.42/8.68pp. Tilepermutationreducescleanpanel82.38/77.86/71.69to8.41/6.67/6.67. Supportscolor-robustspatialdiscrimination;grayremovesusefulstaincues,scramblingisnotlabelpreserving.
Morphologybranchdomainprobe89.17%versus25%chance;branchCKA.95-.98. Usefulregularization/overlap,notdomain-freeanatomicaldisentanglement. Confusionmatrices/probesdonotidentifycausesofindividualerrors.
Controlledbackbones:R50full81.88/68.47/69.68;EffNetfull81.58/66.30/73.04. EffNethigherabsoluteAMLunderthisrecipe. Source-relativegainsR50+1.17/+5.42/+10.05;EffNet+3.45/+3.37/+.10. Broadbackbone-independentbenefitisunsupported.
Controlledtraining14.91vs9.12minR50and15.93vs10.31minEffNet(1.64x/1.55x). One-imageinference3.24vs3.05ms;params24.97vs24.11M. MeasuredlatencySDoverlaps;noefficiencysuperiorityclaim. Cytohasdifferentinferencecost/batch/budget;noimputedmatchedspeedups.

12.PROVENANCEANDMANUSCRIPTACTION
Higherreportedprimary93.07/88.18/73.78andcomparison90.57/82.72/74.66areunlinkedtoretainedcheckpoints. Preserveasreportedconfigurationsonly;donotinsertintoverifiedrecentbaselinecomparisons. Componentstudy,oldhistoricalstudy,recentUDAandSGDvariants legitimatelyhavedifferentfullreferences. Theircausaldifferenceshavenotbeenisolated.
Recommendedorder:
4.1Data/access/resource/provenanceprotocolmatrix.
4.2CommoncohortrecentUDA(main_recent.tex).
4.3RelatedWBCsystems(related_WBC_complete.tex),explicitresourceannotations;allDoRLheadsin supplement.
4.4Controlledcomponent/mechanism evidence,ownreference;perclassfigure/erroranalysis.
4.5Stability/backbone/cost,scopedtospecificcheckpoints.
Supplement:allnaturalDGincludingnegativefindings(natural_DG_complete.tex),allseeds/heads,100labelandTTAsettings,historicalbaselines,safeasset/duplicateaudits.
Stateofartclaimmustbeconditionalonexacttaskandprotocol;nooveralluniversalSOTAclaim.
Mosturgentimprovements:reproducibleprimarycheckpointlink;faithfulPLUEbank/inference;classconditionalpseudolabelcollapse/monocyteerrors;controlledsource-learningdiagnosis(head/sampler/LR/lossweights);explicitRLprior/policycontrols;patient/slidedisjointexternalsiteverification. Theseareproposals,notalreadymeasuredimprovements. Noadditionaltraininglaunchedforthisanalysis.

```

