Research on Evaluation Metrics for AAIE ![](Aspose.Words.51022809-1b95-4805-a26f-bc84ae6218e0.001.png)

**Why we wrote this** 

ForAAIE,we’refine -tuninglanguagemodelsto detectAI -generatedwritingand produce teacher-style feedback for student work. This report explains, in everyday terms, the measures(“metrics”)we’llusetojudgewhetherourmodelsaredoingagoodjob , whateach metrictellsus,whatitdoesn’t,andwhentousewhich metric.

**The two things we’re evaluating** 

1)AI -detection(IsthistextlikelywrittenbyAI?):Wecomparethemodel’sdecisionsagainst knownexamples(human,AI,orhybrid)andseehowoftenitgetsitright.

2)Feedbackquality(Isthemodel’sfeedbacksimilarincontentandmeaningtoateacher’s feedback?): We compare the model’s feedback with real teacher feedback for the same essay.

**Perplexity metric** 

Perplexityisanumberthatreflectshowpredictableapieceoftextistothemodel(lower= lesssurprise).Weuseitduringtrainingtomonitorlearningandpickthebestcheckpoint, andasasupportingsignalforAI -detection.

Limits:lowsurprisedoesn’tguaranteequalityorcorrectness,sowedon’tuseitaloneto judgefeedback.

**BLEU metric** 

BLEUisaphrase -matchingscore.Ifthemodel’sfeedbackreusesmanyofthesameshort phrasesthatateacherused,BLEUtendstogoup.Goodforstyle/wordingsimilarity.

Limits:canmissgoodparaphrases.

**ROUGE metric** 

ROUGEcheckscoverage:didthemodelmentionthekeyideastheteachermentioned?Good forensuringfeedbackcoversrubricpoints.

Limits:stilloverlap -based;doesn’tfullyunderstandmeaning.

**BERTScore Metric** 

BERTScorecomparesmeaning,notjustwords.Ituseslanguagerepresentationstoseeif twopiecesoffeedbacklineupsemantically,evenwithdifferentwording.Goodforcapturing paraphrases;usuallyalignsbetterwithhumanjudgmentthanpureoverlap.

**Classification metrics (for AI**-**detection or rubric labels)** 

Accuracy = overall right -or-wrong. Precision = when the model says “AI”, how often it’s correct.Recall=ofallactualAIcases,howmanywecatch.F1=balanceofprecisionand recall.Averaging:Macrotreatseachclassequally(goodwithimbalance);Weightedreflects real-worldproportions;Microaggregatesglobally(oftenequalsaccuracyinmulticlass).

**Fairness and care** 

We’ll review errors across meaningful groups (e.g., ESL status, essay length, topic) and adjustthresholdsorrulesifweseeunevenpatterns.Teachersremainthefinaldecision - makers.Modeloutputisadraftorasignal and notaverdict.

**When to use which metric**  

•Whiletraining:trackPerplexityforlearningprogressandcheckpointchoice.

•Feedbackquality:useBERTScore(meaning),plusROUGE(coverage)andBLEU(overlap), withasmallteacherreview.

•AI -detection/rubriclabels:reportPrecision,Recall,F1,Accuracyandstatewhetherresults aremacroorweighted.

**How we set up trustworthy testing** 

We’llbuildastratifiedgoldset(acarefullycurated,human -checkedmini-datasetcovering different essay types). We’ll keep training/validation/test splits fixed so scores are comparable over time. Where possible, we’ll include real teacher feedback so BLEU/ROUGE/BERTScorearemeaningful.

**What this means for AAIE — AI**-**detection** 

Wewillcalibratethedetectortobalanceprecision(avoidfalseflags)andrecall(catchreal cases). Results will include a confidence signal and short explanation. Teachers are encouragedtoreviewflaggedcasesratherthantreatthemasfinal.

**What this means for AAIE — Feedback generation** 

Wewillfine-tunemodelsonteacher-styledataandjudgeresultsbymeaning(BERTScore), coverage (ROUGE), and overlap (BLEU), with teacher review as the final word. Draft feedbackwillbe clearlylabelledandeditable.

**What we will publish (simple, repeatable outputs)** 

•Trainingcharts:Perplexityovertimeandthechosencheckpoint.

• Feedback quality: BERTScore, ROUGE, BLEU, plus a few anonymised examples next to teachercomments.

•AI-detectionquality:Precision,Recall,F1,Accuracy,andashortnoteonfairnesschecks.

**Key takeaways** 

No single number tells the whole story. We use a bundle of metrics to reflect wording, meaning, coverage, and decision quality. Perplexity is for training progress and early checks,notforjudgingfeedbackusefulness.BERTScore+ROUGE(+BLEU)givearounded picture of feedback quality; Precision/Recall/F1 summarise detector behaviour. Fairness andteacheroversightarebuiltin:modelsassist and teachersdecide.
