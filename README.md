
# VirPat-2024
In this repository you will find the corpora and code used in the following paper: ____PAPER____HERE____

## Introduction
Virtual patients (VPs) have become powerful tools in medical education and health simulation. VPs allow medical students to simulate a real clinical consultation, allowing them to reproduce a wide variety of consultation types, thus gaining valuable experience before medical examinations or interviews with real patients. Virtual patients are based on dialogue systems, which are artificial intelligence-based automated systems designed to exchange information with users through natural language conversations. The main goal of a dialogue system is to enable effective communication between humans and computers, understand user input in the form of text or voice, and respond appropriately to user demands. To achieve this proposal we have created 2 medical domain corpora: a corpus of manually aligned doctor questions, patient responses and the corresponding clinical history [(QA corpus)](#QA)  and a corpus of medical dialogue questions in Spanish annotated with intentions [(Intent corpus)](#Intent). Furthermore, to demonstrate that these corpora are useful, we created 2 models: For the first a Question-Answer system ([Code](https://github.com/huggingface/transformers/blob/main/examples/legacy/question-answering/run_squad.py) to experiment with the QA model and the best final model(liiiiiinnnnnkkkkk)) and for the second an intent classification system ([Code](https://github.com/Midoiaga/VirPat-2024/blob/main/ClinicalIntentClassification(Vir-Pat).ipynb) use to create the Intent classifier model and the final best [model](https://huggingface.co/Mikelium5/DoctorIntentClassifier)).


## VIR-PAT-QA corpus
<a id="QA"></a>
The aim of the VIR-PAT-QA corpus is to associate is to associate each dialogue with a corresponding clinical record in natural language, enriching the dialogue dataset with a textual description of each patient, thus opening the way to create new virtual patients simply by adding new clinical records to the dataset. To get that goal we tranlate automatically from English to Spanih doctor-patient consultation dialogues, recorded following the format of the OSCE exams and later on trancribed by [(Fareez et al. (2022))](#Fareez). Once tranlated the text, we had to manually correct all the tranlations errors. Then, we created the clinical records taking into account the doctor-patient dialogues. To end, we need to associate each answer of the patient to the clinical report where this answer was given.
 


![alt text](https://github.com/Midoiaga/VirPat-2024/blob/main/Figures/procesamientoDatos.png)

The final dataset contains a total of 6290 question-answer pairs from 129 different clinical cases in the SQuAD v2.0 format from Rajpurkar et al. (2016) with json structure. It was divided into training, development and test sets (75%, 10% and 15% of the corpus respectively). In this dataset we can find 3 type of questions:

  - Questions that need to be answered: questions that require seeking the answer in the reports.
    
      * Answered questions: the response appears in the report

      * Unanswered questions: when the information necessary to respond does not appear in the report, the span is empty and the "is_impossible" attribute value was set to True. This type            corresponds to questions where the patient did not understand the question or when the answer in the dialogue did not answer the question. (This type have an empty space in the     "answer" section from the dataset)

  - Questions that do not need and answer, as when the medical student makes a comment. For example, in a relatively important proportion of the utterances given by the doctor or medical student there are expressions like "Thank you", "OK", "Now I will check your temperature" that do not require an answer from the patient. It is important that these types of sentences are understood and detected, because otherwise a standard QA system would try to give an answer for every question it is being asked, and that would be incorrect for these types of utterances. (This type have an "I" in the "answer" section from the dataset. This "I" is the first letter of all the reports and it is a way to distinguise the from the other two type of question.)

In the following table you can find the distribution of each type of question:

| Question type                       | train | dev | test |
|----------------------------------------------|----------------|--------------|---------------|
| Questions that need to be answered           | 4573           | 496          | 915           |
  |             - Answered questions   | 2753           | 295          | 580           |
|               - Unanswered questions | 1820           | 201          | 335           |
| Questions that do not have to be answered    | 228            | 27           | 51            |
| **Total**                               | 4801  | 523 | 966  |

The corpus has the next attributes: Starting with the “data” is the part where it is all the information of the clinical reports, questions and answers. Continuing with the “paragraphs” section, we find the clinical report, question and answers of a specific patient. Inside that section we have the “context”, which is the clinical report itself and for the other side the “qas”, which is the part that contains all the information related with the question and answers. From the questions we can get the question text itself (“question”), an identifier (“id”), the flag that determines if a question is possible to answer to the question with the context or not (“is impossible”). And the “answer” element is comprised by the the text of the actual answer (“text”) and the span where the text begins (“answer start”). To end, we have less relevant attribute which is the document id or title (“title”), this attribute is not taken into account by the model.

Moreover, the QA corpus also contains different format of question: the one that has the only the question itself, other one with the question and the intention of the doctor together and the last one that only has the intention of the doctor.




##  Intent corpus
<a id="Intent"></a>
This corpus is an adaptation from the French corpus of the "A French Medical Conversations Corpus Annotated for a Virtual Patient DialogueSystem" [(Laleye et al. (2020))](#Laleye) paper. The corpus
was automatically translated from French to Spanish and it was manually corrected, giving 2691 utterances where 145 different intent types were identified and from them 11 were considered main categories. They were classified in a hierarchical way from more generic to more specific. The deepest brach of the hierachy could arrive 4 leves of subcategories, counting the main category. The corpus is divided in three different sets in a stratified way, 80% for training containing 2079 utterances and 10% for development and test with 306 utterances each.

This dataset has a csv format, where the first column is the utterance of the doctor ("texto"). The next column refers to the main intention of the doctor (categoria_general) and the next columns until "intent_3" are subintents of the previous columns. And the last column (intent_4) is the final reprentation of the intent for that utterance.


The following tables explains each intent with a descrition, example and amount:

| Main Intents         | Description                                                                       | Examples                              | Amount                              |
|----------------------|------------------------------------------------------------------------------------|----------------------------------------|--------------------------------------|
| afirmar (affirm)              | When the doctor confirms the patient's response.                                   | Yes / Very good                         | 13                                   |
| despedida (goodbye)            | When the doctor wants to end the conversation.                       | Good bye / Good bye!                        | 6                                    |
| estado  (state)              | When the doctor asks how the patient is doing in general.                           | How do you feel? / How are you?              | 7                                    |
| motivo_de_consulta (reason for consultation)  | When the doctor asks the patient why he has come to doctor.                        | Why are you coming? / What brings you here?  | 61                                   |
| otros (others)               | Which are not part of other _intent_ groups, because they have nothing to do with the topic. | I ask for your health card           | 5                                    |
| personal (personal)            | When the doctor asks for the patient's lifestyle and personal data.            | ¿Do you drink alcohol? / What is your name?      | 499                                  |
| psiquiatria (psychiatry)         | When the doctor says to talk about the patient's feeling.            | What do you feel? / are you happy?             | 60                                   |
| saludo (greeting)              | When the doctor greets the patient to start the conversation.                          | hello / good morning                     | 25                                   |
| sintoma  (symptom)             | When the doctor asks about the symptoms of the patient or those around the patient.              | Allergies? / How's your cough?       | 1604                                 |
| tratamiento (treatment)         | When the doctor asks about the patient's previous treatments.                  | Other medications? / Have you had any surgery? | 384                                  |
| vida_sexual (sexual life)         | When the doctor asks for the details of the patient's sex life.           | Are you sexually active?          | 27                                   |
| **Total**          |                                                                                    |                                        | 2691                                 |



| Intent personal | Description                                                                                   | Examples                                         | Amount |
|--------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------|--------------------------------------|
| adiccion (addiction)                | Questions about the patient's addictions are included; the main onesalcohol and smoking with its own category. All other substances category are included more generally. This uterrances are divided in quantity, frequency, etc    | Do you drink alcohol? / How much do you smoke? | 112 |
| contacto (contact)                |When the doctor asks the patient who to contact in case of emergency. |   Who is the person to notify? / Who to alert in case of need? | 7 |
|   datos (data)                   | When the patient's personal data is requested; eg name, years etc.                        | Where do you live? / What is your name?                          | 58              |
| deporte (sport)                 | When the doctor asks to explain the patient's attitude towards sports.                              |  Do you practice sports? / Do you often make physical activities?      |34|
| dieta (diet)                   | When the doctor asks about the patient's eating habits.                                    | Do you eat a lot? / What is your diet?                        | 60                  |
| entorno (environment)                 | Questions about the patient's friends, family, pets, etc.                        | Do you have children? / any pets?                          | 81                        |
| fisico (physical)                  | When the doctor wants to know the physical characteristics of the patient.                                         | How much do you weigh? / What is your height?    | 54 |
| otros (others)                   | These are questions about the patient, but when they don't have much relation with the medical field.   | What is your favorite color? / lifestyle | 14 |
| sueño (sleep)               | There are questions about the patient's sleep habits and how well they slept.    | Do you sleep enough? / Do you sleep well? | 16 | 
| trabajo (work)                 | When the doctor asks questions about the patient's occupation.                                     | What do you do for a living? / Where do you work?     | 47|
| viaje (trip)                   | When the doctor asks about the patient's recent travels.                               | Did you travel? / Have you been in the foreign | 16|


| Intent treatment | Description                                                                             | Examples                                          | Amount |
|-----------------------------|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------|--------------------------------------|
| anticonceptivos (contraceptives)            | Questions about contraceptives. | Do you have an IUD? / do you usecontraceptives? | 20|
| consulta (consultation)                   | When the doctor wants to know if the patient has had a previous consultation.                          | Did you have any tests done before go to the emergency room? / have you ever been at another doctor?  | 31|
| diagnostico (diagnosis)                 | When the doctor asks about previous diagnoses.                                         | How do you know your pressure arterial is high? / When did you have an ophthalmological diagnosis?        | 20|
| historial (history)                  | When the doctor asks to provide the patient's medical history.                                   | Do you have any medical history? / Let's talk about your medical history / | 13|
| medicacion (medication)                 | Questions to find out what kind of medication the patient is taking.                       | When did you take the doliprane? / Are you taking any medication?  | 105|
| operacion (surgery)                  | Utterances about future or past surgeries.                        | When did you have sphincter surgery? /Why do you want to take away your gallbladder? | 195|


| Intent psychiatry | Description                                                                        | Examples                                    | Amount |
|-----------------------------|----------------------------------------------------------------------------------------------|-------------------------------------------------------|--------------------------------------|
| psiquiatria (psychiatry)               | When the patient is asked to give an opinion about his life                         | do you think you should search aid? / Are you satisfied with your life in general? | 44|
| estado_de_animo (mood)          | When the doctor asks about the patient's current mood; that is to say, it is checked whether the patient is happy, sad, angry, etc | are you relaxed / do you feel depressed| 16|


| Intent sexual life | Description                                                                          | Examples                                 | Amount |
|------------------------------|------------------------------------------------------------------------------------------------|----------------------------------------------------|--------------------------------------|
| describir (describe)                 | Open-ended questions about the patient's sexual life.                                         | tell me about your sex life                          | 5 |                  
| edad (age)                        | When the patient is asked when he lost his virginity.                                        | How old were you when you had your first sexual relationship? | 5 | 
| frecuencia (frequency)                  | Asking the patient how often they have sexual intercourse.  | How often do you have sexual relations? | 5 | 
| otros (others)                       | These are questions about sex life, but they are very rare for the evaluation of a diagnosis.    | Are you straight? / Are you heterosexual, homosexual or indeterminate sexuality | 5 | 
| si_o_no (yes/no)                   | These are questions about the patient's sexual life, but only for those that expect a yes or no answer. | Are you sexually active / Have you ever had sex? | 7 |


| Intent Symptom               || Description                                                                    | Examples                  | Amount                            |
|---------------------------------------------|-------------------------------------------------------------|------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| bebe (baby)                   |                                                             |This type of question only occurs when the patient is a child and they cannot speak so the question goes to their parents.| Has the baby had seizures? / What was the baby's weight at birth? |               10                                         |
| entorno (environment)                |                                                             | Questions about the patient's environment (excluding family).|  Are you exposed to anytoxic sustance? / is there any sick around you?   |          20    |
| familia (family)               |                                                             | When the doctor asks about patient's family diseases and symptoms. |  Does your family have any health problems? / Does anyone in your family have oral leukoedema?    |        43                                            |
| paciente (patient)               | alergia (allergy)                                                    | Questions about the patient's allergies.                      |       allergies? / latex allergy? |30 |
|                         | antecedentes (record)                                               | When doctors ask if the patient has had a certain symptom or disease at some other time.| Has this pain ever happened to you?/ Do you have a history of ulcers? |52 |
|                         | aparicion (aparition)                                                  | When it is asked how and when the patient's symptoms appear. | And did it start suddenly or little by little? / Do your gums bleed when you brush your teeth or spontaneously?  |157 |
|                         |cambio (change)                                                      | What the doctor asks what causes to ease or worsen the symptoms.| Is there anything that makes these worse symptoms? / Is the pain relieved or does it get worse with exercise?  | 91|
|                         | capacidad (capability)                                                  | When it asked to test the patient's abilities. |  Can you stretch your legs in front of you? / Can you move your foot? | 42| 
|                         | causa (cause)                                                     | When the doctor asks the patient what could have caused their symptoms. |  Was there any trigger for this pain? / do the emotions trigger your palpitations? | 61|
|                         | describir (describe)                                                  | Questions about patient's illness or symptoms in a broad way. |  tell me about your illness vulvar / How was the vomiting?|193   |
|                         | duracion (duration)                                                   | Questions like how long the patient has had symptoms.| How long have you had this pain? / how long have you been with pain? | 23  |
|                         |embarazo (pregnancy)                                                    | Questions that can be asked if the patient is pregnant. | Is it your first pregnancy / have you water broken|24 |
|                         | fiebre (fever)                                                     | Utterances about patient's fever.|   Do you have fever? / What is your temperature?| 25  |
|                         | frecuencia (frequency)                                                 | When it is asked how often a symptom occurs.|  Does this tiredness bother you? / How often do you have hallucinations?| 15|
|                         | inicio (start)                                                     | When it is asked when the patient's first symptoms appeared.| When did it start? / When did you start coughing? |45 |
|                         | localizacion (localization)                                               | When doctors ask in what part of the body has the patient the symptom.| can you localize the pain?/does it pain down to the shoulders? |72  |
|                         | secuela (sequel)                                                    | Questions about symptom's consequences in their daily life.| Does your shortness of breath prevent you to do certain things? / Did the pain stop you from eating?  |29  |
|                         | seguimiento (follow-up)                                                | Asking the patient if they have ever come to treat an illness.| And are you being followed for any particular disease?/are you being followed up for your hypertension? | 10|
|                         | si_o_no (yes/no)                                                    |When the doctor questions the patient about a particular symptom and when he expects a yes or no answer. | Do you have ringing in your ears? / do you have an itchy nose? | 662|

## References

Faiha Fareez, Tishya Parikh, Christopher Wavell, Saba Shahab, Meghan Chevalier, Scott Good, Isabella De Blasi, Rafik Rhouma, Christopher McMahon, Jean-Paul Lam, Thomas Lo, and Christopher W. Smith. A dataset of simulated patient-physician medical interviews with a focus on respiratory cases. Scientific Data, 9(1):313, 06 2022.ISSN 2052-4463. doi: 10.1038/s41597-022-01423-1. URL [https://doi.org/10.1038/s41597-022-01423-1](url). <a id="Fareez"></a>

Fr ́ejus A. A. Laleye, Ga ̈el de Chalendar, Antonia Blani ́e, Antoine Brouquet, and Dan Behnamou. A French Medical Conversations Corpus Annotated for a Virtual Patient Dialogue System. In Proceedings of The 12th Language Resources and Evaluation Conference, pages 574–580, Marseille, France, May 2020. European Language ResourcesAssociation. URL [https://www.aclweb.org/anthology/2020.lrec-1.72](url). <a id="Laleye"></a>
