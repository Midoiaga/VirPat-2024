# VirPat-2024

## Annotation guide

| Main Intents         | Description                                                                       | Examples                              | Amount                              |
|----------------------|------------------------------------------------------------------------------------|----------------------------------------|--------------------------------------|
| afirmar (affirm)              | When the doctor confirms the patient's response.                                   | Yes / Very good                         | 13                                   |
| despedida (goodbye)            | When the doctor wants to end the conversation.                       | Good bye / Good bye!                        | 6                                    |
| estado  (state)              | When the doctor asks how the patient is doing in general.                           | ow are you / how are you?              | 7                                    |
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
|                         | si_o_no (yes/no)                                                    |When the doctor questions the patient about a particular symptom and when he expects a yes or no answer. | Do you have ringing in your ears? /
do you have an itchy nose?  | 662|

