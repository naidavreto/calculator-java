Zbirni LOC: 153 LOC (calculator.java + start.java) + 19 LOC (licence) 



*****Calculator.java*****
	
	LOC 134

	Broj čvorova (n): 34
	Broj bridova (e): 40
	
	C=E-N+2=40-34+2=4
	Ciklomatska složenost iznosi 4.

	U vezi s kognitivnom složenošću, možemo primijetiti da metoda evaluateExpression ima nekoliko grananja i petlji koje bi mogle otežati čitanje i razumijevanje koda. Također, metoda Calculate ima mnogo grananja, što također može povećati kognitivnu složenost.

	Statička analiza:
		
		Linije 8-19: Definisana je unutrašnja statička klasa `Operations`, koja sadrži konstante za matematičke operacije, kao što su sabiranje, oduzimanje, množenje i dijeljenje. Ove konstante su označene ključnom rječju "final", što znači da im se vrijednosti dodjeljuju samo jednom i ne mogu se kasnije promijeniti. Klasa Operations ima privatni konstruktor.Ovo je čest pristup kada se želi obezbjediti da se klasa koristi samo za grupisanje konstanti ili metoda, a ne za kreiranje objekata.

		Linije 21-27: Metoda ToString u klasi Operations vraća simbole operacija u stringu. Ova je malo konfuzno jer obično metode koje vraćaju string sačinjen od različitih vrijednosti koriste naziv kao toString.
		
		Linije 29-53: Metoda `Run` samo poziva `evaluateExpression` sa zadatim izrazom. Ako `Run` ne obavlja dodatne operacije, može se direktno pozvati metoda `evaluateExpression`.

		Linije 89-139: Metoda Calculate vrši izračunavanje rezultata na osnovu operacija i brojeva.

Kod sadrži mnogo blokova koda koji se ponavljaju u `Calculate` metodi.

Code Smells:

1. Statička promjenljiva `finalResult`: Statičke promjenljive se često izbjegavaju, posebno ako nisu potrebne. Treba koristiti lokalne promjenljive unutar metoda gdje je to moguće.
2. Korištenje Stringa za matematičke operacije: Metoda `ToString` u unutrašnjoj klasi `Operations` vraća string koji predstavlja simbole matematičkih operacija. 
3. Dugačke metode: Metoda `evaluateExpression` i `Calculate` su relativno duge i složenešto otežava održavanje i razumjevanje koda.
4. Nepotrebno korištenje `ToSting`
5. Nesigurna upotreba `try-catch` bloka: U metodi `evaluateExpression` koristi se `try-catch` blok bez preciznog navođenja izuzetaka koji se hvataju. Treba specificirati izuzetke.
6. Nekonzistentna upotreba zagrada u kontrolnim strukturama: U nekim dijelovima koda, nema zagrada oko blokova koda u `if` i `else` konstrukcijama, što može dovesti do problema sa čitljivošću i potencijalno uvođenje grešaka.


*****Start.java*****

	LOC 19

	Broj čvorova (n): 3
	Broj bridova (e): 2
	
	C=E-N+2=2-3+2=1
	Ciklomatska složenost iznosi 1.

	Program je jednostavan, sa jednom petljom i jednim grananjem što znači da će kognitivna složenost biti niska upravo zbog jednostavnosti strukture i logike.

	Statička analiza:
	
		Linija 3: `String Expression;`Varijabla `Expression` je deklarisana, ali trenutno nema vrijednosti. Može dovesti do potencijalne NullPointerException greške.

		Linije 5-10: Unutrašnja petlja `while (active) { ... }`Kod unutar ove petlje zahtjeva unos korisnika i obradu unosa dok korisnik ne unese "exit". Ovo djeluje ispravno, sve dok korisnik ne unese nešto što nije validan izraz.
	
		Linija 7: Scanner scanIn;` Varijabla `scanIn` se deklariše unutar petlje. Deklaracija izvan petlje neće dovoditi do ponovnog kreiranja skenera u svakoj iteraciji petlje.

Ovaj kod djeluje ispravno i obavlja očekivane funkcionalnosti. Međutim, postoji nekoliko mjesta gdje se može dodati provjera kako bi se poboljšala robusnost i rukovanje potencijalnim greškama. 

Code Smells:

1. Linije 9-19: Otvaranje novog Scanner-a unutar petlje se može izbjeći kreiranjem objekta Scanner jednom izvan petlje i ponovo ga koristiti.
