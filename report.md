## TODO

Synthèse de 4 pages en anglais

- Introduction
  - Domaine
  - Idées principales du document étudié
  - Identifier la problématique de l'article

- Positionnement par rapport à l'existant
  - State of the art (at the time)

- Compréhension + Restitution
  - Description de la contribution
  - Explication, synthèse
  - Exemples, commentaires

- Discussion
  - Recul: critique
  - Observations

- Ce qui a été fait depuis

- Bibliographie (recos sur les slides)
  - Hiérarchiser
  - Norme ISO OBLIGATOIRE

  - équilibrer conférence inter et journaux inter
  - éviter ArXiv
  - livres
  - regardernb citations



Soutenance de 10 min + 5 min questions

---

Questions pour le premier jet

- IEEE Keywords corrects?

---


# The Rythm In Anything

## Introduction

The Rythm In Anything, or TRIA, is an artificial intelligence model trained to generate drums with audio-prompted rhythm and timbre.
The work from Patrick O’Reilly et al. fall within Music Information Retrieval discipline, which is the science of retrieving information from music.
The novelty here is the high fidelity drum recordings, generated from a rhythm and a timbre audio.
The model takes simple rhythm patterns, an audio of some beatboxing or tapping sounds; and as drumkit timbres, it only takes an example recording.
The strength of this model is not only the high fidelity of the audio generated, but also that it works even with timbres it was not trained on.
The article focuses on how the dualization of rhythm and timbre allows the model to give better synthetizations.
The code is fully available on their github and webpage.

// Problématique //


## State of the Art - before publication

// sur quoi ils se sont appuyés

At the time of the publishing of their article,

## Contribution

The authors partition their contribution into three separate parts. First, the model, then the dualization task, and finally how the evaluations carried out show the performances of the model.

The authors worked on TRIA, a

#### Datasets





#### Tasks

#### Methodology
// expliquer modele transformer
// tokenization
// pas encoder decoder

// bien expliquer dualization
// donc expliquer les différentes versions


// VERIFY DESC OF MF
The state of the art model used is MelodyFlow, which takes in input an audio prompt of the desired rhythm - sond gestures just like for TRIA, and a text prompt of the desired timbre.
MelodyFlow is a one billion parameter transformer model. It was trained both on public and private data, for twenty thousand hours of music in total.
There is a parameter that controlls how much the generated audio keeps the rhythmic structure of the given rhythm prompt. This target flow step is a parameter that ranges from 0.0 to 1.0, corresponding respectively to full noising and no noising. In other words, values closer to 0.0 will lower the influence of the rhythm prompt in the output audio
The authors chose to use values 0.0, 0.1, and 0.2 for this target flow step parameter, they found that greater values resulted in synthetizations that did not take the timbre prompt into account enough. This results in three versions, used for comparison in the experimentation, respectively Melodyflow_0.0, Melodyflow_0.1, and Melodyflow_0.2.


#### Experiments and Results

The authors conducted subjective and objective evaluations to assess the performances of TRIA. They wanted to measure the quality of the synthetizations, as well as how close the audio generated was to its audio-prompted timbre and rhythm.

**Subjective evaluation**

The subjective evaluation was carried out in order to verify how musically pleasing the generated audios were, and also how the synthetizations from TRIA compared to MelodyFlow's generations and the random excerpts.
For comparison purposes, in these evaluations the authors compare audio generated from the model TRIA 2-band with random audios extracted from the dataset MoisesDB, and also with audio generated from the model MelodyFlow 0.2.
Evaluators here are humans, recruited through the platfomr Prolific. The evaluations were done through ReSEval, which stands for Reproducible Subjective Evaluation. Which is a framework used for building subjective evaluations.
In order to have an homogeneous testers base, the people recruited had to pass a listening test. Out of the 120 persons originally recruited, 116 passed the listening test and went on with the evaluation of the audios.
For the subjective evaluation, listeners rated audio from 80 sets.
A set is composed of an audio rhythm prompt, the associated generation from TRIA 2-band, and from MelodyFlow 0.2, and a drum extract randomly taken from MoisesDB.
The 80 generations were made with ten rhythm prompts: five with tapping sounds, and five with beatboxing audio, on 8 different audio timbre prompts. Each audio clip generated lasts for three to four seconds, which is the duration of the given rhythm prompt.
Three pairwise comparisons were evaluated for each set by five persons, comparing TRIA to MelodyFlow, Tria to the random excerpt, and MelodyFlow to the random excerpt.
Each listener was given ten pairwise comparisons to evaluate.

// INSERER FIGURE

The results shown in // FIGURE XXXXX // show the evaluations form the listeners on the comparisons of each audio. The subjective evaluation shows there are no clear preference when comparing audio synthetized from TRIA 2-band or Melodyflow 0.2.
However, when comparing audio generated from either of these models to the random extract from the Moises database, the favourite one is most often the generated audio.

This is very promising. First, because it means that generations from TRIA are on par with generations from MelodyFlow, which indicates that the authors were able to build a model that performs at least as well as the primary existing model.
Moreover, TRIA is a very small model compared to MelodyFlow. MelodyFlow is a model twenty-five times the size of TRIA, and was trained on two thousand times more data.
Finally, being able to have generations well liked by human listeners but, most of all, with audio input is an even greater achievement. Allowing for audio prompting makes the creative process a lot easier than the complex task of translating the audio prompts into a text that will be correctly interpreted by the model.


**Objective evaluations**

The objective evaluations are conducted on three criteria: adherence to the rhythm prompt, adherence to the timbre prompt, and audio quality of the synthetizations.

The evaluation of the adherence to the rhythm prompt is about measuring how well the rhytmic structure of the rhythm prompt was preserved in the associated generation.
Evaluations were carried out on all variants of TRIA and MelodyFlow, and on the random anchor.
The metric used here is the F1 score, to measure the correspondance between transcription - the audio generated by the model, and ground truth - the prompt given to the model in input supplemented with human annotations about the kick, snare, and hi-hat in the audio.
// EXPLAIN F1 SCORE AND HOW THEY RETRIEVED IT //
A higher F1 score shows for tighter correspondance between the two audios.

// INSERER FIGURE

// timbre adh

// audio quality
Finally, in order to measure the realism of the synthetizations from TRIA compared to random excerpts from MoisesDataBase.
Here the authors decided against comparing TRIA's generations againds MelodyFlows since MelodyFlows uses text prompt describing the timbre prompt.
The metric used here is Kernel Audio Distance, or KAD, which is
// EXPLAIN KAD
The authors used two types of KAD for the evalutation: KAD-PANN, which ...
And also KAD-ClapLaionMusic, which ...


The results of the rhythmic evaluation show TRIA 2-band is performing significantly better than MelodyFlow for beatboxing. The kick and snare placement is better matching the audio prompt.
That is mostly due to the dualization of the audio prompt. Since we separate the spectrogram into higher and lower frequencies // DEVELOP HERE
TRIA 1-band and 2-band non adaptive are overtaken by TRIA 2-band.
Whereas 3-band and 4-band versions of TRIA only show slightly better results in the kick placement, and not so much improvement for the snare placement.
Here, the authors conclude that in order to capture the rhytmic structure of an audio, splitting the spectrogram in two may be efficient enough, to get a synthetization really close to the rhythm audio prompted.

// results timbre prompt

// results audio quality

The authors finish by concluding that TRIA is outperforming MelodyFlow since TRIA's generations are more precise and close to the prompted rhythm and timbre, thanks to the inputs being given as audios, and the dualization of the spectrograms. These are TRIA's strongest advantages.





## Discussion

## State of the Art - after publication

// What has been done since the publication

