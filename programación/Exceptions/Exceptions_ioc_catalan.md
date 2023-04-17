# Exceptions

- **Què és la gestió d'excepcions?**
    - el conjunt de mecanismes que un llenguatge de programació proporciona per detectar i gestionar els errors que es puguin produir en temps d’execució.
- **Tenim 2 maneres de gestionar les excepcions:**
    - 1a manera: dissenyant els mètodes de manera que retornin un codi d’error que es revisa després de la crida a la funció o mètode amb l’ajut d’instruccions condicionals per tal de prendre la decisió adequada. Aquesta tècnica no dóna bons resultats quan l’error és fatal (ha de provocar la finalització del programa) i es pot produir en diferents nivells de crides internes, ja que la funció o el mètode dissenyats per nosaltres es pot cridar dins d’altres funcions o mètodes, fet que fa impossible saber la cascada de crides fins al punt en el qual s’ha produït l’error.
    - 2a manera: Utilitzant construccions especials per a la gestió d’errors proporcionades pel llenguatge de programació, com és habitual en els llenguatges moderns com C++, Visual Basic i Java, que acostumen a proporcionar mecanismes de propagació de l’error cap a les funcions o mètodes que han cridat la funció o mètode en què s’ha produït l’error, de manera que és possible conèixer la cascada de crides fins el punt en el què s’ha produït l’error.
- **Com és el model de gestió d'excepcions que proporciona Java?**
    - en produir-se un error, la màquina virtual llança (throw) un avís que el programador hauria de poder capturar (catch) per resoldre la situació problemàtica.

* * *

## 1.1.1. Tipus d'excepcions

- **Quines peculiaritats tenen els errors?**
    - Els errors corresponen a situacions irrecuperables, que no tenen solució i que no depenen del programador, el qual no s’ha de preocupar de capturar.
    - No s’haurien de produir mai, però quan tenen lloc provoquen la finalització brusca del programa.
- **Exemples d'errors:**
    - Quan la màquina virtual es queda sense recursos per continuar amb l’execució del programa.
    - Quan alguna cosa va malament en la càrrega d’un servei d’un proveïdor.
    - Quan deixa de respondre un canal d’entrada/sortida.
    - ...
- **Quines peculiaritats tenen les excepcions?**
    - Corresponen a situacions excepcionals que els programes es poden trobar en temps d’execució.
    - S'hi poden incloure, fins i tot, els errors de programació.
- **Què hauria de fer el programador per evitar que el programa peti per saltar excepcions?**
    - El programador ha de preveure cada tipus d'excepció i escriure el codi adequat per a la seva gestió.
- **En quina classe engloba Java tots els possibles errors?**
    - A la classe Error.
- **En quina classe engloba Java totes les possibles excepcions?**
    - A la classe Exception.
- **Què succeeix quan es produeix una situació problemàtica d'Error o Exception?**
    - Es crea un objecte de la classe Error o Exception que conté la informació del context en què s'ha produït el problema.
- **De quina classe deriven les classes Error i Exception?**
    - De la classe Throwable.
- **Què proporciona la classe Throwable?**
    - Mecanismes comuns per a la gestió de qualsevol tipus d'error i excepció.
- **Quins mecanismes de la classe Throwable per la gestió de qualsevol tipus d'error i excepció convé conèixer?**
    - 1r mecanisme: Existència de 4 constructors per a qualsevol classe derivada.
    - 2n mecanisme: Existència de mètodes per conèixer el context en el qual s'ha produït la situació problemàtica, i per tant, poder actuar en consequència.
- **Quins són els 4 constructors de la classe Throwable?**

```java
    Throwable()
       /* Construeix un objecte Throwable amb missatge null */
    Throwable(String message)
       /* Construeix un objecte Throwable amb el missatge indicat */
    Throwable(String message, Throwable cause)
       /* Construeix un objecte Throwable amb el missatge indicat i amb la causa que ha 
          provocat la situació */
    Throwable(Throwable cause)
       /* Construeix un objecte Throwable amb la causa que l'ha provocat i com a missatge, 
          el resultat de: cause==null ? null : cause.toString() */
```

- **Per a què serveix que hi hagi constructors de la classe Throwable que tenen de paràmetre d'entrada un objecte de la classe Throwable?**
    - Perquè un objecte serà causant de la creació del nou objecte, i es podran encadenar els errors i /o excepcions.
- **Quins són els mètodes de la classe Throwable que ens permeten conèixer el context en el qual s'ha produït la situació problemàtica (i d'aquesta manera poder actuar en conseqüència)?**

```java
    Throwable getCause();  /* Retorna la causa o null */
    String getMessage();   /* Retorna el missatge o null */
    void printStackTrace();   /* Visualitza pel canal d'errors, el context en el que s'ha
                              produït l'error i la cascada de crides des del mètode main()
                              que han portat al punt en el que s'ha produït l'error */
    String toString();   /* Retorna una curta descripció de l'objecte */
```

- **On ens hem de centrar en 1r i en 2n lloc per desenvolupar aplicacions Java amb una bona gestió d'excepcions?**
    - En 1r lloc: en el coneixement de la jerarquia de classes que neix a partir de la classe Exception.
    - En 2n lloc: en els mecanismes de gestió d’excepcions que proporciona Java.
- **Quins 2 grans subtipus d'excepcions trobem en la classe Exception?**
    - 1r subtipus d'excepcions: Excepcions implícites.
    - 2n subtipus d'excepcions: Excepcions explícites.
- **Què són les excepcions implícites?**
    - Són excepcions que la mateixa màquina virtual s'encarrega de comprovar durant l'execució d'un programa.
    - El programador no té l'obligació de capturar ni gestionar aquest tipus d'excepcions.
    - Estan agrupades en la classe `RuntimeException`.
    - Normalment estan relacionades amb errors de programació:
        - Errors que normalment no es revisen en el codi d'un programa (com rebre una referència null en un mètode quan el dissenyador ha soposat que qui cridi haurà passat referència no nul·la).
        - Errors que el programador hauria d'haver revisat en escriure el codi (com sobrepassar la grandària assignada a una taula).
- **Què són les excepcions explícites?**
    - Totes les excepcions de la classe `Exception` que no pertanyen a la subclasse `RuntimeException`, que el programador ha de tenir en compte si es poden produïr.
- **Quins 4 mecanismes de gestió d'excepcions que proporciona Java ens cal saber?**
    - Com es gestionen les excepcions.
    - Com es generen (llancen, en terminologia Java).
    - Com es creen noves excepcions per donar suport a una gestió d'excepcions per a les classes que dissenyem.
    - Quins efectes té l'herència en la gestió d'excepcions.

* * *

## 1.1.2. Captura i tractament

- **Quin mecanisme proporciona el llenguatge Java per capturar una excepció i definir l'actuació que correspongui?**
    - El try-catch.
- **En què consisteix el try-catch?**
    - Consisteix a col·locar el codi susceptible de generar (llançar) l'excepció que es vol capturar dins un bloc de codi precedit per la paraula reservada try i seguit de tants blocs de codi catch com excepcions diferents es volen capturar.
- **Quina és la sintaxi del try-catch?**

```java
    try {
   			  <bloc_de_codi_susceptible_de_llançar_excepció>  
    } catch (nomClasseExcepció1 e1) {
    <bloc_de_codi_a_executar_si_en_el_bloc_try_s'ha_produït_una_nomClasseExcepció1>  
    } catch (nomClasseExcepció2 e2) {
    <bloc_de_codi_a_executar_si_en_el_bloc_try_s'ha_produït_una_nomClasseExcepció2>  
    } ...
    } finally {
    <bloc_de_codi_a_executar_en_qualsevol_cas-s'hagi_produït_o_no_una_excepció->  
    }
```

- **Què succeeix quan es produeix una excepció en el codi del bloc try?**
    - La màquina virtual avorta l'execució del codi del bloc try i comença a avaluar els diversos blocs catch, en l'ordre en què estiguin situats, fins a trobar el primer bloc que en la seva classe d'excepcions inclogui l'excepció produïda en el bloc try.
- **Què succeeix quan no existeix cap bloc catch que correspongui a l'excepció produïda?**
    - La màquina virtual executa el codi del bloc finally, en cas d'existir.
    - Posteriorment, avorta el mètode en què s'ha produït l'excepció i propaga l'excepció al mètode immediatament superior, perquè sigui allà on es capturi l'excepció.

```java
//Classe on creo l'excepció checked
public class NotPositiveAgeException extends Exception {
    NotPositiveAgeException(){
        super("No es permet posar edats negatives.");
    }
}
```

```java
public class Persona {
    private String nombre;
    private int edat;
    
    //throws -> L'excepció es propaga en aquest exemple al mètode que ha 
    //cridat a aquest constructor, en aquest exemple al mètode main de la 
    //classe Programa, per tal de veure si es pot capturar allà
    public Persona(String nombre, int edat) throws NotPositiveAgeException {
        guard(edat);
        this.nombre = nombre;
        this.edat = edat;
    }
    
    //throws -> L'excepció es propaga al mètode que ha cridat aquest mètode, en 
    //aquest exemple al constructor Persona(String nombre, int edat), per tal de
    //capturar-la allà
    private void guard(int edat) throws NotPositiveAgeException {
        if (edat < 0) {
            NotPositiveAgeException e = new NotPositiveAgeException();
            throw e;
        }
    }
}
```

```java
public class Programa {
    //l'excepció és capturada finalment aquí mitjançant el try-catch
    public static void main(String[] args) {
        try {
            Persona p1 = new Persona("Pau", -1);
        }
        catch(NotPositiveAgeException e){
            System.out.println(e.getMessage());
        }
    }
}
```

- **Què succeeix si l'excepció va passant al mètode superior i quan arriba al main() tampoc és gestionada?**
    - Es produeix una finalització anormal de l'execució del programa i l'excepció es llança.
- **Quan s'executa el bloc opcional finally?**
    - Sempre, s'hagi produït una excepció o no, hagi estat capturada l'excepció o no.
    - Fins i tot s'executa si dins els blocs try-catch hi ha alguna sentència :
        - continue
        - break
        - return
- **Quina és la única situació en què el bloc finally no s'executa?**
    - Quan es crida el mètode System.exit() que finalitza l'execució del programa.
- **On situariem les sentències de tancament d'un fitxer que hem obert ?**
    - Al bloc finally que segueix al try-catch.
- **És possible crear un try que no tingui un catch?**
    - Si, per exemple el següent codi, en el que el codi del bloc finally assegura l'execució de certes accions.

```java
    try
    {
      obrirAixeta();
      regarGespa();
    } finally { 
      tancarAixeta();
    }
```

- **Què succeeix quan es produeix una excepció?**
    - Es crea un objecte de la classe corresponent a l'excepció que conté informació del context en què s'ha produït el problema.
- **Quins són els mètodes heretats de la classe Throwable que ens permeten obtenir informació del context en què s'ha produït l'excepció a partir de l'objecte generat de la classe corresponent a l'excepció?**

```java
    String getMessage();   /* Retorna el missatge o null */
    void printStackTrace();   /* Visualitza pel canal d'errors, el context en el que s'ha produït l'error i la cascada de crides des del mètode main() que han portat al punt en el que s'ha produït l'error */
    String toString();   /* Retorna una curta descripció de l'objecte */
```

- **Per què és millor escriure l'excepció en concret que no la superclasse Exception al capturar l'excepció?**
    - Perquè si peta i al catch hi he posat Exception e, pot ser que estigui capturant una excepció que no tinc en compte. En canvi, si al catch hi poso la subclasse específica d'Exception, sé que l'excepció capturada serà de la subclasse especificada.
- **Quan finalitza la propagació de l'excepció?**
    - Quan trobem un mètode que captura l'excepció.
- **Exemple llançament excepció dins un catch:**

```java
public class NotPositiveAgeException extends Exception {
    NotPositiveAgeException(){
        super("No es permet posar edats negatives.");
    }
}
```

```java
public class Persona {
    private String nombre;
    private int edat;

    public Persona(String nombre, int edat) throws NotPositiveAgeException {
        guard(edat);
        this.nombre = nombre;
        this.edat = edat;
    }

    private void guard(int edat) throws NotPositiveAgeException {
        if (edat < 0) {
            NotPositiveAgeException e = new NotPositiveAgeException();
            throw e;
        }
    }
}
```

```java
import java.util.Arrays;

public class Programa {

    public static void main(String[] args) {
        //Recojo la excepción que lanza el método ola()
        try {
            ola();
        } catch (Exception e2) {
            //throw new RuntimeException(e);
            System.out.println("A2: Retorna el missatge o null de l'excepció e2:" + e2.getMessage());

            System.out.println("B2: Visualitza pel canal d'errors, el context en el que s'ha produït l'error i " +
                    "la cascada de l'excepció e2: e2.printStackTrace():");
            System.out.println(Arrays.toString(e2.getStackTrace()));
            e2.printStackTrace();

            System.out.println("C2: Retorna una curta descripció de l'objecte excepció e2: e2.toString():");
            System.out.println(e2.toString());

            System.out.println("D2: Retorna la causa de l'excepció: e2.getCause(): " + e2.getCause());
            System.out.println();
        }
    }

    private static void ola() throws Exception {
        try {
            //Creo objeto que lanzará la excepción NotPositiveAgeException
            Persona p1 = new Persona("Pau", -1);
        }
        //Recojo la excepción que lanza el constructor del objeto p1
        catch(NotPositiveAgeException e){
            System.out.println("A:Retorna el missatge o null de l'excepció e: e.getMessage(): " + e.getMessage());

            System.out.println("B:Visualitza pel canal d'errors, el context en el que s'ha produït l'error i " +
                    "la cascada de l'excepció e: e.printStackTrace():");
            System.out.println(Arrays.toString(e.getStackTrace()));
            e.printStackTrace();

            System.out.println("C:Retorna una curta descripció de l'objecte excepció e: e.toString():");
            System.out.println(e.toString());

            //Creo una nova excepció de tipus Exception, que serà llançada ara.
            //Aquest objecte excepció serà creat amb el constructor al que li passo un objecte
            //de tipus Throwable cause. L'objecte e2 té la causa que ha provocat
            //l'excepció de l'objecte e i el missatge de l'objecte e
            Exception e2 = new Exception(e);
            throw e2;
        }
    }
}
```

* * *

## 1.1.3. Gestió: captura o delegació

- **Quines excepcions no obliga el llenguatge de Java a gestionar pel programador?**
    
    - Les excepcions de la classe RuntimeException.
- **Quines 2 maneres tenim d'informar-nos sobre les excepcions que pot llançar un mètode?**
    
    - Primera manera: Fent una ullada a la documentació del mètode.
    - Segona manera: Observant els errors de compilació que es produeixen si no es gestiona una excepció que no sigui RuntimeExcepion.
- **Què fa el compilador de Java si s'adona que no totes les excepcions no RuntimeException són gestionades pel programa?**
    
    - Informa d'un error similar a:
        - unreported exception nomExcepció; must be caught or declared to be thrown
- **Quins són els 2 mecanismes de que disposa el programador per gestionar les excepcions que no són de tipus RuntimeException?**
    
    - 1r mecanisme: Gestionar l’excepció dins el mètode en què es pugui produir capturant-la amb la utilització de blocs “try - catch”.
    - 2n mecanisme: Delegar la gestió de l’excepció al mètode superior, fet que s’indica en la capçalera del mètode, declarant les excepcions que no es gestionaran en el mètode amb la clàusula `throws` i seguint aquesta sintaxi següent:
        - \[modificadors\] nomMètode (&lt;arguments&gt;) \[throws exc1, exc2...\]

* * *

## 1.1.4. Llançament

- **De quins 2 passos consta llançar una excepció des d'un mètode?**
    - Primer pas: Es crea un objecte de la subclasse de la classe `Exception` que correspongui a l’excepció que es vol llançar (generar).

```java
nomExcepció e = new nomExcepció (...);
```

- - Segon pas: Es llança l’excepció amb la sentència `throw` seguida de l’objecte creat.

```java
throw e;
```

- **Quines 2 coses ha de decidir el programador en el moment en què dins un mètode es llança una excepció?**
    - 1\. Gestionar l'excepció dins el mateix mètode.
    - 2\. Delegar la gestió de l'excepció a mètodes superiors.
- **Què implica gestionar l'excepció dins el mateix mètode que llança l'excepció?**
    - Que la instrucció on es llança l'excepció hauria d'estar dins un bloc try-catch que capturés l'excepció.
- **Què implica gestionar l'excepció a mètodes superiors del mètode que llança l'excepció?**
    - Que la capçalera del mètode inclogui la declaració de l'excepció amb la clàusula throws.
    - Aquesta és la manera més usual de treballar.
    - El llançament de l'excepció fa que el mètode finalitzi i l'excepció es propagui cap al mètode superior en la pila de crides, el qual l'haurà de capturar o delegar.

## 1.1.5. Creació

- **Com pot el programador crear les pròpies excepcions?**
    - A partir de la derivació de la classe Exception o d'alguna de les seves classes derivades.
- **Què succeeix si creem una nova excepció derivada de la classe RuntimeException o d'alguna classe filla d'aquesta?**
    - La nova excepció no serà de gestió obligatòria.
- **Exemple de creació d'una excepció:**

```java
    //Fitxer Excepcio11.java
     
    public class Excepcio11 {
       public static void main (String args[]) {
          try {
             provocoExcepcio(0);
             provocoExcepcio(10);
          } catch (LaMevaExcepcio e) {
             e.printStackTrace();
          }
          System.out.println ("El programa finalitza correctament");
       }
     
       public static void provocoExcepcio(int valor) throws LaMevaExcepcio {
          System.out.println ("Valor: " + valor);
          if (valor!=0) throw new LaMevaExcepcio (valor);
          System.out.println ("No s'ha provocat l'excepció.");
       }
    }
```

```java
    //Fitxer LaMevaExcpecio.java
     
    public class LaMevaExcepcio extends Exception {
       private Integer valor;
     
       public LaMevaExcepcio (int xxx) {
          valor = new Integer(xxx);
       }
     
       public String toString () {
          return "Exception LaMevaExcepcio: Error motivat per valor = " + valor.toString();
       }
    }
```

* * *

## 1.1.6. Efecte de l'herència

- **Què succeeix si un mètode és una sobreescriptura d'un mètode de la classe base que incorpora la clàusula throws?**
    - El mètode sobreescrit no té per què llançar les mateixes excepcions que el mètode de la classe base.
    - El mètode sobreescrit pot llançar les mateixes excepcions o menys que el mètode de la classe base, pero NO més excepcions.