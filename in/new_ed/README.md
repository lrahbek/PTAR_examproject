# The New Study Programmes

For the Public Transport Acces and Reach exam project, the study programmes that are newly or to-be established had to be defined, and missing information had to be filled out, the initial csv file can be found in the current folder, ```new_study.csv```. The names, locations and instituions were extracted from Appendix F in the [addendum to the FBUM plan](https://ufm.dk/lovstof/politiske-aftaler/aftale-om-flere-og-bedre-uddannelsesmuligheder-i-hele-danmark/tillaegsaftale-fra-22-marts-2022), and then further specified via the instituions described implementations. 


## Filling out the Blanks

Two major changes were made to the initial list, in Appendix F: The individual instituions submitted plans for how to specfically establish the different study programmes in the initial offer [in 2021](https://ufm.dk/lovstof/politiske-aftaler/aftale-om-flere-og-bedre-uddannelsesmuligheder-i-hele-danmark/implementering-af-flere-og-bedre-uddannelsesmuligheder-i-hele-danmark), and in 2023 a [second addendum](https://ufm.dk/lovstof/politiske-aftaler/aftale-om-flere-og-bedre-uddannelsesmuligheder-i-hele-danmark/2-tillaegsaftale-fra-4-maj-2023) to the FBUM plan were made. This pulled back parts of the initial plan; specifically the instituions were given more freedom in the establishing of the welfare-oriented programmes, because of a record-low number of applications to these in the year prior. The revisions to the initial list, will be with a focus on specifiying each programme and their locations. Some programmes have not yet been established, and others have been scraped - however all prorgams in the initial list will be included, as to not increase the class (new or old) difference even more. The specifications for these are presented here: 

- Per the [suggestions from MARTEC](https://ufm.dk/lovstof/politiske-aftaler/aftale-om-flere-og-bedre-uddannelsesmuligheder-i-hele-danmark/bilag/de-maritime-uddannelsesinstitutioner-institutionsplaner.pdf), the maritime programme in Frederikshavn, have been specified as a Bachelor in Naval Architecture and Marine Engineering (Skibsteknik og marin konstruktion). 

- Per the [suggestions from Zealand](https://ufm.dk/lovstof/politiske-aftaler/aftale-om-flere-og-bedre-uddannelsesmuligheder-i-hele-danmark/bilag/erhvervsakademierne-institutionsplaner.pdf), the three technical programmes in Guldborgsund, have been specified as three Academy Profession Programmes in the subject fields IT, technical, and bio- and laboratory (IT, tekniske og bio og laboratorietekniske ormåde). 

- The new dance study programme in Holstebro have been specified as a bachelor in Dance and Choreography (Dans og Koreografi) by [Den Danske Scenekunstskole](https://ddsks.dk/da/campusser). 

- The new music study programme in Holstebro have been specified as Music and Co-Creation (Rytmisk musik og samskabelse), by [Det Jyske Musikkonservatorium](https://musikkons.dk/uddannelser/rytmisk/rytmisk-musik-og-samskabelse/)

- The AP Graduate in Production Technology (produktionsteknolog), to be placed in Skjern, have been established by [Erhvervsakademi MidtVest, located at Innovest](https://www.eamv.dk/guide-til-uddannelsesvalg/skjern). 

- The bachelors in Social Work in Hjørring, is not being established, however it is still included as it is a part of the original list. Aalborg University were to locate it at the [UCN Hjørring Campus](https://nordjyske.dk/nyheder/hjoerring/dekan-garanterer-en-ny-socialraadgiveruddannelse-med-50-pladser/3438470). 


Further location specifications: 

- The bachelor of Occupational Therapy (ergoterapeut), is to be located at [UC SYD Campus Haderslev](https://www.ucsyd.dk/uddannelse/ergoterapeut)

- The bachelor of Education (lærer i folkeskolen) in Hillerød, is specfically located at [Københavns Proffesionshøjskoles' Campus Hillerød](https://www.kp.dk/uddannelser/laerer/ny-laereruddannelse-i-hilleroed/). 


## Matching the New Programmes with Existing Programmes 

Most of the new programmes have identical (for the most part) existing counterparts. However, some new programmes are the first of their kind, so for the sake of both analysing differences but also visualising differences, they are collapsed with similar programmes. This is done by assigning inidivudal programmes 'CODEs' to represent them, and then assigning the same codes to similar but not identical programmes in the cases where it makes sense. This concerns the following: 

- The three APs in Guldborgsund are not available at any existing study programme. Upon manual inspection of the suggestions and programmes in this area, they all share contents with the APs in Automation Engineering (automationsteknolog), Agro Business and Landscape Management (jordbrugsteknolog), and Nutrition and Technology (procesteknolog). The three new and three old programmes have been assigned the same CODE. 

- Naval Architecture and Marine engineering in Frederikshavn is the first of its kind in Denmark, however it shares similarities with Technology Management and Marine Engineering, why these two are assigned the same CODE. 

- Music and Co-Creation does not share exact name nor contents with any other programme. To be able compare it to similar programmes, all programmes with 'musik' in either the name or the institution name were extracted from the UddannelsesZoom data. When the masters programmes were removed the following were left: Electronic music and sound, Music Management, Music, Music production, Tonmeister, and Musicology. These were all assigned the same code. 

The codes for all study programmes are presented here: 

|CODE|Programmes Included (English)|Programmes Included (Danish)|
|----|-----------------------------|----------------------------|
|VET|Veterinarian|Veterinærmedicin|
|SOC|Social worker|Socialrådgiver|
|MAR|Technology Management and Marine Engineering, Naval Architecture and Marine engineering|Maskinmester, Skibsteknik og Marin Konstruktion|
|ARC|Architecture|Arkitektur|
|MED|Medicine|Medicin|
|PED|Pedagogy/Social Education|Pædagog|
|EDU|Education/Teacher|Lærer i Folkeskolen|
|RAD|Radiography|Radiograf|
|LAW|Law|Jura|
|PRO|Production Technology|Produktionsteknolog|
|MID|Midwifery|Jordemoder|
|OCC|Occupational Therapy|Ergoterapeut|
|BIO|Biomedical Laboratory Science|Bioanalytiker|
|MEC|Mechanical Engineering|Diplomingeniør - Maskinteknik|
|DAN|Dance and Choreography|Dance and Choreography|
|GUL|APs in the IT, technical and bio-and laboratorytechincal fields, and Automation Engineering, Agro Business and Landscape Management, and Nutrition and Technology|IT, tekniske og bio og laboratorietekniske ormåde, og Automationsteknologi, Jordbrugsteknologi og Processteknologi.|
|MUS|Music and Co-Creation, Music, Music Management, Electronic Music and Sound, Music production, Tonmeister, and Musicology|Rytmisk Musik og Samskabelse, Musik, Music Management, Elektronisk musik og lyd, Musikproduktion, Tonemester og Musikvidenskab|