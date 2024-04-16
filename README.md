
# VirPat-2024
In this repository you will find the corpora and code used in the following paper: ____PAPER____HERE____(It will be posted when it is available)

## Introduction

Virtual patients (VPs) have emerged as potent educational tools in medical training and healthcare simulation. They offer medical students the opportunity to simulate authentic clinical consultations, allowing them to practice a wide range of scenarios and gain valuable experience before engaging with real patients during medical exams or interviews. These VPs are built upon dialogue systems, which are automated AI systems designed to interact with users through natural language conversations. The primary objective of a dialogue system is to facilitate effective communication between humans and computers, comprehend user input in the form of text or speech, and provide appropriate responses to user queries.

To realize this objective, we have developed two medical domain corpora: a corpus containing manually aligned doctor questions, patient responses, and corresponding clinical histories in spanish [(VIR-PAT-QA corpus)](#QA), and a corpus of medical dialogue questions in Spanish annotated with intentions (Intent corpus)(#Intent). Additionally, to demonstrate the utility of these corpora, we have developed two models: a Question-Answer system ([QA model](https://huggingface.co/Mikelium5/VIR-PAT-QA/) and [Code](https://github.com/huggingface/transformers/blob/main/examples/legacy/question-answering/run_squad.py) to experiment with) and an intent classification system ([Intent classifier model](https://huggingface.co/Mikelium5/DoctorIntentClassifier) and [Code](https://github.com/Midoiaga/VirPat-2024/blob/main/ClinicalIntentClassification(Vir-Pat).ipynb) use to create it). These models aim to enhance medical training and education by enabling effective communication and interaction between medical professionals and AI systems.


## VIR-PAT-QA corpus
<a id="QA"></a>


The goal of the VIR-PAT-QA corpus is to align each dialogue with a corresponding clinical record in natural language, thereby enhancing the dialogue dataset with textual descriptions of each patient. This approach paves the way for the creation of new virtual patients by simply adding new clinical records to the dataset. To achieve this objective, we initially translated doctor-patient consultation dialogues from English to Spanish, which were recorded following the format of the OSCE exams and subsequently transcribed by [(Fareez et al. (2022))](#Fareez). Following translation, we manually corrected any errors in the translations. Subsequently, we created clinical records based on the doctor-patient dialogues. Finally, we associated each patient's answer with the clinical report in which it was given.
 


![alt text](https://github.com/Midoiaga/VirPat-2024/blob/main/Figures/procesamientoDatos.png)

The ultimate dataset comprises 6,290 question-answer pairs derived from 129 distinct clinical cases, formatted according to the SQuAD v2.0 format proposed by Rajpurkar et al. (2016) with JSON structure. The dataset was partitioned into training, development, and test sets, constituting 75%, 10%, and 15% of the corpus, respectively. Within this dataset, three types of questions are present:

  - Questions that need to be answered: questions that require seeking the answer in the reports.
    
      * Answered questions: the response appears in the report

      * Unanswered questions: They refer to instances where the required information to formulate a response is absent in the clinical report. In the dataset, these instances are characterized by an empty span and the "is_impossible" attribute set to True. Such questions may arise when the patient fails to comprehend the inquiry or when the provided answer in the dialogue does not adequately address the question. Consequently, the "answer" section in the dataset remains empty for these instances.

  - Questions that do not need and answer pertain to instances where an answer is not required, typically occurring when a medical student or doctor makes a comment rather than solicits information. These comments might include expressions like "Thank you" or "OK," or statements indicating the next course of action, such as "Now I will check your temperature." Detecting and understanding these types of utterances is crucial, as a standard question-answering system might erroneously attempt to generate responses for each question posed, which is inappropriate for these types of statements. In the dataset, such instances are denoted by an "I" in the "answer" section, serving as a distinguishing marker from other question types.


In the following table you can find the distribution of each type of question:

| Question type                       | train | dev | test |
|----------------------------------------------|----------------|--------------|---------------|
| Questions that need to be answered           | 4573           | 496          | 915           |
  |             - Answered questions   | 2753           | 295          | 580           |
|               - Unanswered questions | 1820           | 201          | 335           |
| Questions that do not have to be answered    | 228            | 27           | 51            |
| **Total**                               | 4801  | 523 | 966  |


The corpus consists of several attributes: Beginning with the "data" section, it contains all the information regarding clinical reports, questions, and answers. Moving on to the "paragraphs" section, we encounter the clinical report, along with the associated questions and answers for a specific patient. Within this section, the "context" refers to the clinical report itself, while the "qas" section contains details regarding the questions and answers. From the questions, we extract the question text ("question"), an identifier ("id"), and a flag indicating whether the question can be answered based on the context ("is_impossible"). The "answer" element includes the actual text of the answer ("text") and the starting position of the answer within the context ("answer_start"). Lastly, there is a less relevant attribute known as the document ID or title ("title"), which is not utilized by the model.


Moreover, the QA corpus also contains different question formats: the one that has the only the question itself, other one with the question and the intention (intent) of the doctor together and the last one that only has the intention of the doctor.




##  Intent corpus
<a id="Intent"></a>


This corpus is adapted from a French corpus described in the "A French Medical Conversations Corpus Annotated for a Virtual Patient Dialogue System" paper by [(Laleye et al. (2020))](#Laleye). Initially in French, it underwent automatic translation to Spanish and subsequent manual correction, resulting in 2691 utterances. Among these, 145 distinct intent types were identified, with 11 categorized as main categories. The intents were hierarchically organized, spanning up to four levels of subcategories, including the main category.

The dataset is stratified into three sets: 80% for training (2079 utterances), and 10% each for development and testing (306 utterances each). In CSV format, the dataset's columns include the doctor's utterance ("texto"), the main intention of the doctor ("categoria_general"), followed by sub-intents up to "intent_3", and finally, the last column ("intent_4") represents the final intent for each utterance.


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

Faiha Fareez, Tishya Parikh, Christopher Wavell, Saba Shahab, Meghan Chevalier, Scott Good, Isabella De Blasi, Rafik Rhouma, Christopher McMahon, Jean-Paul Lam, Thomas Lo, and Christopher W. Smith. A dataset of simulated patient-physician medical interviews with a focus on respiratory cases. Scientific Data, 9(1):313, 06 2022.ISSN 2052-4463. doi: 10.1038/s41597-022-01423-1. URL [https://doi.org/10.1038/s41597-022-01423-1](https://doi.org/10.1038/s41597-022-01423-1). <a id="Fareez"></a>

Fr ́ejus A. A. Laleye, Ga ̈el de Chalendar, Antonia Blani ́e, Antoine Brouquet, and Dan Behnamou. A French Medical Conversations Corpus Annotated for a Virtual Patient Dialogue System. In Proceedings of The 12th Language Resources and Evaluation Conference, pages 574–580, Marseille, France, May 2020. European Language ResourcesAssociation. URL [https://www.aclweb.org/anthology/2020.lrec-1.72](https://www.aclweb.org/anthology/2020.lrec-1.72). <a id="Laleye"></a>
