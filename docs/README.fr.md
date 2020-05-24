
# ITI 1521 - Lab 02

### Soumission

Veuillez lire les [instructions junit](JUNIT.fr.md) pour obtenir
de l'aide avec l'exécution des tests pour ce laboratoire.

Veuillez lire attentivement les [Directives de soumission](SUBMISSION.fr.md).
Les erreurs de soumission affecteront vos notes.

Soumettez les réponses aux

* Combination.java
* DoorLock.java

# Part 1: Conversion de type

## Objectifs d'apprentissage

* **Décrire** en vos propres mots ce que l'on entend par conversions de type de données.
* **Différencier** entre les conversions de type implicites et explicites.
* **Reconnaître** les situations où le forçage du type peut se faire sans conséquence sur l'exactitude des calculs.

## Conversion de type

Comme vu au laboratoire précédent, Java est un langage fortement **typé**. Il nous sera parfois utile de **convertir** une donnée d'un type primitif à un autre. Pour ce faire, il faudra toutefois être vigilant afin de ne pas **perdre de l'information.** Il existe 2 types de conversion: celles **implicites** et celles **explicites**.

### Conversion implicite/sans perte d'information

Les conversions implicites sont celles où il n’y a pas de perte de données (aucune perte d'information possible). Elles se produisent automatiquement lors de l'exécution du programme.

Par exemple, l’**affectation** d’une valeur peut se faire par une conversion implicite:

```java
float money;
int cash= 25;
money = cash;         // Converts from int to float
System.out.println (money);
```

Cette conversion est implicite, car la conversion d’un entier **int** vers un nombre à décimal **float** se produit sans perte d’information. On remarque aussi que le programme imprime « 25.0 ». Le « .0 » provient du fait que le 25 de type **int** est converti en **float**.

C'est aussi ce qui se produit lorsqu'une valeur de type **int** est affectée dans une variable de type **long**. Le type **long** représente aussi une valeur entière, mais l'intervalle de valeurs qu'il représente est plus grand que celui d'un **int** ; et il contient toutes les valeurs représentées par ce dernier. La conversion automatique dans l'autre sens est impossible puisqu'il y plusieurs valeurs représentées par un **long** qui ne peuvent être représentées avec la quantité de mémoire réservée pour un **int**. Il existe autant de situations qu'il y a de combinaisons de **types primitifs**. Vous pouvez les retrouver dans le [tableau](#tableau1) plus bas.

Il existe un second cas dans lequel la conversion implicite s’effectue. Il s’agit de la **promotion arithmétique**, c’est-à-dire lorsqu’un opérateur doit modifier le **type** de ses **opérandes** afin d’exécuter l’opération.

Par exemple:

```java
double num1 = 2.0;
int num2 = 6;
System.out.println (num2/num1);
```

Dans cet exemple, le programme imprime 3.0 à l’écran. La variable « num2 » est convertie en **float** avant la division.

À titre de référence, il existe une série de règles qu’il vous est possible d’appliquer afin de savoir quels seront les **types des opérandes** lors d'opérations effectuées avec

* `+`
* `-`
* `*`
* `/`
* `%`
* `<`
* `<=`
* `>`
* `>=`
* `==`
* `!=`

_À effectuer dans l'ordre:_

1.  Si un des opérandes est de type **double**, l'autre est converti en **double** ;
2.  Si un des opérandes est de type **float**, l'autre est converti en **float** ;
3.  Si un des opérandes est de type **long**, l'autre est converti en **long** ;
4.  Dans **tous les autres cas**, les deux opérandes sont convertis en **int**.

Veuillez noter qu’il n’existe aucune conversion pour le type **boolean**.

Le tableau ci-dessous résume l'ensemble des conversions **sans perte d'information** pour les différents **types primitifs** :

| DE | VERS |
| --- | --- |
| byte | short, int, long, float, double |
| short | int, long, float, double |
| char | int, long, float, double |
| int | long, float, double |
| long | float, double |
| float | double |


### Conversion explicite/forçage de type (« _type cast_ » en anglais)

Les conversions explicites sont celles où il peut y avoir perte de donnée. Pour ce faire, nous utilisons « l’opérateur de forçage de type ». Il s’agit en fait de deux parenthèses entre lesquelles se trouve le **type de donnée** dans lequel nous voulons convertir notre valeur.

Par exemple :

```java
double d = 16.987;
float f = (float) d;   // Converts from double to float without any loss of data
int i = (int) f;      // Converts from float to int with loss of data
long l = (long) i;    // Converts from int to long without any loss of data
System.out.println (d);
System.out.println (f);
System.out.println (i);
System.out.println (l);
```

On obtient alors à la console :

```java
16.987
16.987
16
16
```

Dans la sortie du programme, on remarque une perte de données, soit celles des valeurs des décimales « .987 », lors de la conversion de **float** à **int**. Il faut donc être vigilant lors de l'utilisation de ce type de conversion et s'assurer que les pertes d'information ne nuisent pas au bon fonctionnement de votre programme. Vous expérimenterez davantage ce type de conversion dans la prochaine partie du laboratoire.

## 2. Les messages d'erreurs

Programmer efficacement. Au cours du semestre, plusieurs idées vous seront présentées afin de développer cette habileté. L'une des principales habiletés est le **débogage**. Au début, les étudiants perdent beaucoup de temps avec cette activité, parfois, ils cherchent dans la mauvaise section du code. Nous reviendrons sur ce sujet au cours des prochains laboratoires. Pour l'instant, nous allons nous concentrer sur les messages d'erreurs. Il est important de bien comprendre les messages d'erreurs, et de se familiariser avec chacun d'eux. Pour faciliter la compréhension, je vous suggère de créer des petits programmes tests illustrant un seul cas d'erreur.

**Exercice!** Créez une nouvelle classe nommée **Test** ayant une méthode principale. Dans le corps de la méthode principale, vous déclarerez une variable de type **int**, à laquelle, vous affecterez la valeur **Long.MAX_VALUE.** C'est la plus grande valeur pour le type **Long**. Essayez par vous-même.

<center><h3>Quel est le message d'erreur affiché par le compilateur?</h3></center>

Parfois, la logique de nos programmes est telle qu'on souhaiterait tout de même faire cette conversion. Il faut alors être prudent. **Utilisez toujours un test afin de vous assurer que la valeur de l'expression se situe dans un intervalle de valeurs appropriées**. Lorsqu'on force une conversion (**type explicite/casting**), on dispense le compilateur de l'une de ses tâches essentielles, qui consiste à s'assurer que tous les types des sous-expressions sont compatibles. C'est comme si on disait au compilateur « je sais ce que je fais, s'il te plait, laisse-moi faire l'affectation de cette valeur à cette variable ».

```java
long l;
...
if (l >= Integer.MIN_VALUE && l <= Integer.MAX_VALUE) {
  int i = (int) l;
  ...
}
```

Puisque la valeur de la variable `l` est comprise dans l'intervalle des valeurs possibles pour un entier int, pourquoi faut-il forcer la conversion à l'aide de la syntaxe _(int)_ ? Autrement dit, pourquoi ne pourrait-on tout simplement écrire ceci :

```java
long l;
...
if (l >= Integer.MIN_VALUE && l <= Integer.MAX_VALUE) {
  int i = l;
  ...
}
```

La réponse est simple: le compilateur n'effectue pas de conversion implicite s'il y a un risque qu'il y ait perte d'information! Vous obtiendrez ainsi l'erreur suivante.

```java
Test.java:5: error: incompatible types: possible lossy conversion from long to int
             int i = l;
                     ^
1 error
```

Par ailleurs, on ne pourrait utiliser ce mécanisme (opérateur de cast) afin de transformer une chaîne de caractères (**String**) en un nombre ! Par contre, chaque type primitif possède une **classe « wrapper »**. Cette classe a un nom semblable au type auquel elle est associée. Par exemple, pour le type **int**, il y a la classe **Integer** (et de même, il y a les classes **Double, Boolean, Character**, etc). Comme le nom le suggère, chacune de ces classes enveloppantes sert à sauvegarder une valeur à l'intérieur d'un objet. Comme ceci :

```java
public class Integer {
  private int value;

  public Integer(int v) {
   value = v;
  }
  ...
}
```

Nous verrons plus tard des situations où ces objets seront nécessaires (lors de la présentation des **types abstraits de données**). Cependant, un aspect important de ces classes est qu'elles regroupent aussi un ensemble de méthodes utiles pour ce type.

Jetez-y un oeil par vous-même:

*  Allez à [https://docs.oracle.com/javase/8/docs/api/overview-summary.html](https://docs.oracle.com/javase/8/docs/api/overview-summary.html)

Il s'agit de la documentation des **classes et méthodes de Java 8.0**. Au fil de la session, vous devrez vous référer à cette documentation afin de connaître et d'utiliser ces classes et méthodes.

* Visitez le package **lang**.

Ce dernier est toujours chargé par défaut dans vos programmes (vous n'avez donc pas besoin de faire l'usage de _import_). C'est notamment dans ce package que vous retrouvez les classes « wrapper ». Par ailleurs, la classe « System » que vous connaissez bien en raison de l'usage de _println()_ s'y trouve aussi.

  * [http://docs.oracle.com/javase/8/docs/api/java/lang/package-summary.html](http://docs.oracle.com/javase/8/docs/api/java/lang/package-summary.html)

* Plus bas dans cette page, vous pouvez trouver la classe **Integer**.
  * [http://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html](http://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html)

* Trouvez maintenant la méthode **parseInt(String s)** et identifiez le type de retour de la méthode.

Il existe plusieurs erreurs de compilation. Ces erreurs peuvent être réduites si vous comprenez bien les **types** et que vous appliquez bien les règles de **syntaxe**. Le tableau ci-dessous résume les **erreurs de compilation** les plus courantes:

| MESSAGE D'ERREUR | EXPLICATION |
| --- | --- |
| `variable VARIABLE_NAME might not have been initialized` | Utilisation de la variable VARIABLE_NAME non initialisée. Attention, il peut aussi s'agir d'une faute de frappe! |
| `';' expected` | Un point-virgule est manquant à la fin d'une ligne de code. |
| `cannot assign a value to a final variable VARIABLE_NAME` | Affectation d'une valeur à une constante VARIABLE_NAME déjà initialisée. |
| <pre>incompatible types<br>found: TYPE1<br>required: TYPE2</pre> | Tentative d'affecter une valeur de type TYPE1 à une variable de type TYPE2. |
| <pre>cannot find symbol<br>symbol: WORD<br>location: LINE</pre> | Le compilateur trouve un mot WORD qu'il ne comprend pas. Vérifiez qu'il ne s'agit pas d'une faute de frappe. |
| `illegal start of expression` | Le compilateur trouve un élément qui ne devrait pas se trouver à cet endroit. |
| `not a statement` | La ligne de code n'est pas valide. |
| <pre>reached end of file while parsing<br>}<br>\^</pre> | Il y a probablement une erreur dans vos blocs de code. Vérifiez vos accolades { }. |

Bref, les **messages d'erreur** vous donnent beaucoup d'information (endroit de l'erreur, type d'erreur, etc.) Apprenez à bien les lire et les comprendre. Cela facilitera grandement le processus de débogage de votre code.

## Exercices!

Qu'est-ce qui sera affiché à la console lors de la compilation et l'exécution des courts programmes ci-dessous?

## Question 1.21:

```java
 public class Test {
  public static void main ( String[] args ) {
    int num1 = 9 ;
    double num2 = 12.0;
    double sum = num1 + num2;
    System.out.println(sum);
  }
}
```

## Question 1.22:

```java
 public class Test {
  public static void main(String[] args) {
    double num1 = 18.4;
    double num2 = 1.6;
    int sum = num1 + num2;
    System.out.println(sum);
  }
}
```

## Question 1.23 :

```java
public class Test {
  public static void main(String[] args) {
    double num1 = 13.6;
    double num2 = 2.5;
    int sum = (int)num1 + (int)num2;
    System.out.println(sum);
  }
}
```

## Question 1.24 :

```java
public class Test {
  public static void main(String[] args) {
    double num1 = 13.6;
    double num2 = 2.5;
    int sum = (int)(num1 + num2);
    System.out.println(sum);
  }
}
```

## Question 1.25 :

```java
public class Test {
  public static void main(String[] args) {
    int num = 96;
    char a = num;
    System.out.println(a);
  }
}
```


## Question 1.26 :

```java
public class Test {
  public static void main(String[] args) {
    System.out.println( (float)(int)2017.89432 );
  }
}
```

## Question 1.27:

Pour cette question nous allons revisiter la méthode principale **main**. Comme vous l’avez vu précédemment, la méthode main doit contenir l’argument **String args[]**. Cet argument permet de fournir des données au programme lors de son lancement. Pour ce faire, il suffit de fournir les donnes via la ligne de commande de la manière suivante :

```java
> java MyProgram one two
```

Où **args** contient maintenant les chaînes de caractères « one » et « two ». On peut alors manipuler la variable args comme un tableau régulier.

Voici un **exemple** :

Maintenant, construisez la classe « Sum » qui fait la conversion de tous les éléments sur la ligne de commande, de **String** en **int**, et fait aussi la **somme** des éléments.

_Indice: Utiliser les méthodes de la classe « Integer » fournies dans la documentation Java_

```java
> javac Sum.java
> java Sum 1 2 3 4 5
```

Votre programme doit avoir une sortie similaire à:

```java
The sum is 15
```

Voici un cours vidéo qui explique le processus étape par étape : [https://www.youtube.com/watch?v=38C2lJTbJNU](https://www.youtube.com/watch?v=38C2lJTbJNU)


# Part 2: Programmation orientée objet

## Objectifs

* **Implémenter** des classes simples
* **Créer** des associations entre classes
* **Approfondir** la notion d'encapsulation de données

Pour cette partie du laboratoire, vous devez créer trois classes : **Combination, DoorLock** et **SecurityAgent**. On souhaite explorer le concept d'association entre des classes. Ainsi, un objet de la classe **DoorLock** possède une variable d'instance de type référence vers un objet de la classe **Combination**. Un objet de la classe **SecurityAgent** possède une référence vers un objet de la classe **DoorLock** , mais aussi, une référence vers un objet de la classe **Combination**. Ainsi, les objets **SecurityAgent** et **DoorLock** ont tous les deux accès au même objet **Combination**.

Dans une classe **Test**, nous tentons de forcer le verrou. Ce programme tente de forcer l'ouverture du verrou à l'aide de combinaisons de chiffres générées aléatoirement. Afin que le programme trouve la bonne combinaison rapidement, chaque chiffre de la combinaison prend ses valeurs dans l'intervalle 1…5\. Après trois essais infructueux, le verrou devient inutilisable, il faut donc demander à l'objet **SecurityAgent** de le réactiver.

### Combination

Vous allez soumettre cet exercice. Téléchargez et complétez le fichier de démarrage ici:

* Combination.java

Créez une classe, nommée **Combination**, afin de contenir trois valeurs entières (de type int).

1. déclarez toutes les variables d'instance nécessaires afin de contenir ces trois valeurs entières ;
2. définir un constructeur, **public Combination(int first, int second, int third)**, afin d'initialiser les valeurs de cet objet ;
3. implémentez la méthode d'instance **public boolean equals(Combination otherx)**, telle que **equals** retourne la valeur **true** si l'objet désigné par le paramètre **other** contient les mêmes valeurs, dans le même ordre, que cet objet ; l'ordre des variables est le même que l'ordre des paramètres du constructeur. Étant donné les énoncés suivants :

```java
 Combination c1, c2, c3;

 c1 = new Combination(1, 2, 3);
 c2 = new Combination(1, 2, 3);
 c3 = new Combination(3, 2, 1);
```

**c1.equals(c2)** retourne **true** mais **c1.equals(c3)** retourne **false** ;

4. finalement, implémentez la méthode **public String toString()** afin de retourner une chaîne de caractères représentant l'état de cet objet, et telle que les valeurs des variables d'instances soient séparées par le symbole « :». Étant donné,

```java
Combination c1;
c1 = new Combination(1, 2, 3);
System.out.println(c1);
```

**_le résultat affiché sera «1 :2 :3»._**

L'interface de la classe **Combination** est constituée des méthodes suivantes : le constructeur, la méthode **equals** ainsi que la méthode **toString**.

En principe, les données devraient être validées. En particulier, toutes les valeurs devraient faire partie de l'intervalle 1 à 5\. Cependant, puisque nous n'avons pas encore les outils nécessaires afin de traiter les situations exceptionnelles, nous assumerons (pour l'instant) que toutes données sont valides, ainsi aucune validation ne sera nécessaire.

**Note** : mon implémentation pour cette classe fait environ 20 lignes, sans compter les lignes blanches. Il ne s'agit pas de créer l'implémentation la plus compacte. Je vous donne ces informations afin que vous puissiez évaluer la complexité des tâches.

### DoorLock

Vous allez soumettre cet exercise. Téléchargez et complétez le fichier de démarrage ici:

* DoorLock.java

Créez une classe **DoorLock** (simplement un verrou ou une serrure) ayant les caractéristiques suivantes :

1.  déclarez une constante de type int, nommée **MAX_NUMBER_OF_ATTEMPTS**, que vous initialiserez à la valeur 3 ;
2.  variables d'instance. La classe **DoorLock** doit posséder toutes les variables d'instance nécessaires afin de
    i.  désigner un objet de la classe Combination,
    ii.  déterminer si la serrure est ouverte ou verrouillée,
    iii.  savoir si la serrure est activée ou non, et
    iv.  connaître le nombre d'essais ratés pour ouvrir cette serrure ;
3.  la classe n'a qu'un constructeur, **DoorLock(Combination combination)**. Ce dernier initialise cette instance à l'aide de valeur reçue en paramètre. Lorsqu'un objet de cette classe est créé
    i.  la serrure est verrouillée,
    ii.  l'objet est activé et
    iii.  le nombre de tentatives ratées doit être mis à zéro ;
4.  implémentez la méthode d'instance **public boolean isOpen()** qui retourne **true** si le verrou est ouvert et **false** sinon ;
5.  implémentez la méthode d'instance **public boolean isActivated()** qui retourne **true** si ce verrou est activé et **false** sinon ;
6.  implémentez la méthode d'instance **public void activate(Combination c)** qui modifie l'état de l'objet afin de représenter l'état actif du verrou si la bonne combinaison est passée en argument, c'est-à-dire que la valeur du paramètre c est la même («equals») que celle de la combinaison de cet objet ;
7.  finalement, implémentez la méthode d'instance **public boolean open(Combination combination)** qui
    i.  n'ouvre le verrou que s'il est actif, si la combinaison passée en argument est la même que la combinaison de ce verrou alors la méthode change l'état de l'objet afin de représenter l'état ouvert, et doit remettre à zéro le compte du nombre d'essais ratés,
    ii.  sinon, c'est à dire la mauvaise combinaison a été passée en argument, alors le nombre d'essais ratés est incrémenté de un,
    iii.  si le nombre d'essais ratés atteint la valeur MAX_NUMBER_OF_ATTEMPTS alors le verrou doit être désactivé.

**Note :** mon implémentation compte environ 40 lignes, sans compter les lignes blanches.

### SecurityAgent (si le temps le permet)

Créez la classe **SecurityAgent** telle que décrite ci-bas.

1.  variables d'instances. Un agent de sécurité est responsable d'un seul verrou. Déclarez toutes les variables d'instance nécessaires afin qu'un agent de sécurité
    i.  mémorise (stock) une combinaison et
    ii.  ait accès au verrou dont il est responsable, c'est à dire une référence vers un objet de la classe DoorLock ;
2.  implémentez un constructeur sans paramètre tel que lorsqu'un nouvel agent est créé
    i.  il crée aussi une nouvelle combinaison et sauve une référence vers cet objet,
    ii.  il crée aussi un nouveau verrou (instance de la classe DoorLock) à l'aide de la combinaison sauvegardée. Afin de simplifier l'implémentation, vous pouvez toujours utiliser la même combinaison :

```java
Combination secret;
secret = new Combination(1,2,3);
```

si **secret** est le nom de la variable d'instance qui désigne la combinaison. Sinon, laissez les agents de sécurité utiliser leur imagination, de sorte que chaque agent de sécurité «invente» une nouvelle combinaison qu'il est le seul à connaître.

```java
int first, second, third;

first = (int) (Math.random()*5) + 1;
second = (int) (Math.random()*5) + 1;
third = (int) (Math.random()*5) + 1;

secret = new Combination(first, second, third);
```

Voici une façon plus élégante d'obtenir le même résultat :

```java
java.util.Random generator;
generator = new  java.util.Random();

int first, second, third;

first = generator.nextInt(5) + 1;
second = generator.nextInt(5) + 1;
third = generator.nextInt(5) + 1;

secret = new Combination(first, second, third);
```

les valeurs valides appartiennent à l'intervalle 1 à 5.

3.  implémentez la méthode d'instance **public DoorLock getDoorLock()** qui retourne une référence vers un objet de la classe **DoorLock** sauvegardé par cet agent ;
4.  implémentez la méthode d'instance **public void activateDoorLock()** qui ré-active le verrou à l'aide de la combinaison sauvegardée.

**_Observation :_** mon implémentation comporte environ 15 lignes de code.

### programme Main

Une classe SecurityAgency accompagne ce laboratoire. Cependant, je vous suggère de l'utiliser que lorsque les classes ci-haut auront été amplement validées.

La classe Test contient une méthode main qui

1.  Elle utilise un argument de ligne de commande qui représentant le nombre maximum de tentatives de forcer.
2.  Elle crée un agent de sécurité, nommé bob ;
3.  elle demande à bob l'accès au verrou ;
4.  elle utilise une approche naïve afin de forcer la serrure
5.  Suite à trois essais ratés, le verrou sera désactivé, il faut alors demander à bob de le réactiver.
6.  Lorsque le verrou a été forcé, la méthode imprime la combinaison ainsi que le nombre d'échecs.

N'oubliez pas de passer une valeur sur la ligne de commande. Voici quelques exemples :

```java
> java SecurityAgency 300
Success!
Number of attemtps: 266
The combination is: 3:1:3

> java SecurityAgency 10
Success!
Number of attemtps: 1
The combination is: 4:1:5

> java SecurityAgency 120
Success!
Number of attemtps: 115
The combination is: 2:2:1

> java SecurityAgency 400
Success!
Number of attemtps: 383
The combination is: 2:4:5

> java SecurityAgency 90
Success!
Number of attemtps: 89
The combination is: 3:5:1

> java SecurityAgency 8
Failed!
Reached the maximum number of attempts before finding the combination!
```

**Attention :** si l'une ou l'autre des méthodes est implémentée incorrectement et si vous ne donnez pas l'argument de la ligne de comande, il se peut que la méthode main soit prise dans une boucle infinie, utilisez alors Ctrl-c afin de terminer le processus.

**Suggestion :** construisez des classes tests pour chacune de vos classes.

* SecurityAgency.java

## Resources

* [https://docs.oracle.com/javase/tutorial/getStarted/application/index.html](https://docs.oracle.com/javase/tutorial/getStarted/application/index.html)
* [https://docs.oracle.com/javase/tutorial/getStarted/cupojava/win32.html](https://docs.oracle.com/javase/tutorial/getStarted/cupojava/win32.html)
* [https://docs.oracle.com/javase/tutorial/getStarted/cupojava/unix.html](https://docs.oracle.com/javase/tutorial/getStarted/cupojava/unix.html)
* [https://docs.oracle.com/javase/tutorial/getStarted/problems/index.html](https://docs.oracle.com/javase/tutorial/getStarted/problems/index.html)
