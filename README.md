# Test technique Livenexx 
### *Poste : Lead développeur Symfony*

>Durée : 45 minutes maximum

>15 Questions Symfony - 10 questions PHP - 5 questions SQL

>Bonne réponse = 1 pts, Mauvaise réponse = -1 pts, Pas de réponse = 0 pts

# Symfony

### 1- Dans les templates twig, quelles fonctions sont disponibles pour aider au traitement des formulaires ?

*Plusieurs réponses attendues.*

- A] `form_show()`
- B] `form_start()`
- C] `form_display()`
- D] `form_row()`

### 2- On considère le code suivant :

```php
$entityManager = $this->getDoctrine()->getManager();
$product = new Product();
$product->setName('Laptop');
$product->setPrice(2499);
$product->setDescription('Polished and bitten');
```

Quel code doit-on ajouter pour sauver le produit dans la base de données ?

- A] `$entityManager->persist($product); $entityManager->flush();`
- B] `$entityManager->flush($product);`
- C] `$entityManager->save($product);`
- D] `$entityManager->persist($product);`

### 3- On considère le code suivant :

```php
/**
* @Route("/home")
*/
class HomeController extends Controller {
    /**
    * @Route("/categories", name="categories")
    */
    public function categoriesAction() {
        return $this->json([
            ['name' => 'cats'],
            ['name' => 'dogs'],
            ['name' => 'horses'],
        ]);
    }
}

```

Qu'est-ce que retourne un appel à l'url `/home/categories` ?

- A] Il retourne le template correspondant et l'affiche avec les données fournies
- B] Il renvoie une erreur : la fonction json() n'est pas définie dans le controlleur
- C] Il retourne un objet Json avec le format suivant : `[{"name":"cats"},{"name":"dogs"},{"name":"horses"}]`
- D] Il renvoie une erreur : aucun template pour le chemin donné
- E] Il retourne la chaîne suivante : `cats dogs horses`

### 4- Quelle syntaxe peut-on utiliser pour exécuter du code en Twig ?

- A] `{% %}`
- B] `{{ }}`
- C] `{# #}`
- D] `{ }`

### 5- On considère le code suivant

```php
/**
* @Route("/products/{productId}/edit", name = "edit_product")
*
*/
public function editProductAction(Request $request, Product $product)
{
    // ...
}
```

Comment configure-t-on **ParamConverter** pour que le paramètre `productId` soit affecté à la propriété `id` de Product ?

- A] `@ParamConverter("product", options={"mapping": {"field": "id"}})`
- B] `@ParamConverter("product", options={"productId": "id"})`
- C] `@ParamConverter("product", options={"mapping": {"productId": "id"}})`
- D] `@ParamConverter("product", options={"mapping": {"Product": "id"}})`


### 6- Comment fait-on pour récupérer un paramètre POST appelée `foo` depuis l'objet `$request` de type Request ?

- A] `$request->request->get('foo')`
- B] `$request->get('foo')`
- C] `$request->post('foo')`
- D] `$request->query->get('foo')`
- E] `$request->post->get('foo')`
- F] `$request->parameter('foo')`


### 7- Un utilisateur est-il authentifié auprès de tous les firewalls après un login réussi ?

- A] Oui, c'est automatique
- B] Oui, si les firewalls ont la même valeur que l'option `context`
- C] Oui, si l'option `shared` vaut vrai
- D] Non, ce n'est pas possible, les firewalls sont indépendants les uns des autres

### 8- On considère le code suivant :


```php
class AddBookCommand extends Command
{

    public function __construct($requireTitle = true)
    {
        parent::__construct();
        $this->requireTitle = $requireTitle;
    }
    
    public function configure()
    {
        $this
        ->setName('book:add')
        ->setDescription('Add a new book.')
        ->addArgument('title',
        $this->requireTitle ? InputArgument::OPTIONAL : InputArgument::REQUIRED,
        'Book title');
    }
    
    protected function execute(InputInterface $input, OutputInterface $output)
    {
        $output->writeln('Adding new book...');
        // add new book with specified title
        $output->writeln('Book added!');
    }
}
```

Quel est le résultat de l'exécution de la commande `php bin/console book:add Titanic` ?

- A] La console affiche : `Adding new book... Book added!`
- B] Erreur : the title should be passed as `-title=Titanic`
- C] Erreur : `requireTitle` property is undefined
- D] Erreur : missing method `initialize()`


### 9- Vous souhaitez créer une nouvelle commande de console avec Symfony.

Quelle classe utiliseriez-vous pour créer des **styles de sortie personnalisés** ?

- A] Symfony\Component\Console\OutputFormatterStyle
- B] Symfony\Component\Console\OutputStyleFormatter
- C] Symfony\Component\Console\OutputStyle
- D] Symfony\Component\Console\OutputFormatter

### 10- On considère l'entité suivante

```php
/**
* @ORM\Entity()
*/
class Product
{
  // ...
  /**
  * @ORM\PrePersist
  */
  public function setCreatedAtValue()
  {
    $this->createdAt = new \DateTime();
  }
}
```

À quel moment la méthode `setCreatedAtValue()` sera-t-elle invoquée ?

- A] Avant que l'entité ne soit persistée en base de données
- B] Après que l'entité soit persistée en base de données
- C] Jamais : l'annotation `@ORM\PrePersist` n'existe pas
- D] Jamais : les callbacks du cyle de vie n'ont pas été activés par
- E] l'annotation `@ORM\HasLifecycleCallbacks()`


### 11- Quel type de réponse sera produit par le code suivant :

```php
use Symfony\Component\HttpFoundation\File\File;
use Symfony\Component\HttpFoundation\ResponseHeaderBag;

public function download()
{
    $file = new File('/invoices/companies/123/invoice.pdf');
    return $this->file($file,'company_123_invoice.pdf', ResponseHeaderBag::DISPOSITION_INLINE);
}
```

- A] StreamedResponse
- B] BinaryFileResponse
- C] FileResponse
- D] Erreur : nombre d'arguments invalide pour la fonction `file()`


### 12- Si vous souhaitez mettre en place un filtre de requêtes avec Symfony 3+, vous pouvez utiliser :

- A] Event Listeners
- B] Event Subscribers
- C] Event Listeners et Event Subscribers
- D] Le filtrage de requête n'est pas supporté par Symfony 3+


### 13- Parmi les exemples ci-contre, quel sont ceux qui permettent de charger un service dans un controlleur ?

- A] `$this->get('service.to.load')`
- B] `$this->getFromContainer('service.to.load')`
- C] Passé en tant que paramètre d'une action, par exemple : `public function GetBooksAction(BooksService $booksService) {}`
- D] `$this->getContainer()->get('service.to.load')`


### 14- Comment feriez-vous pour vérifier que vous pouvez utiliser la variable book depuis un template twig ?

- A] `{% if book is defined %}`
- B] `{% if book exists %}`
- C] `{% if book is present %}`
- D] `{% if book is available %}`

### 15- On considère les templates suivants :

`base.html.twig`

```php
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>{% block title %}John's Shop{% endblock %}</title>
    </head>
    <body>
        <div id="content">
            {% block body %}{% endblock %}
        </div>
    </body>
</html>
```

`page.html.twig`

```php
{% extends 'base.html.twig' %}
{% block title %}Products for cats{% endblock %}
{% block body %}
    <div>Good products for your cat</div>
{% endblock %}
```

Quel sera **le titre de la page** au chargement du template `page.html.twig` ?

- A] John's Shop
- B] Products for cats
- C] John's Shop - Products for cats
- D] Good products for your cat

# PHP

### 1- En PHP, un entier est stocké sur...

- A] 32 bits
- B] 64 bits
- C] 32 ou 64 bits : cela dépend de la plateforme

### 2- Parmi ces types de variables, sélectionnez ceux qui sont valides en PHP.

- A] integer
- B] long
- C] array
- D] string
- E] char

### 3- Répondez à cette question

Si la variable `$a` est égal à 7 et la variable `$b` est égale à `$a`, quelle est la valeur de `$$b` ?


### 4- Quelle est la valeur de la variable $sentence ?

```php
$a = 4;
$b = 10;
$sentence = "There are ".$a++." cakes for ".++$b." people.";
```

### 5- Quel serait le résultat du code ci-dessus ?

```php
$numbers = array('one', 'two', 'three', 'four');
$sliced = array_slice($numbers, -2, 1);
echo end($sliced);
```

- A] one
- B] two
- C] three
- D] four

### 6- Quelle fonction n'est pas une fonction PHP par défaut ?

- A] floatval
- B] print_r
- C] is_real
- D] getsize


### 7- Si vous exécutez le code suivant plusieurs fois :

`$encoded = md5(‘my test string’);`

Quelle proposition est vraie concernant de la valeur de `$encoded` ?

- A] Elle sera toujours la même
- B] Elle alterne entre deux valeurs
- C] Elle sera plus encodée à chaque fois

### 7- Quelles propositions sont évaluées à true ?

```php
$a = 47;
$b = 'test';
```

- A] `( $b || ($a<=75 && $a>=30) )`
- B] `( $b===true || ($a>=75 && $a<=30) )`
- C] `( $b && ($a<=75 || $a>=30) )`
- D] `( $b===true && ($a<=75 || $a>=30) )`


### 8- Quelles propositions convertissent le type de la variable $a en un entier ?

*Sélectionner toutes les bonnes réponses.*

```php
$a = '8';
echo gettype($a); // prints 'string'
```

- A] `settype($a, 'integer');`
- B] `$a = (int)$a;`
- C] `unset($a);`
- D] `is_integer($a);`


### 9- Quelle fonction permet d'obtenir les informations détaillées sur la version PHP quiest installée, avec les modules et les extensions ?

Répondre avec le nom de la fonction.

### 10- 
