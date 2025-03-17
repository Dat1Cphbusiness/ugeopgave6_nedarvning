### Træn nedavning med disse tre opgaver. 

Task 1 og 2 træner hvad du lærte til mandagslektionen. Task3 kan du kaste dig ud i _efter_ du har forberedt dig til onsdagslektionen.
[Se Forberedelse til onsdag](https://dat1cphbusiness.github.io/content/inheritance/#onsdag)

## Task 1: Butik med produkter
Her skal vi arbejde med en klasse der nedarver fra en anden. I dette program som skal bruges i en butik, findes der produkter og så findes der produkter som har en udløbsdato( som regel mad og drikkevarer)
I programmet vil vi gerne behandle alt som et produkt, men madvarer har alligevel lige lidt ekstra, som vi også godt vil tage hånd om.

**Emner:** super, LocalDate, instanceOf, downcasting, polymorfi

1.a Start et projekt med en Main klasse, hvori du har main metoden

1.b Lav en klasse Product, med felterne price og name. Lav også en konstruktør og en toString-metode.

1.c Lav en klasse Perishable, som nedarver fra Product og har et felt bestBefore. Typen på dette felt skal være LocalDate.

 <details>
        <summary>
             Hint
 </summary>
Har du aldrig brugt LocalDate datatypen?
Ofte sætter man sig først ind i en datatype når behovet opstår. 
Her kan man vælge enten at slå datatypen op i <a href="https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html">Java API dokumentationen</a> eller man kan lave en generel søgning og finde en forklaring, måske med nogle gode eksempler.
    </details>  

1.d Perishable skal der være en konstruktor som tager price, name og bestBefore som parametre. De to første skal sendes videre til super konstruktoren, mens den sidste skal assignes lokalt.
  <details> 
        <summary> Hint</summary>
  Læs om super og se hvordan man kalder super klassens konstruktor <a href="https://www.baeldung.com/java-super">her</a>.
   </details> 

1.e I main metoden, lav 2 objekter af typen Product. Det kan være objekter der repræsenterer en stol og en T-shirt.
Tilføj så et objekt af typen Perishable, som repræsenterer en plade chokolade. Lad referencen være af typen Product.

<details> 
        <summary> Hint</summary>
            Konstruktoren til Perishable forventer en dato. Derfor er du nødt til først at lave en dato instans som du kan sende med som argument til konstruktoren. Det gør du sådan her:

<code>LocalDate date = LocalDate.of(2026, 4, 1);</code>

Læs mere om <a href="https://www.baeldung.com/java-creating-localdate-with-values">custom dates</a>
</details> 


1.f I main metoden skal du nu printe hver af de tre objekter ud, gennem implicit kald til deres toString metode.
Forventet output:
```
Stol: 1099kr.
T-shirt pris: 299kr. 
Chocolade pris: 33kr.
```


<details> 
        <summary> Hint</summary>
         Et implicit kald til et objekts konstruktor kan ske ved blot at give referencen til objektet som argumentet til println metoden:

<code>System.out.print(product1)</code>
(println metoden vil kalde objektets toString metode for dig)
</details> 



1.g For at få udløbsdatoen på chokoladen med, skal du overskrive toString metoden i Perishable klassen.
I din definition af toString i Perishable klassen, kan du starte med at hente outputtet fra super klassens version af toString metoden. Kald den med
<code>
String s = super.toString()
</code>

Til ```s``` kan du nu tilføje udløbsdatoen, før ```s``` returneres.

Test igen. Forventet output

``` 
Stol: 1099kr.
T-shirt pris: 299kr. 
Chocolade pris: 33kr. Mht: 01.04 2026
```

---------

_Hvis du undrer dig over at referencen til chokolade objektet ikke bare kunne være Perishable når nu det er en Perishable, er det et godt tegn. Du tænker rigtigt.
Det er dog svært at forklare hvorfor ligenu, fordi det bliver først relevant når programmet er lidt mere udviklet.
Helt kort kan man sige at det er fordi vi nogle gange har brug for at kunne **erklære** referencen uden at vi ved hvilken specifik type der skal **instantieres**._

---------
1.h For at lege lidt med betydningen af referencens datatyper, så lad os tilføje en metode til Perishable. Kald den isAfterBestBefore(). Metoden skal returnere true hvis den dato vi har nu, er efter produktets udløbsdato.

<details> 
        <summary> Hint</summary>
Du skal kigge på <code>LocalDate.now()</code> og <code>date.isAfter()</code> 
   </details> 

1.i I main metoden kan du prøve at kalde den nye metode du har lave på den Product instans der repræsenterer chokoladen. Det kan ikke lade sig gøre. Hvorfor mon?

Det er fordi referencen er Product, og derfor kan man ikke kalde metoder og felter som kun er i Perishable, heller ikke selvom objektet jo ER af type Perishable.
Løsningen er **ikke** bare at lave referencen om til Perishable. Løsningen er at tjekke om en _instans_ (ikke at forveksle med _referencen_) er af en bestemt type, downcaste referencen til den type, og dernæst kalde metoden.

Analyser dette eksempel, indtil du helt forstår hvad der sker.
Prøv så om du kan overføre det til din kode, sådan at du får testet din nye metode i Perishable.

```java
Animal a = new Dog()         //reference of type superclass, but actual instance of type subclass  
        
    if(a instanceof Dog){    //using the instanceOf operator 
        
         Dog d = (Dog) a;    //downcasting  
         d.wagTail();        // calling the special subclass method
}
```



## Task 2: Skole med roller
Her skal vi arbejde med tre klasser hvor to konkrete klasser arver fra en tredje abstrakt klasse.

**Emner:** Nedarving og lister, instanceOf og downcasting, abstract og polymorfi

2.a Lav en klasse Person, med feltet name. Lav også en konstruktør og relevant getter- og setter-metode. Lav derudover metoden boolean addCourse(String course). Metoden skal ikke gøre noget, så du kan lade den returnere true og ikke gøre andet (en dummy-metode).

EKSTRA: Den korrekte Java-måde at lave en metode, der ikke gør noget, er dog at gøre den abstract, så det kan du gøre i stedet hvis du vil. Hvis du vælger at lade metoden være abstract, skal du også lade klassen være abstract. En abstract metode har ingen {} men skrives sådan: public abstract boolean addCourse(String course);

2.b: Lav to klasser Student og Teacher, som arver fra Person. Lav konstruktører til klasserne, som kalder Persons konstruktør ved at bruge keywordet super().
  <details> 
        <summary> Hint</summary>
  Læs om super og se hvordan man kalder super klassens konstruktor <a href="https://www.baeldung.com/java-super">her</a>.
   </details> 


2.c Lav to ArrayList<String> i Student kaldet passedCourses og currentCourses. Lav to ArrayList<String> i Teacher kaldet canTeach og currentCourses. Lav om i konstruktørerne, så der skal gives en ArrayList<String> passedCourses eller canTeach med som parameter, når objektet oprettes.

2.d Override metoden addCourse i Student. Når metoden bliver kaldt, skal du sikre, at kurset ikke ligger i den studerendes passedCourses-ArrayList, da en studerende ikke kan tage kurser, som allerede er bestået én gang. Hvis den studerende ikke tidligere har bestået kurset, lægges det i currentCourses. Lad metoden returnere true eller false alt efter om kurset blev tilføjet til currentCourses.

 <details>
        <summary>Hint </summary>
         Se om ikke <a href="https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html">ArrayList</a> har en metode, der kan hjælpe dig med opgaven.
 </details> 

2.e Override metoden addCourse i Teacher. Når metoden bliver kaldt, skal du sikre, at kurset ligger i underviserens canTeach-ArrayList, da underviseren skal være kvalificeret til at undervise for at blive sat på kurset. Hvis underviseren er kvalificeret, lægges kurset i currentCourses. Lad metoden returnere true eller false alt efter om kurset blev tilføjet til currentCourses.

2.f Lav en klasse Main med en main-metode, hvor du tester Student og Teacher. Du skal oprette et antal studerende og et antal undervisere og give dem ArrayLists af Strings (beståede kurser til de studerende og canTeach-kurser til underviserne). Gem alle dine objekter i en ArrayList<Person> persons.

2.g Kør din persons-liste igennem med en for-løkke og tilføj kurset "Java 1.0" til dem alle (sørg for at nogle af dine studerende allerede har bestået dette og andre ikke har, samt at nogle af underviserne er kvalificerede til at undervise i det og andre ikke er). Hver gang ét af dine kald til addCourse() returnerer false, skal du printe navnet på den studerende eller underviseren. Hvis det er en Student skal du også printe " har allerede bestået dette kursus." og hvis det er en Teacher skal du også printe " kan ikke undervise i dette fag".
 <details>
        <summary>Hint </summary>
        For at finde ud af om der er tale om et Student-objekt eller et Teacher-objekt, skal du bruge instanceof. 
         </details> 



## Task 3: Gæt et tal med 2 slags spillere

**Emner:** Interface, polymorfi

3.a Skriv et interface der hedder Player, og som indeholder metoden `int guessANumber(int min, int max)`.

3.b Skriv to klasser som hver især implementerer dette interface:HumanPlayer og ComputerPlayer

3.c I HumanPlayer skal `guessANumber` implementeres sådan at brugeren bliver bedt om at taste et tal mellem `min` og `max` i konsollen. Metoden skal returnere det tal spilleren har tastet.

3.d I ComputerPlayer skal `guessANumber` implementeres sådan at 'gættet' genereres ved brug af Random. Igen skal tallet returneres.

3.e Skriv en main-metode, hvor du genererer et tilfældigt tal, som er det der skal gættes.

3.f instansierer både en ComputerPlayer og en HumanPlayer og kald `guessANumber` på dem én ad gangen, hvor du efter et gæt evaluerer om det var for højt eller for lavt.

3.g Fortsæt med at kalde de to spilleres `guessANumber` metoder, indtil der kan udnævnes en vinder.




