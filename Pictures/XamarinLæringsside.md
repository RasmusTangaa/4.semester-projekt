[Tilbage](https://rasmustangaa.github.io/4.semester-projekt/Xamarin/)  

Denne side kommer til at afdække selve produktet af den app, som jeg har procuderet i xamarin forms. Her har jeg testet produktet på android, da det fra start har været nemmest at koncentrere sig om android, samt at det har været lidt svært at få testet på IOS.  

Ideen med projektet startede med et medlem af gruppen, Malik Bonnicksen, som sammen med PO for den nystartede virksomhed Megahard fremlagde projektet:  
![image alt text](Udklip50.PNG)  
![image alt text](Udklip51.PNG)  
![image alt text](Udklip52.PNG)  
![image alt text](Udklip53.PNG)  

Hertil har jeg som beskrevet designet en app, som ligesom billedet viser, forbindet til en raspberrypy server, hvortil der kan hentes en playliste ned, og der kan oploades sange til playlisten.  
Undervejs vil jeg beskrive hvordan jeg sætter den færdige server op, så jeg kan bruge den til mit behov, nemlig at forbinde til min app.  
Serveren er lavet således, at den er forbundet til spotify, hvor det kræves, at man har spotify premium, hvis man gerne vil lægge sange op i Queue gennem serveren, som bruger en spotify api. At hente playlisten ned kræver derimod ikke spotify premium.  

På min PC har jeg en mappe med hele projektet af RaspberryPy, som har python som sprog. Dette har jeg hentet fra Maliks github.  
For at starte serveren laver jeg en git bash på mappen, hvor jeg starten serveren med følgende:  
![image alt text](Udklip54.PNG)  

Selve min app er bygget op efter MVVM arkitekturen, hvilket betyder at man har Models - Views - Viewmodels. 
Models står for at lagre alt business logikken og data for de objekter der er relevant i forhold til de user stories som PO har opsat for at projektet bliver en succes.  
Et eksempel kunne være en "User":  
![image alt text](Udklip55.PNG)  

Dertil er der Viewmodels, som bindeleddet mellem View og models, samt de services, som jeg bruger i projektet til f.eks at forbinde til raspberryPy serveren.  
Et eksempel kunne være den viewmodel jeg kalder "AccountViewModel", som styrer alt der er relevant for at dataen fra en bruger bliver retmæssigt præsenteret i de views, som viser Brugerens account. Her er nogle små udsnip af viewmodellen, som viser brugen af en User property med inotifychanged event, samt async metoder, der forbinder til en service, og henter en bruger og opdatere en bruger:  
![image alt text](Udklip56.PNG)  
![image alt text](Udklip57.PNG)  

Herefter er der Views, som er det sidste led, og som sørger for at man har en god brugergrænseflade, som slutbrugeren kan kigge på og interagere med.  
Disse views bruger Xaml til at lave designet med. Et eksempel kunne være:  
![image alt text](Udklip58.PNG)  
1. en klassisk xaml binding, hvor man binder til property "CurrentUser" fra den viewmodel som jeg viste tidligere.  
2. en command binding, som fungere lidt på samme måde, hvor man har en property i sin viewmodel af typen Icommand, som man så forbinder en metode til. Hertil kommer der et eksempel efter punkt 3.  
3. Da det er en tabbedPage jeg viser her i it view, så fungere det ligesom en liste af view man kan trykke på. Her er "SongPage" f.eks en helt view i sig selv, som vises, når man trykker på den i sin tabbedPage. Dette var kun et af mange eksempler på et view.  

Hertil et eksempel på brugen af Icommand, med en forbundet metode til:  
Først selve property for Commanden:  
![image alt text](Udklip59.PNG)  
Herefter tilskriver man Command property til en bestemt metode.
![image alt text](Udklip60.PNG)  
Hvor metoden også ligger i Viewmodel, og er faktisk en metode som allerede er vist længere oppe i form af "UpdateUserAsync".  

Efter denne korte gennemgang af MVVM arkitekturen til min app, så tænker jeg at jeg vil vise nogle af de funktionaliter, som gør sig gældende i den app jeg har lavet.  
Generelt er funktioaliterne:  
- Login side med email og kodeord
- Registerings side med email, kodeord, brugernavn og mobilnummer. Her fungere mobilnummeret som en validering af kontoen, da brugeren får et godkendelses besked tilsendt, hvor man så indtaster en kode i appen.  
- en konto side, hvor man kan ændre nogle af sine kontooplysninger. f.eks brugernavn.  
- En side hvor man kan se den nuværende playliste med de sangnumre der kan afspilles.  
- en side hvor man kan forbinde til en bar, og derefter vælge en sang der skal indsættes i playlisten mod betaling af 1 token.  
- en side til at lægge flere tokens ind.  

Jeg vil starte med at vise login og registrerings siden, hvor jeg til dette formål har bruge googles firebase. Her er der en authentication database med brugerens email og kodeord, som jeg har forbundet med deres realtime database til at oplagre data om brugeren som mobilnummer og brugernavn. Databasen gør brug af NoSql, hvilket er en forandring i forhold til tidligere semestre. I NoSQl har man en hel del mere fleksibilitet, da man kan gemme en hel masse ustruktureret data. Ulempen er selvfølgelig, at det kan være svært at navigere i, hvis man har meget forskelligt data. I mit tilfælde har det dog kun været bruger informationer, da jeg kun har brugt det til login authentication.  

Først login siden:  
![image alt text](Udklip61.PNG)  
På siden har man mulighed for at indtaste email og kodeord.  Ting som "Remember me" og "Forgot password" er dog ikke implementeret, da jeg ikke har vurderet det så højt.  
Derudover kan man trykke på "Sign in", når man har tastet de rigtige login oplysninger, samt trykke på "Sign Up", hvis man ikke har en konto.  
Herefter Registeringssiden:  
![image alt text](Udklip62.PNG)  
På denne side taster man oplysninger ind i de 4 felter. Når man har gjort det, så kan man bede om en validerings sms, hvor man så taster den kode ind, som man har modtaget på sin mobil nummeret tilhører.  
Herefter er man registeret. Disse ting vises på billederne nedenunder:  
![image alt text](Udklip63.PNG)  
Man trykker altså på "Send Verification sms", hvortil at man får tilsendt en kode til det angivne nummer. Nummeret er et testnummer jeg anvender, hvor den faste kode tilsendt er 123456.  
![image alt text](Udklip64.PNG)  
Herefter trykker man på "Verify code", hvortil at hvis koden passer, så bliver man registeret, samt automatisk logget ind.  



