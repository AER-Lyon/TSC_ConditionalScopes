# Boucles et conditionnal scopes

## Portée des variables

On peut se figurer un programme C comme des blocs d'instructions consécutifs.

```c
char *text = "Hello world";
printf("%s", text);
```
```
> Hello world
```

Ici, une suite de 2 instructions.

> La variable déclarée dans la première ligne est accessible et utilisée par la deuxième.
___

Il est possible de regrouper le code en l'englobant entre des accolades.

```c
{
    {
        char *text = "Hello world";
        printf("%s", text);
    }
    my_putstr(text);
}
```
```
main.c: In function ‘main’:
main.c:17:18: error: ‘text’ undeclared (first use in this function);
   17 |     my_putstr(text)
```

L'appel à la fonction `my_putstr` n'a pas accès à la variable: **elle est détruite à la sortie de son scope.**

___

Dans le cas suivant, la variable `text` est accessible dans l'ensemble du code.

> Les variables sont accessibles au sein de leur scope et des scopes enfants.

```c
{
    char *text = "Hello world";
    {
        printf("%s", text);
    }
    my_putstr(text);
}
```
```
> Hello worldHello world
```

## Scopes conditionnels

Utiliser les scopes comme présenté précédemment peut sembler peu utile. Les scopes prennent leur interet lorsqu'ils sont associés à une déclaration conditionnelle.

```c
{
    char *text = "Hello world";
    /* Déclaration conditionnelle */ {
        printf("%s", text);
    }
    my_putstr(text);
}
```
> La déclaration conditionnelle s'écrit avant l'accollade ouvrant le scope.

Une déclaration conditionnelle rend l'execution du code englobé par le scope facultative et dépendante d'une condition donnée.

La déclaration conditionnelle s'écrit:

```c
if (/* Condition */)
```

Par exemple:
```c
{
    char *text = "Hello world";
    if (my_strlen(text) > 15) {
        printf("%s", text);
    }
    my_putstr(text);
}
```
```
> Hello world
```

## Boucles

De la même manière, on peut remplacer la déclaration conditionnelle par une déclaration de boucle.

```c
{
    char *text = "Hello world";
    /* Déclaration de boucle */ {
        printf("%s", text);
    }
}
```

Par exemple:
```c
{
    char *text = "Hello world";
    int i = 0;
    while (i < 5) {
        printf("%s", text);
        i++;
    }
}
```
```
> Hello worldHello worldHello worldHello worldHello world
```

Le scope précédé par la déclaration `while` s'executera du temps que la condition est vraie.

Une alternative à `while` plus concise existe également, elle s'utilise à l'aide du mot clé `for` et regroupe la logique de déclaration, d'incrémentation et la condition d'arrêt dans la déclaration.

Elle s'écrit comme il suit:
```c
for (int i = 0; i < 5; i++)
```

On choisit généralement entre les deux selon le critère suivant:

- Boucle for: lorsque le nombre des itérations est connu.
- Boucle while: lorsque le nombre des itérations est inconnu.

## Pour s'entraîner:
1. Écrire un programme qui fait la somme des 10 premiers nombres entiers positifs

2. Écrire un programme C qui affiche les 9 tables de multiplication pour les entiers de 1 à 9. Chaque table comporte 9 éléments, sous la forme suivante:
    ```
    1 2 3 4 5 6 7 8 9
    2 4 6 8 . . .
    ...
    9 18 27 36 . . 
    ```

3. La banque X nous accorde un prêt si la somme de vos intrêts dépasse 1000 euros. L’intrêt est de 3.5 % par an.

    Voici un exemple pour vous guider dans vos affaires financières:
    ```
    Somme initiale place: 2000 euros
    1-ire anne : intret = (2000 x 3.5)/100 = 70
    2-ime anne : intret = (2070 x 3.5)/100 = 72.45
    ...
    On arrete quand : intret > 1000 euros.
    ```

    En suivant l’exemple précédent écrire une fonction qui, à partir d'une somme initialle donnée en paramètre, détermine le nombre d’années nécessaires pour bénéficier d’un prêt.

