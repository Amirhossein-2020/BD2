Classi: identificati da almeno un identificatore artificiale, abbiamo una classe se solo se vogliamo rappresentare dati su un concetto
	Hanno delle proprietà:
		statiche(attributi: default cardinalita' [1..1] e associazioni: default molteplicità [0..*]): devono essere cambiati esplicitamente da utenti
	Vanno specificati 
		dinamiche(operazioni): i cui valori possono essere calcolati a partire dai valori di altre proprietà automaticamente ogni volta che servono
			o possono essere cambiamenti dei valori di attributi o link(stato dell'oggetto)
			nome_operaz(arg1:Tipo1, arg2:Tipo2, arg3:Classe, self:Classe(solo per operazioni di classe ed e' implicito e omesso)):tipo_ritorno
				tipo_ritorno e tipo di argomenti possono essere tipi concettuali oppure classi di diagramma, possono anche non avere alcun ritorno

Associazioni: sono identificati dal proprio nome e la coppia di oggetti associati(identificati tramite i loro identificatori univoci sia artificiali che reali) rappresentano la possibilita' di un link tra istanze delle coppie senza identificatori espliciti, nessuna coesistenza
	Classi di associazioni: associazzioni con attributi con ulteriori associzioni o relazioni is_a e generalizzazioni (non cambia la natura di associazioni)

Tipi di dati:
	Base: Intero, Reale, Data, Ora, DataOra, Stringa, Booleano
	Specializzati:	intervalli: 18..20
		maggiore/minore /uguale: >,<,>=,<=
Vanno specificati:
	Enumerativi: per tipi di dati dicreti, finiti, piccoli: Dom: enum{simbolo1, simbolo2}
	Composti(Record): Dom: record(etichetta1: tipo1, etichetta2: tipo2)

Vincoli di integirta': Ulteriori restrizioni sul livello estensionale ammesso(insieme degli oggetti e link coesistibili)
	Vincolo di molteplicità sui ruoli delle associazioni
	Vincolo di molteplicità sui valori degli attributi (forse non sia di tipo integrita')
	Vincolo di identificazione di classe: non possono coesistere due oggetti diversi che coincidono in valore di un insieme di attributi che sono connessi agli stessi oggetti di alter classe tramite link, puo' essere applicato solo agli attributi a molteplicità [1..1] e associazioni a molteplicità [1..1]
	Vincoli esterni	
	
Generallizazzioni e is_a: ereditamento o/e specializzazione(restrizione dei tipi) di proprietà statiche e dinamiche della superclasse
	specializzazione degli attributi: dominio di attributo nella sottoclasse deve essere un sottoinsieme del corrispondente attributo nella superclasse
	specializzazione delle operazioni: la segnatura deve essere compatibile, stesso numero e tipo di argomenti e il dominio di ritorno piu' ristretto
	specializzazione nelle classi di associazioni: il tipo di sottoclasse di associazione deve essere compatibile con quella superclasse anche le sue molteplicità: m_sup <= m_sott <= M_sott <= M_sup
	generalizzazione tra attori: B->A: l'attore B puo' fare le veci dell'attore A e ne eredita tutte le use-case
	generalizzazione tra use_case: B->A: alcune funzionalità di A possono sono rimpiazzate con le funzionalità di B

Use-case: le funzionalità (in modo generale ma non tutte) del Sistema che coinvolge piu' classi e associazioni, insieme omogenee di funzionalità accedute da un insieme omogeneo di utenti, quando c'e' un arco tra un attore e un use-case significa che tale attore puo' accedere a tutte le funzinalità dentro quel use-	case
	dipendenze tra use_case: 
		A <<include>> B, alcune funzionalità di A possono usare alcune funzionalità di B 
		B <<extend>> A, alcune funzionalità di A sono estese con le funzionalità di B

Documenti di specifica:
	Tipi di dato:
	una classe: per ogni operazione della classe, cosa calcola e se e come cambia livello estensionale
		pre-condizioni su: oggetto di invocazione, valori degli argomenti, altri oggetti del sistema, che devono essere soddisfatte affinche' l'opeazione possa essere invocate
		post-condizioni definizioni di: valore di ritorno, modifiche al livello estensionale
	uno use-case: definisce insieme delle operazioni dello use-case e il resto come operazioni della classe
	vincoli esterni: regole del dominio applicativo per alta qualità dei dati (business rules) che non sono esprimibile tramite diagramma, definiti cosi:
		identificatore univoco: [V.classi_a_cui_il_vincolo_si_applica.nome_vincolo]
		asserzione matematica che definisce condizioni che devono essere soddisfatte per un livello estensionale legale


Sintassi:
	1. Linguaggio dei termini: denotano oggetti di intresse induttivamente sulle funzioni(caso induttivo) e variabili(caso base)
	Simboli apparteneti all'alfabeto di linguaggio:
		V: simboli di variabili
		F: simboli di funzione con numero di arità(argomenti) f/k; simbolo di costante: arità 0, zero/0, succ/1; f(var1, term2) 

	2. Linguaggio delle formule(FOL): induttivamente sui connettivi, quantificatori, simboli speciali(caso induttivo) e predicate(caso base), Sequenze finite validi di simboli(formule):
		P: simboli di predicato con numero di arità p/k; contiene predicato di ugualianza di arità 2 "=", doppio/2, Somma/3; p(termin1, termin2)
		{¬, ∨, ∧, →, ↔}: connettivi logici; p1 □ p2, ϕ □ ψ 
		{∀, ∃}: quantificatori; □ var ϕ, formula chiusa(TQBF): formula con tutte le variabili quantificate, S non gioca alcun ruolo!
		{"(", ")", ","}: simboli speciali

Semantica: M,S |= ϕ m modello di ϕ sse eval[I, S](ϕ) = true ma per formule chiuse M |= ϕ sse eval[I, S](ϕ) per qualsiasi S	
	valida: se ϕ e' vera per ogni I e S, insoddisfacibile: se ϕ e' falsa per ogni I e S ϕ, soddisfacibile se ϕ e' vera se esiste una I ed una S
		0. Definire D: insieme finite o infinito degli oggetti del mondo(dominio di interpretazione)
	Valutazione con 2 nozioni:
		1. dei termini: pre-eval[preNAT, S] : T -> D, T insieme di tutti termini producibili da V, F
			1.1. dei termini atomici:
				Pre-interpretazione: corrispondenza dai simboli della funzione in F alle funzioni totali su D: 
					pre-eval[preNAT, S](c) = preNAT(c)
					preI/preNAT : F -> (D^k -> D) : preI/preNAT(f/k) = f(k)
				Assegnamento di variabili: funzione separata da ma per pre-iterprerazione dalle variabili agli elementi di D;
					pre-eval[preNAT, S](X) = S(X)
					S/W : V -> D : S/W(X)=d
			1.2. dei termini complessi(predefinita): induttivamente
					pre-eval[preNAT, S](f(t1, ..., tk)) = preNAT(f)(pre-eval[preNAT, S](t1), ..., pre-eval[preNAT, S](tk))
		2. delle formule: eval[NAT, S] : ϕ -> {true, false}, ϕ insieme di tutte le formule producibili da V, F, P
			2.1. delle formule atomiche: funzione I che da significato(interpretazione, valore true o false) alle formula atomiche(predicati con argomenti tutti termini, lettere proposizionali), I |= ϕ sse ϕ e' vera nell'interpretazione I; consiste di 2 parti:
				2.1.1. preI
				2.1.2. una corrispondenza da simboli di predicato a relazioni su D:
					eval[NAT, S](p(t1,...,tk)) = NAT(p)(pre-eval[preNAT, S](t1), ..., pre-eval[preNAT, S])
					NAT/I: P -> R ⊆ D×···×D : NAT/I(p)={(d1,d2, ..., dk) | di ∈D}      

			2.2. delle formule complessi(predefinita): usando le regole si stabilisce il significato di formule piu' complesse(contenente: connettivi, quantificatori, simboli speciali) induttivamente 
				eval[preNAT,S](ϕ → ψ) = eval[preNAT,S](¬ϕ∨ψ)
				eval[preNAT,S](ϕ ↔ ψ) = eval[preNAT,S]((ϕ→ψ)∧(ψ→ϕ))
				eval[preNAT,S](∃V ϕ) = true se esiste d ∈ D t.c. eval[preNAT,S[V/d]](ϕ) = true
					= false altrimenti
				eval[preNAT,S](∀V ϕ) = true se per ogni d ∈ D vale eval[preNAT,S[V/d]](ϕ) = true
					= false altrimenti
				Ordine di precedenza: 1. "()"	2. ¬	3. ∧, ∨	    4. ∀, ∃	5. →

Vogliamo far diventare tutto il diagramma delle classi e vincoli esterni diventino un formulone Φ soddisfacente i requisiti che restringe l'insieme dei modelli possibili(che definiscono tutti e soli livelli estensionali legali), la Semantica del Mondo Reale impone alle interpretazioni M di fissare l’interpretazione di tutti i simboli (di predicato e di funzione) in modo consistente con la realtà, ad eccezione dei simboli di predicato(valutati da utente) per: 1. classi 2. associazioni 3. attributi 4. operazioni

Alfabeto: oltre a connettivi, quantificatori, connettori e simboli speciali sono univocamente definiti gli insiemi:
	P := per ogni modulo nel diagramma delle classi(classi, associazioni, attributi, domini, operazioni di classe) e per ogni operazione use-case nel documento di specifica di ogni use-case nel diagramma use-case
	F := per ogni operazione che opera sui valori dei domini in generale operaioni matematiche 

	L'estensione di un simbolo di predicato sara' tutte e sole istanze appartenenti a M(p), dato M interpretazione(livello estesnionale legale) che modella Φ
	Se usassimo simbolo di funzione per attributi non possiamo rappresentare attribuiti multivalori
	Dom_comp = record(f1:Dom1, ..., fn:Domn) un dominio composto da n field

	P = {=/2, >/2, </2, >=/2, <=/2, C/1, Dom/1, attr/2[attr(c, d)], assoc/2[assoc(ruolo1:c1,ruolo2:c2) ordine alfabetico dei ruoli], attr/3[attr(c1,c2,v)], "Dom_spec"/1[Dom(d) ^ "Dom_spec"(d)], Dom1/1, ..., Domn/1, f1/2, ..., fn/2,  Dom_comp/1[Dom_comp(d) ^ Dom1(d1) ^ ... ^ Domn(dn) ^ f1(d, d1) ^ ... ^ fn(d, 	dn)], operaz_c_Dom1_..._Domn/(n+2)[operaz_c_Dom1_..._Domn(c, d1, ..., dn, dr) per overloading bisogna rappresentare operazioni omonime con simboli di predicato diversi mettendo tipi di argomenti e classe di invocazione nella segnatura], Intero/1, Reale/1, Stringa/1, Data/1, Ora/1, DataOra/1, h/2, m/2, s/2, "0..59"/1, "0..23"/1, anno/2, mese/2, giorno/2, "0..2025"/1, "1..12"/1, "1..31"/1} 
infatti qua definiamo solo gli elementi di P ma non contiene nessuna logica che domini le relazioni tra questi elementi


	F = {+/2, -/2, */2, //2, ||/2, sqrt/1, pow/2, log/1, len/1(funzioni standard aritmetiche + su stringhe), 0, 1, ....,(costanti che denotano elementi dei domini) "uomo", "donna"(valori per domini enumerativi), adesso/0(una istanza del dominio DataOra}

Vincoli sui livelli estensionali ammessi:
1. Disgiunzioni sulle classi e domini:
∀x A(x) →¬B(x):  non c'e' bisogno di scrivere la direzione contraria perche' già per contronomiale e' vero che ∀x B(x) → ¬A(x)
	- Due classi diverse non appartenenti ad uno stesso DAG di generalizzazioni: ∀x B(x) → ¬C(x)
	- Due classi diverse appartenenti ad uno stesso DAG di generalizzazioni tali che il cammino che le congiunge passa per due classi figlie di una generalizzazione {disjoint}: ∀x A(x)→¬B(x)
	- Due domini diversi semanticamente disgiunti: ∀x Intero(x) → ¬Stringa(x)
	- Una qualunque classe e un qualunque dominio: ∀x A(x) → ¬Dom(x)
2. Relazioni di sottoinsieme tra classi e tra associazioni:
	- Le istanze di una classe figlia di una generalizzazione sono anche istanze della classe base: ∀x B(x) → A(x)
	- Le istanze di una associazione figlia di una generalizzazione sono anche istanze dell’associazione base: ∀x,y s(x,y) → r(x,y)
3. Generalizzazioni complete tra classi{Complete}: ∀x C(x) →E(x) ∨ F(x) ∨ G(x)
4. Specializzazione di domini: ∀x dom_spec(x) ←→ [dom(x) ∧ “x soddisfa il criterio di specializzazione”]
5. Tipizzazione di associazioni tra due classi: ∀c1, c2 assoc(c1, c2) → C1(c1) ∧ C2(c2), cioe' gli elementi dell'estensione sono gli elementi del prodotto cartesiano tra M(C1) x M(C2)
6. Tipizzazione di attributi delle classi e delle associazioni:
	- ∀c, v attr(c, v) ∧ C(c) → dom(v): diverse classi e diverse associazioni possono avere attributi omonimi su domini potenzialmente diversi, pero' non e' possible tra classe figlia e padre
	- ∀c1, cn, v attr(c1, c2, v) ∧ assoc(c1, c2) → dom(v)
7. Vincoli di cardinalità: 
	- sui ruoli delle associazioni:
		- Vincolo di cardinalità minima (solo se > 0):
			∀c1 C1(c1) → ∃c2^(1), ..., c2^(min2) c2^(1) != c2^(2) ∧ · · · ∧ c2^(min2-1) != c2^(min2) ^ assoc(c1 , c2^(1)) ∧ · · · ∧ assoc(c1 , c2^(min2)) 
			∧
			∀c2 C2 (c2) → ∃c1^(1), ..., c1^(min1) c1^(1) != c1^(2) ∧ · · · ∧ c1^(min1-1) != c1^(min1) ^ assoc(c1^(1) , c2) ∧ · · · ∧ assoc(c1^(min1), c2)
		- Vincolo di cardinalità massima (solo se != ∗):
			∀c1 C1(c1) → ¬∃c2^(1) ,..., c2^(max2+1) c2^(1) != c2^(2) ∧ · · · ∧ c2^(max2) != c2^(max2+1) ^ assoc(c1 , c2^(1)) ∧ · · · ∧ assoc(c1 , c2^(max2+1))
			∧
			∀c2 C2(c2) → ¬∃c1^(1), ..., c1^(max1+1) c1^(1) != c1^(2) ∧ · · · ∧ c1^(max1)!= c1^(max1+1) ^ assoc(c1^(1), c2) ∧ · · · ∧ assoc(c1^(min1+1), c2)
	- sugli attributi di classi:
		- Vincolo di cardinalità minima (solo se min > 0):
			∀c C(c) → ∃v^(1), ..., v^(min) v^(1) != v^(2) ∧ · · · ∧ v^(1) != v^(min) ∧ · · · ∧ v^(min−1) != v^(min) ∧ attr(c, v1) ∧ · · · ∧ attr(c, v^(min))
		- Vincolo di cardinalità massima (solo se max != ∗):
			∀c C(c) → ¬∃v^(1), ..., v^(max+1) v^(1) != v^(2) ∧ · · · ∧ v^(1) != v^(max+1) ∧ · · · ∧ v^(max) != v^(max+1) ∧ attr(c, v^(1)) ∧ · · · ∧ attr(c, v^(max+1))
	- sugli attributi di asociazioni:
		- Vincolo di cardinalità minima (solo se min > 0):
			∀c1, c2 assoc(c1,c2) → ∃v^(1), ..., v^(min) v^(1) != v^(2) ∧ · · · ∧ v^(1) != v^(min) ∧· · ·∧ v^(min−1) != v^(min) ∧ attr(c1,c2,v^(1)) ∧· · ·∧ attr(c1,c2,v^(min))
		- Vincolo di cardinalità massima (solo se max != ∗):
			∀c1, c2 assoc(c1,c2)→¬∃v^(1),...,v^(max+1) v^(1) != v^(2)∧· · ·∧v^(1) != v^(max+1)∧· · ·∧v^(max) != v^(max+1) ∧ attr(c1,c2,v^(1))∧· · ·∧attr(c1,c2,v^(max+1))
8. Tipizzazione di operazioni:
	- delle classi:
		∀c, v1,..., vn, vr op[C, T1, ...,Tn](c, v1, ..., vn, vr) → C(c) ∧ T1(v1) ∧ ··· ∧ Tn(vn) ∧ Tr(vr)
	- delle associazioni:
		∀c1, c2, v1, ..., vn, vr op[assoc, T1, ..., Tn](c1, c2, v1, ..., vn, vr) → assoc(c1, c2) ∧ T1(v1) ∧ ··· ∧ Tn(vn) ∧ Tr(vr)
9. Vincoli di identificazione di classe: per ogni vincolo di identificazione {id}:
¬∃c, c′, v1, ..., vn, c1, ..., cm C(c) ∧ C(c′) ∧ c != c′ ∧ attr1(c, v1) ∧ · · · ∧ attrn(c, vn) ∧ attr1(c′, v1) ∧ · · · ∧ attrn(c′, vn) ∧ assoc1(c, c1) ∧ · · · ∧ assocm(c, cm) ∧ assoc1(c′, c1) ∧ · · · ∧ assocm(c′, cm)

operazioni: segantura
	pre-condizioni(π): condizioni sugli argomenti e sul livello estensionale del sistema che devono valere all’avvio dell’esecuzione dell’operazione, affinché il suo comportamento sia definito
		Input: Un livello estensionale come un modello M-in di Φ ∧ ξ1 ··· ∧ ξn che soddisfa la Semantica del Mondo Reale, valori per arg(variabili libere)
		¬p(x, y) se x e y vengono dati come argomenti e la condizione e proprio su queste istanze pero' se dovessimo controllare la condizione su altre istanze dovremmo introdurre nuove variabili con le corrispettive quantificatori
	post-condizioni(ρ): condizioni sul livello estensionale del sistema che devono valere al termine dell’esecuzione dell’operazione (nel caso questa faccia side-effect) e definizione dell’eventuale valore di ritorno
		Output: Un nuovo livello estensionale come un nuovo modello M-out di Φ ∧ ξ1 ···∧ ξn che soddisfa la Semantica del Mondo Reale, ed un eventuale valore di ritorno
		Modifica del Livello Estensionale dei Dati:
			Nuovi elementi del dominio di interpretazione: per nuove istanze delle classi o domini
			Elementi del dominio di interpretazione che non esistono più:
			Nuove ennuple di predicati: Alla relazione che interpreta il predicato x viene aggiunta la coppia (u,v) oppure x(u,v)
			Ennuple di predicati che non esistono più:
			Valore di Ritorno: result = 

Il soddisfacimento delle precondizioni π deve garantire che M-out |=Φ ∧ ξ1 ··· ∧ ξn e che quindi è ancora un livello estens. legale dei dati.
M-out è uguale ad M-in se l’operazione non ha side-effect sui dati

Estensione del FOL(SOL):
1. Insiemi (di assegnamenti di variabili):
	Un insieme è definito a partire da una formula FOL φ aperta e consiste in tutte e sole le assegnazioni alle variabili libere di φ che rendono la formula vera.
	Se l’operazione fa side-effect, specifichiamo, per ogni definizione di insieme, se φ va interpretata sul livello estensionale all’inizio o al termine dell’esecuzione dell’operazione.
2. Operazioni insiemistiche (∩, ∪, -, etc.)
	 ∪B∈A B: dove A è un insieme di insiemi
	 ∩B∈A B: dove A è un insieme di insiemi
3. Funzioni su insiemi (come Sigma, | |, Pi, etc.):
	∏(a1,...,an)∈A ψ(a1,...,an): la funzione valuta al prodotto dei valori ψ(a1,...,an) per tutte le ennuple (a1,...,an) nell’insieme A.
	∑(a1,...,an)∈A ψ(a 1 ,...,a n ): la funzione valuta alla somma dei valori ψ(a1,...,an) (per una qualche funzione ψ) per tutte le ennuple (a1,...,an) nell’insieme A (insieme di n-ple).
        Argmax(a1,...,an)∈A  (at) prendi la tupla che ha Valore massimo per campo at
	| |: la funzione può essere riscritta come:  Sigma(a1,...,an)∈A   1 (come somma di un 1 per ogni ennupla di A).
4. Ordinamento:
	sorted(elem : T [0..*]) : (elem : T, pos : Intero > 0) [0..*] 
		tipi multivalori
		tipo di argomento T è una classe o dominio
		tipo di ritorno è anonimo composto da due campi, possiamo anche dargli un nome e definirlo separatamente nel documento 
		ordinamento non sara unico quando ci sono due elementi uguali per nostro criterio
		criterio dell'ordinamento:
			per tipi di dato naturalmente ordinati(tipi di base) basta sfruttare <=
			nel caso piu' generale: definiamo una operazione ausiliaria T<=(a: T, b: T): Booleano
				pre-condizione: 
				post-condizione: true sse a <= b
	pre-condizioni: o nessuna o in base al criterio dell'ordinamento possiamo condizionare i valori dei parametri o/e il livello estensionale tali che siano ordinabili
	post-condizioni:
		ins ⊆ T
		O := insieme di tutti e soli gli ordinamenti(insiemi di coppie) corretti dei valori dell'argomento di input secondo il criterio, 
			{ins_ord | ins_ord ⊆ ins × 1..|ins| ^ 1 ^ 2}:
				1.  Ogni elemento di ins deve comparire esattamente una volta in ins_ord:
					- ∀o o ∈ ins → ∃i (o, i) ∈ ins_ord
					- ∀o o ∈ ins → ¬∃ i1, i2 i1 != i2 ∧ (o, i1) ∈ ins_ord ∧ (o, i2) ∈ ins_ord (funzione)
					- ∀i (Intero(i) ∧ 1 ≤ i ∧ i ≤ |ins|) → ∃o (o, i) ∈ ins_ord (suriettiva) e iniettivita viene implicata automaticamente perche' dominio e codominio sono della stessa 						cardinalita'
				2. Criterio: ∀o1, o2, i1, i2 (o1, i1) ∈ ins_ord ∧ (o2 , i2) ∈ ins_ord ∧ i1 ≤ i2 → T≤(o1, o2) = true
		result ∈ O 

	o semplicemente definiamo solo il criterio T<= e delegandogli le precondizioni e lasciando il resto gestito automaticamente dalla famiglia sorted definta per ogni classe e dominio:
	sorted T, T<=  (elem : T [0..*]) : (elem : T, pos : Intero > 0) [0..*]

Progettazione di basi di dati relazionali:
2. Schema relazionale(insieme di tabelle) della base dati tenendo conto di tutti i vincoli e dei requisiti di performance(id artificiali) a partire dal diagramma delle classi ristrutturato:
	2.1 Diagramma ristrutturato delle classi c'ha solo le classi le cui istanze vanno memorizzate nel DB viene costruita da una sequenza di passi:
		2.1.1 Eliminazione di attributi multivalore: quindi rimangono solo [0..1] o [1..1]
			Creare una nuova classe le cui istanze rappresentano i valori del tipo di dato effettivamente utilizzate nel livello degli oggetti e link(ecco perche' 1..*): attr[X..Y]
			C 1..* - attr - X..Y NomeArbitrariotipo con attributo valore{id}: Tipo; id perche' non vogliamo rappresentare lo stesso valore piu' volte
		2.1.2 Sostituzione dei tipi di dato concettuali con opportuni tipi supportati da SQL (tipi base o definiti dall’utene) nello schema stesso:
			Tipi base:
				Stringa -> varchar(maxlen di solito 100) char(fixed len)
				Testo -> text, tinytext, mediumtext, longtext, not indexable
				Data -> date
				Intero -> integer, int, tinyint, smallint, mediumint, bigint, unsignedint, int(padding)
				Decimal -> numeric(prec, scala), decimal(prec: max digits, scala: number of digits after decimal points), fixed()
				Approssimati:
					float(prec) 
					double precision
					Reale -> real
				Ora -> time
				DataOra -> timestamp
				Booleano -> boolean
				Intervallo -> interval
				CLOB 
				BLOB
			Id artificiali:
				id -> serial not null
				orrrrr   
				CREATE SEQUENCE Tabella_id_seq;
				CREATE TABLE Tabella(
					id integer default nextval('Tabella_id_seq') not null
				);


			Tipi specializzati: X..Y -> DomName
				CREATE DOMAIN DomName AS integer
					CHECK(value >= X and value <= Y); 
				CREATE DOMAIN StringaNumerica AS string
					CHECK(value like 'R%' / '_');
			Tipi enumerativi: {'',''} -> DomName
				CREATE TYPE DomName AS ENUM ('','', ...); i valori non sono stringhe ma sono gli identificatori per elementi dell'insieme
			Tipi compost: DomName -> DomName
				CREATE DOMAIN Type1_not_null AS Type1
					CHECK (value IS NOT NULL and ...);
				CREATE DOMAIN Type2_not_null AS Type2
					CHECK (value IS NOT NULL);
				CREATE TYPE DomName AS (
					f1 Type1_not_null
					f2 Type2_not_null
					...	
				);
		2.1.3 Eliminazione delle generalizzazioni tra classi: per ogni singolo livello di ogni generalizzazione, scegliendo tra:
			Fusione di sottoclassi nelle loro superclassi:
				Relazione is-a:
					- Alla superclasse viene aggiunta l'attributo tipo: TipoSuperclasse
					- Tutte le associazioni e attributi di sottoclasse vengono ereditate da superclasse con il vincolo di molteplicità minima rilassata a 0
					- CREATE TYPE TipoSuperclasse AS ENUM ('Super', 'Sotto');
					- Vincoli esterni aggiuntivi: solo nel caso [1..1] non [0..1] e attributi e associazioni diversi da superclasse
						∀sup SuperClasse(sup) → [tipo(sup, 'Sotto') ↔ ∃a attr(sup, a)] in caso di molteplicità [1..1] di attr nella sottoclasse
						∀sup SuperClasse(sup) → [tipo(sup, 'Sotto') ↔ ∃a assoc(sup, a)] in caso di molteplicità [1..1] di assoc nella sottoclasse
						Se la sottoclasse specializza l'attributo di superclasse: l'attributo specializzato ed il suo dominio vengono eliminati e:
						∀sup, v SuperClasse(sup) ∧  attr(sup, v) ∧ tipo(sup, 'Sotto') -> condizione su v
						Se la sottoclasse specializza l'associazione di superclasse: Vedi fusione di associazioni 
						
				Generalizzazione:
					{disjoint}: Tutto come sopra tranne:
						- Per ogni sottoclasse tutte le associazioni e attributi di sottoclasse vengono ereditate da superclasse con il vincolo di molteplicità minima rilassata a 0
						- CREATE TYPE TipoSuperclasse AS ENUM ('Super', 'Sott1', 'Sott2',...);
						- Vincoli esterni come sopra ma per ogni singolo sottoclasse
					{disjoint, complete}: Come {disjoint} tranne:
						- CREATE TYPE TipoSuperClasse AS ENUM ('Sotto1', 'Sotto2',...);
				is_a indipendenti: ne disjoint ne complete, tutto rimane come {disjoint} tranne:
					- Non viene definite l'attributo tipoSuperclasse ed il dominio corrispondente invece
					- Per ogni sottoclasse alla superclasse viene aggiunta l'attributo is_sotto1:boolean 
					- Vincoli esterni: il predicato tipo(sup, 'Sotto1') viene sostituito con is_sott(sup, true)
					{complete}: come indipendenti con un ulteriore vincolo esterno:
						∀sup SuperClasse(sup) → [is_sott1(sup, true) ∨ is_sott2(sup, true)  ∨ ...]

			Divisione delle superclassi in classi disgiunte:
 				Generalizzazione: 
					- Tutte le associazioni e gli attributi di superclasse con le relative molteplicità vengono ereditati da sottoclassi per associaizoni assoc_sott1,... rispettivamente e 						viene elimnata la superclasse
					- Viene recuperata la semantica dei vincoli di identificazione di attributi e associazioni {id} della superclasse:
					{disjoint, complete}: 
						- ¬∃sott1, sott2,..., a, as  SottoClasse1(sott1) ∧ SottoClasse2(sott2 ) ∧...∧ attr(sott1, a) ∧ attr(sott2, v) ∧ assoc(sott1, as) ∧ assoc(sott2, as)
			Sostituzione con associazioni: 
				is_a indipendenti:
					- Le freccie is_a diventano associazioni rispettivamente chiamate sott1_isa_sup, sott2_isa_sup,... con le molteplicità del ruolo vicino a superclasse 1..1 con {id} e 						vicino a sottoclasse 0..1; il vincolo {id} implica che non possono coesistere due istanze della stessa sottoclasse, diverse ed avente i link con la stessa istanza di						superclasse 
					- Attributi specializzati vengono eliminati come fusione ed il predicato tipo sostituito da sotto_isa_sup(sott, sup)
					- relazioni specializzati: vedi sostituzione di associazioni
				Generalizzazione:
					{disjoint}: come sopra con:
						Vincoli Esterni: [V.Sup.gen.disj]
							¬∃ sup, sott1, sott2,... SuperClasse(sup) ∧ SottoClasse1(sott1) ∧ SottoClasse2(sott2 ) ∧...∧ sott1_isa_sup(sott1, sup) ∧ sott2_isa_sup(sott2, sup) ∧ ...
					{complete}: come is_a indipendenti con:
						Vincoli Esterni: [V.Sup.gen.compl]
							∀sup SuperClasse(sup) → [ ∃sott1 sott1_isa_sup(sott1, sup)] ∨ [ ∃sott2 sott2_isa_supp(sott2, sup) ∨ ...]
					{disjoint, complete}: {disjoint} and {complete}

		2.1.4 Eliminazione delle generalizzazioni tra associazioni: deve corrsipondere al metodo scelto per le sue classi incidenti
			Fusione: Tutta la parte di sottoclassi e sottoAssociazioni viene eliminata e:
				∀sup, as SuperClasse(sup) ∧ assoc(sup, as) ∧ tipo(sup, 'Sotto') -> condSpecAssoc(come tipoAltraClasse(as, 'SottAltra'))
			Sostituzione: La freccia tra l'associazione e la sua sottoAssociazione viene eliminata e:
			∀ sott1, sup1, sott2, sup2  assocSott(sott1, sott2) ∧ sott1_isa_sup1(sott1, sup1) ∧ sott2_isa_sup2(sott2, sup2) → assocSup(sup1, sup2) cioe' se esistono istanze di sottoclasse connessi 			 	 tramite link di sottoassociazione allora deve esistere il link di superassociazioni tra superclassi corrispettive	
		2.1.5 Definizione di un identificatore per ogni classe che fungera da chiave se non cel'ha definiamo identificatore artificiale denotati come {id2}, {id3},... Km b b
			Selezione di un identificatore primario per ogni classe(non deve essere troppo complicato) che fungera da chiave primaria denotato come {id1}
				- per le sottoclassi ristrutturate tramite sostituzione {id} sul ruolo deve essere identificatore primario(identificatore primario esterno) che coincide con {id1} della 					superclasse
				- per rompere i cicli di identificatori basta creare un altro artificiale in uno dei componenti(classi)
		2.1.6 Ristrutturare i vincoli esterni in vincoli equivalenti definiti sul diagramma ristrutturato e scriverli nel documento di specifica ristrutturata dei vincoli esterni
		2.1.7 Eliminazione delle operazioni della classe dal diagramma e ristrutture le loro specifiche tali che diventano conformi con il diagramma ristrutturato delle classi
	2.2 Traduzione diretta
		Classe: una tabelle relazionale
			C(_attr{id}:type_, attr1:type1, ....)
			CREATE TABLE C{
				attr1 type not null [1..1],
				attr2 type/CustomType [0..1],
				attr3 type default val, 
				primary key (attr1) attributi con {id1}     primary implica not null
				CHECK(inizio <= fine)
			};
		Associazione: 
			vincoli di molteplicità sui ruoli si tradducono in vincoli di chiave e di foreign key o esterni
			Una tabella relazionale:
				C1 - 0..*, C2 - 0..*:
				C1(_attr1{id}:type1_, attr12:type12, ....)
				C2(_attr2{id}:type2_, attr22:type22, ....)

				assoc(_c1:type1_, _c2:type2_, attr1:type3, ...)
					foreign key: c1 references C1(attr)
					foreign key: c2 references C2(attr)
				
				CREATE TABLE assoc{
					c1 type not null,
					c2 type not null,
						siccome non possono essere null nessuno dei due la molteplicità minima viene soddisfata cosi che se una delle istanze sia null il record non esisterebbe nella 							tabella giustamente come nell'estensione non esisterebbe tale link
					attr3 type,
					primary key (c1, c2), primary implica not null
					foreign key (c1) references C1(attr1),
					foreign key (c2) references C2(attr2)
				};
				C1 - 0..*, C2 - 0..1: 
				CREATE TABLE assoc{
					c1 type not null,
					c2 type not null,
					attr3 type,
					primary key (c1), cosi non possiamo avere due occorenze della stessa istanza di C1
					foreign key (c1) references C1(attr1),
					foreign key (c2) references C2(attr2)
				};
				possiamo accorpare C2 in C1 solo che non mettiamo not null per c2 e tutte gli attributi della associazione e c2 non lo includiamo nella primary
				C1 - 0..1, C2 - 0..1:
				CREATE TABLE assoc{
					c1 type not null,
					c2 type not null,
					attr3 type,
					primary key (c1), o primary key(c2)
					unique(c2), o unique(c1)
					foreign key (c1) references C1(attr1),
					foreign key (c2) references C2(attr2)
				};

				C1 - 1..*, C2 - 0..*:
				C2(_attr2{id}:type1_, attr22:type22, ....)
					vincolo di inclusione: attr2 occorre in assoc(c2) si implementa cosi:
					foreign key (attr2) references assoc(c2)    in questo caso diventa impossibile inserire ennuple dentro C2, dobbiamo estrarrlo da C2 e farlo diventare deferrable
				CREATE TABLE assoc{
					c1 type not null,
					c2 type not null,
					attr3 type,
					primary key (c1, c2),
					foreign key (c1) references C1(attr1),
					foreign key (c2) references C2(attr2)
				};
				alter table C2         l'abbiamo estratto per evitare nominare assoc prima che sia definita ma possiamo sempicemente riordinarli portando assoc sopra ed il vincolo dentro C2
				add constraint c2InAssoc
				foreign key (attr2) references assoc(c2) deferrable; in questo caso durante una transazione tutti i vincoli deferrable possono essere violati 

				C1 - 1..1, C2 - 0..*: la combinazione di [C1 - 1..*, C2 - 0..*] e [C1 - 0..1, C2 - 0..*]
			Accorpamento:
				C1 - 0..*, C2 - 1..1 {id1}: accorpamento della tabella dell'associazione nella tabella per C1:
				CREATE TABLE C1{
					attr1 type not null,
					c2 type not null,
					attr3 type,
					attr1Assoc type,
					primary key (attr1, c2),
					foreign key (c2) references C2(attr2)
				};
				l'accorpamento lo possiamo fare anche quando non c'ha {id1} sul ruolo in quel caso c2 non sarebbe primary
				generalizzazioni sostituite da relazioni sott_isa_sup: Sott 0..1, Sup 1..1 {id1}
				CREATE TABLE Sott1{
					attr1 type not null,
					sup type not null,
					attr3 type,
					unique(attr1)
					primary key (sup),
					foreign key (sup) references Sup(attr1)
				};
		Vincoli Esterni:
			1. Asserzione in standard SQL: ignorati 
			2.Trigger:
				- Intercetta un evento(insert/update/delete): eventi che possono portare un DB legale a diventare illegale	
				- Esegue un controllo(codice imperativo con SQL immerso):
					old (solo per UPDATE e DELETE) 
					new (solo per INSERT e UPDATE)
				- Opzionalmente sollevare un errore per rifiutare l'operazione intercettata
				Blue-print:
					we can optionally change the delimiter to $$ so we don't have to write $nome$ instead we write nothing, to restore to normal DELIMITER ;
					create or replace function $V_Classe_nome$ 
					declare isError boolean := false;
					begin
						isError = NOT EXISTS();
						if(isError)
							raise exception 'Vincolo nome violato(Classe.id=%), old/new.id'
						endif;
						return new/old  nel caso di before puo' essere utile
					end $V_Classe_nome$;
	
					create [constraint] trigger V_Classe_nome_nome    diverso dalla operazione
					after/before/instead of {insert/update/delete or ...} on NomeClasse
					deferrable      per questo deve essere constraint e after
					for each row/for statement
					execute precedure V_Classe_nome() 
					[when condizione];

			Alcuni sono implementabili tramite unique, foreign key e inclusione, check(vincoli di ennupla):
				- Nel caso di sostituzione di associazioni quando le classe coinvolte di entrambe le associazione sono uguali: sottassoc(c1, c2) -> supassoc(c1, c2) e' implentabile tramite 					inclusione: foreign key(c1, c2) references superassoc(c1, c2)
				check(v between v1 and v2)(v1<=v2)
			Altri no:
				- Politiche di accesso ai dati: facendo cosi possiamo ignorare update
					REVOKE UPDATE (id) ON Super FROM PUBLIC;
					REVOKE UPDATE (super) ON Sotto FROM PUBLIC;

			 	-  [V.Sup.gen.disj]: dopo Insert(new) on Sott1 o Sott2
				isError = EXISTS(
					SELECT *
					FROM Sott1 s1, Sott2 s2
					Where s1.sup = new.sup AND s2.sup = new.sup
				)
				- [V.Sup.gen.compl]: $V_Sup_gen_compl_1_sup$ dopo Insert(new) on Sup
				isError = NOT EXISTS(
					SELECT sup FROM Sott1 WHERE sup = new.id
					UNION
					SELECT sup FROM Sott2 WHERE sup = new.id
				);
			
				-  [V.Sup.gen.compl]: $V_Sup_gen_compl_2_[Sott1 | Sott2]$ dopo Delete(old) on Sott1 o Sott2
				isError = Exists(
					FROM(Sup sup LEFT OUTER JOIN Sott1 s1 ON sup.id = s1.sup)
					LEFT OUTER JOIN Sott2 s2 ON p.id = s2.sup
					WHERE sup.id = old.sup AND (s1.sup IS NULL) AND (s2.sup IS NULL)
				);


SQL:
	DDL:
		chiave primaria(viene sottolineata) non puo' accettare valori NULL altre chiavi si
		vincolo di integrita' referenziale o di foreign key fra insieme X di attributi in relazione R e la relazione S: ogni t di R deve avere valori per attributi di X tali che compaiono come valori 		degli attributi della chiave (di solito primaria) di S
		vincoli intra-relazionali viengono cotrollatoi prima di insert/update e implementati dal costrutto check e value
		Azioni compensative in seguito di un'operazione che andrebbe a violare vincoli di integrita':
			rifiuto dell’operazione (comportamento di default)
			introduzione di valori NULL 
			cancellazione in cascata
		cf character (16) not null
		alter table add/drop/alter column/constraint
		drop table

	DML: per manipolazione del livello estensionale
		Inserimento:
			insert into Tabella(attr1, attr2, attr3, ....) values (v11, v12, v13, ...), (v21, v22, v23), ...... attributi default possono essere omessi
			insert into Tabella(attr1, attr2, ...) query

			inserimenti consecutive nelle tabelle con id artificiali(hierarchical rows):
				begin transaction;
					DO $$ blocco anonimo
					declare _id integer;
					begin
						set constraints all deferred;    chiede esplicitamente a DBMS di controllare tutti i vincoli deferrreble solo al termine di ogni transazione
						insert into Super(attr1, attr2) values(DEFAULT, 'qualcosa') returning id into _id; default per id 
						insert into Sotto(sup, attr) values(_id, 'qualcosa altra');
					end $$;
				commit;
				in caso di violazione dei vincoli non deferrable la transazione venga roll back 
		Cancellazione:
			delete from tabella
			where id = ...
			orrr
			where id in/not in/... (querry)
		Modifica:
			update Tabella
			set attr1 = ...
			where (default where true)
		Interrogazioni:
			Funzioni aggregate(attr/distinct attr): operazioni su colonne che ritornano un solo valore cioe' una tabella con una sola cella
				avg()
				count() numero di valori non null
				max()
				min()
				sum()
				we can define new aggregated functions by CREATE FUNCTION statement
				
			create or replace view Nome as
				select [distinct] t1.col as c1, t2.col2 as c2, ... / aggr(col) / *    
					la target list deve essere omogenea se contiene agr non deve contenere attr tranne il caso group by in cui deve contenere tutti attr fuori da aggr
					quando lavoriamo con una sola tabella non c'e' bisogno di specificare la tabella t1.col 
					la tabella ritornata non rappresenta per forza una relazione se no dobbiamo usare distinct
				from Tabella1 t1, Tabella2 t2, ViewCreata v
				where c1 =/<> c2 / c1 = (Select aggr(col) from tabella) / and/or  is/is not null   is between  overlaps   condizione sulle righe	
				group by c1
				order by attr1, attr2,... asc/desc
				having condizione sui gruppi, non possiamo accedere ad alias definiti in taraget list

			from puo' contenere query annidata che viene valutato dal piu' interno verso piu' estern
			alias definiti in sottoquery del from sono accessibili da query esterno tramite riferimento alla tabella sotto.alias_targetList_sotto
			anche where puo' contenere condizioni su sottoquerry: =/<>, >, in/=any,not in/<>all, <any, not exists
			le sottoquery non possono contenere operazioni insiemistiche
			quando vogliamo accedere a ogni Colonna della tabella generate da sottoquery nel from dobbiamo dare alla tabella per forza un alias
 
		Operazioni insiemistiche:
			queryA union [all] queryB        all mantiene i dupplicati, mantiene nome del primo operando, union compatibili(numero e dominio di colonne uguali) 
			queryA minus/except queryB
			queryA intersect queryB    meglio implementarlo con join
		
		Interrogazione su piu tabelle:
			FROM T1, T2
			WHERE T1.a1 = T2.a2 and altre_cond
				orrr
			FORM T1 JOIN T2
			ON T1.a1 = T2.a2
			WHERE altre_cond
				orrr
			FROM T1 NATURAL JOIN T2  fa join su attributi omonimi
			FROM T1 LEFT OUTER JOIN T2 tutte le ennuple di T1 saranno sicuramente nel risultato quando non c'e' un elemento di T2 per qui soddisfa la condizione mette NULL
			FROM T1 RIGHT OUTER JOIN come sopra ma al contrario
			FROM T1 FULL OUTER JOIN l'unione dei risultati di due join sopra
		
		Espressioni: funzioni su valori sono diversi da funzioni aggregate
			operazioni su valori:
				date() ritorna il valore per la data di un oggetto

			Nel select, where, set di update, values di insert into:
				Operazioni aritmetiche:
					-, +, /, * 
					sqrt(), sin(), abs(), log(), logbase(base, val), power(base, exp), round(v, prec or digits after .), truncate(v, len), ceil(), floor(), tronc(), least(v1,...), rand()
				Sulle stringhe:
					length()
					upper(), lower(), initcap()
					lpad(string, len, pad), rpad() restituisce la stringa spostata sulla sinistra o sulla destra fino a length caratteri usando il carattere di riempimento pad(def ' ')
					ltrim(string, trimlist), rtrim() restituisce la parte più a sinistra o più a destra da cui altro terminale sono rimossi i caratteri del trimlist(def ' ')
					replace(string, target, replacement) se replacement e' omesso, tutte le occorrenze di target sono cancellate
					substr(string, pos, len)
					translate(string, fromlisst, tolist) come una replace iterativa, restituisce la stringa con ogni carattere in fromlist rimpiazzato con il corrispondente carattere in tolist
					to_char(number, format)
						to_char (1250000 , ’ $9 999 999.99 ’ ) -> $ 1 250 000.00
						to_char ( date ( ’ 2013 − 05 − 21 ’ ) , ’ DD FMMonth YYYY ’ ) -> 21 May 2013
					position(string, substr) se non esiste ritorna 0
					left(string, len) prendi le prime len caratteri di string
					locate(string1, string2) trova la prima occorrenza di string1 nel string2
					concat(string1, string2)
				Sulle date:
					NOW() return current timestamp 
					CURDATE() return current date, CURTIME()
					YEAR(dobj/dtobj) extract year of date object, MONTH(), DAY(), HOUR(tobj/dtobj), MINUTE(), SECOND()
					EXTRACT(DAY/MONTH/YEAR/ from NOW())
					DAYNAME(), MONTHNAME()
					DATE_FORMAT(dobj, '%y') %y 2-digis year, %Y 4-digits year, %m 2-digits month, %M month name, %d 2-digits day, %D day name, %H hour, %i minutes, %p pm-am
					DATE_ADD/_SUB(dobj, INTERVAL 1 DAY/YEAR/MONTH)
					DATEDIFF(dobj1, dobj2) returns difference in days 
					TIME_TO_SEC(tobj) returns seconds elapsed from midnight

		Specifiche realizzative per le operazioni di use-case e delle operazioni di classe:
			Segnatura: convertito in domini compatibili con SQL in fase di ristrutturazione
			Algoritmo: in pseudo-codice contenente eventuali comandi SQL
				precondizioni vanno gestiti con raise exception
				delle classi: uguale a use-case ma sempre con un oggetto di invocazione PAR_1
				se implementata in DB:
					create or replace myfunc(arg1 tipo)
						returns tipo_ritornato as $BODY$
					decalre 
						res tipo1 := NULL
						var2 tipo2 := default_val
					BEGIN
						memorizza il risultato nella variabile Q 
						SELECT a, op(b) into var1, res
						where tabella.id = arg 
						IF (res is NULL) THEN raise exception '... non esiste';
							ELSE
								IF (var2 is NULL) THEN raise exception 'qualcosa';
								ELSE 
									return res;
								END IF;
						END IF;
					END; $BODY$
				se implementato nella DB puo' essere invocata:
					SELECT myfunc(args)
			in realta' basta una discrizione verbale:
				per nuove ennuple:
					Insert into tabella(attr1, attr2, attr3) values(PAR_1, PAR_2, PAR_3) dopo aver rimpiazzato PAR_1,... con valori arg1, ...
				per non esiste gia' un valore per assoc nel precondizioni:
					dopo inserimento restituisce un errore di vincolo di chiave violato allora raise exception 'ennupla gia' esistente' 
					
Altro:
	superiore a : >
	almeno : >=
Ricordati di rilassare tutte le molteplictà minime a 0 finché è possible e cattura la realtà in modellazione
Quando vogliamo controllare un condizione su un valore per un campo o un link, con la molteplictà minima 0 di una istanza di una classe dobbiamo usare PEROGNI x tale che soddisfa il predecato di tale attr o Assoc -> la condizione

Media é sempre Reale e c'ha precondizione
Per trovare nerodi giorni tra due date o istanze si puo sottrarle

Nel caso di accorpamento non c'è bisogno di unique per verificare vincolo di molteplicità massima 1, infatti cio viene implicata dalla chiave primaria dell'oggeto accorpante che non può ripetersi per diversi valori di foreign key, e nel caso di accorpamento il vincolo di inclusione viene implicata da NOT NULL