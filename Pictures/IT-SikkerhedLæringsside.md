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





