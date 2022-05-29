# IT-sikkerheds produktside

På denne side vil der blive fremlagt nogle af de mest centrale produktrelaterede resultater,  
som jeg har opnået i løbet af semesteret.

Hertil skal det nævnes, at der vil tages udgangspunkt i de resultater jeg har opnået undervejs i mit TryHackMe kursus.  
Kurset er opbygget således, at man får noget teori man læser igennem, og derefter skal man prøve nogle eksempler i praksis,  
så man får en forståelse for, hvad teorien kan bruges til.  

Der vil altså ikke blive brugt direkte eksempler, som relaterer sig direkte til det produkt, der skulle laves til virksomheden Megahard.  
Dette er grundet, at det It-sikkerhed med penetration testing som kurset har drejet sig om, hovedsagligt har været websites som angrebsmål.  
Da jeg ikke har stået for at skulle lave hjemmeside i gruppen, men derimod en app i mit andet emne, så har det været lidt svært med tiden at få det til at passe.

Eksemplerne der vil blive gennemgået er kun en lille del af det samlede læringsprodukt, som består af over 300 siders samlet teori og øvelser. Dette ville kunne ses ved at gå tilbage, og trykke ind på "TryHackMe - JR Penetration Tester", hvor man videreføres til et google docs. Eksemplerne vil ydermere kun bestå af de endelige resultater for hvert emne i kurset, og ikke rigtig selve teorien og selve udførelsen af øvelserne, da dette kan ses i google docs dokumentet. Da jeg også gerne vil forkorte det til noget som ikke tager en evighed at læse, så vil der til nogle af emnerne ikke være eksempler for alt hvad jeg har lavet.

# Introduction to webhacking - Første hovedmodul

Kurset begyndte for alvor først med dette emne.  

Det startede med "walking an applikation", hvor man skulle bruge developer tools i browseren til at bryde igennem html og css.  
![image alt text](Billede1.png)
![image alt text](image.png)  

Dertil blev de forskellige værktøjer i developer tools gennemgået, som omhandlede:
- Inspector
- Debugger
- Network


Dernæst var det "Content Disovery", som omhandler hvilke måder man kan indhente informationer omkring et website på.  

Her var det lige fra at tilgå hjemmeside paths, som burde være lukket ned fra udviklerens side:
![image alt text](Billede2.png) 

Og derudover at bruge favicons(hjemmeside url logoer) til at indhente informationer omkring framework:
![image alt text](Billede3.PNG)  

Derudover prøvede man også at sende requests afsted til hjemmesiden, hvor man kunne få informationer omkring serveren osv:
![image alt text](Billede4.PNG)

Derudover kunne der også gemme sig kommentarer, der burde være slettet, når man kigger på en hjemmesides page source:
![image alt text](Billede5.png)

Hvor man tilgik framework hjemmesiden og indsamlede informationer omkring login i dette tilfælde:
![image alt text](Billede1.1.png)

Som i dette tilfælde kunne bruges til noget login på den hjemmeside der bruger frameworket:
![image alt text](Udklip.PNG)

Eksemplet med at have så dårligt et login system er dog nok ikke så mange der bruger i den virkelige verden.  

Dernæst blev der gennemgået en masse automatiserende processer, blandt andet hvor man bruger wordlists der f.eks indeholder kodeord,  
som man kan prøve af automatisk, i stedet for at skulle taste det ind manuelt:

Der blev anvendt noget der hedder FFUF:
![image alt text](Udklip2.PNG)  
Her prøver man en wordlist af på en hjemmesides mange directories:  
![image alt text](Billede1.2.png)



Dernæst var det næste undermodul, som omhandlede "Subdomain Enumeration"  
Afsnittet omhandler, at man skal prøve at finde subdomæner til en hjemmeside.  
Her blev der brugt metoder som Brute Force, OSINT og Virtual host.

Brute Force:  
![image alt text](Billede6.png)

OSINT - Sublist3r:  
![image alt text](Billede7.png)

Næste underemne består af Authentication Bypass

Emnet omhandler hvordan man et websites authentication kan blive brudt.

Man starter med at finde brugernavne, ved at indtaste brugernavne på en hjemmeside, som så derefter typisk vil fortælle, om det pågældende brugernavn eksisterer.  

![image alt text](Billede8.png)
De fundne brugernavne gemmes i et dokument til senere.

Herefter udfører man automatiserede brute force angreb med brugernavne listen, samt med en liste med almindelige brugte kodeord.  
![image alt text](Billede9.png)  

Dette er kun et af forskellige eksempler på authentication bypass. i google docs kan der også ses eksempler med at man lavet reset på et password,  
samt hvordan man manipulere med cookies, for at logge ind.  

Næste underemne er IDOR
IDOR står for Insecure Direct Object Reference, og er når man fra client side beder om nogle filer, data eller dokumenter, men der bliver ikke  
sikkerhedschekket fra server siden af, så man ved ikke om filerne tilhører brugeren.  

Et eksempel jeg har gennemgået til dette emne er f.eks at man har en lignende url:  
online-service.thm/profile?user_id=1305   
Her kan man se nogle data om en bruger der har et id på 1305.  
Men hvis man ændrer i url, så der f.eks står 1000 i stedet, så vil man se informationer omkring en bruger med id på 1000.  
Dette er et IDOR brud. Derudover fremgår der flere eksempler hvor værdien er hashed og meget mere i google docs.  

Hertil har jeg et lille praktisk eksempel, som jeg selv lavede med IDOR:   
![image alt text](Udklip3.PNG)  
Her brugte jeg bare developer tools i browser til at lave IDOR, da det var et eksempel, hvor der i url ikke var mulighed for at ændre id.

Næste underemne er File Inclusion.

Generelt handler File Inclusion om, at man i nogle applikationer vil kunne hente filer osv. Men Dette kan udnyttes ved at bruge "path traversal",  
hvor man gå tilbage i diretories med ../  
![image alt text](Billede10.png)  
![image alt text](Billede11.png)  

Bedste eksempel på at vise det med følgende:  
![image alt text](Udklip4.PNG)  
Man går tilbage i path 4 gange med ../, så man til sidst befinder sig i / folderen. Derefter er der skrevet /etc/passwd, for at kunne tilgå en passwd filen, som gerne skulle indeholde nogle kodeord til forskellige brugere.  

Dette er det primære eksempel jeg har arbejdet med, og derudover har jeg arbejdet med forskellige måder der bliver input valideret, og hvordan man kan bryde dette,  
og dermed stadig lave File Inclusion.  

Et enkelt eksempel på dette kunne være task 5 - lab 3 ved file inclusion.  
Her fortæller en error, at filen skal være en .php type fil, hvor jeg så prøver at ombryde denne input validering:  
![image alt text](Udklip5.PNG)  


næste underemne er SSRF.  
SSRF står for Server-Side Request Forgery.  
Angrebet omhandler at man sender request til en server.  
Her kan der være to typer angreb:   
-	data bliver returneret til hackeren.
-	Blind SSRF - angrebet foregår, men det bliver ikke returneret noget til hackeren.

Uden at gå for meget i dybden SSRF, så vil jeg bare vise et eksempel for det. Resten kan selvfølgelig læses i google docset.  
![image alt text](Udklip6.PNG)  
![image alt text](Udklip7.PNG)  
Her ender jeg ud med at bruge directory traversal fra forrige underemne til at jeg rent faktisk udfører en SSRF angreb.  
Hvis man kigger i page source efterfølgende, så vil informationer fra path /private være lagt ind "encoded" i base64 format, og man har dermed lavet  
et request af noget data, som man ikke burde have adgang til.  

Næste underemne er Cross-Site Scripting  
Her handler det om, at man gerne vil have lagt et javascript script over på en anden computer, hvor det så bliver executet, og udfører et eller andet.  
I de eksempler jeg har arbejdet med har man bare brugt XSS payload script, som laver en pop up box med alert:  

![image alt text](Billede12.png)  
Men det kan også være farlige scripts, som f.eks at man stjæler login tokens gennem cookies:
![image alt text](Billede13.png)  
Eller en keylogger, som onfanger alt hvad en bruger indtaster gennem deres keyboard på deres pc:  
![image alt text](Billede14.png)  




