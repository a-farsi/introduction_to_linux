# 1. Variable d'environnement:

Pour créer une variable d'environnement:
```
export NOM_VARIABLE_ENV=VALEUR
```
la variable d'environnement sera créée sur la session terminal en cours, mais ne sera pas persistanate si la sesssion termial est fermée ou expirée.
pour rendre les variables persistentes, il faudera modifier le fichier _.bashrc_.

Pour afficher la valeur d'une variable d'environnement : 
```
echo $NOM_VARIABLE_ENV
```
La commande qui permet d'afficher toutes les variables d'environnement est 
```
printenv
```
Pour supprimer une variable d'environnement :
```
unset NOM_VARIABLE_ENV
```
# 2. Manipumation de fichier et Dossier:

### 2.1 Creation de fichier et dossier:
Nous pouvons créer un fichier avec la commande suivate : 
```
touch NOM_FICHIER
```
Pour supprimer le fichier : 
```
rm NOM_FICHIER
```

Pour supprimer un répertoire:
```
rm -r NOM_REPERTOIRE
```
Copier un fichier et coller le dans un répertoire
```
cp ./NOM_FICHIER ./NOM_REPERTOIRE/
```

Copier le ficher et coller le dans un répertoire en lui affectant un autre nom:
```
cp ./NOM_FICHIER_1 ./NOM_REPERTOIRE/NOM_FICHIER_2
```

Déplacer le fichier dans un autre repertoire en le rennomant:
```
mv ./NOM_FICHIER_1 ./NOM_REPERTOIRE/NOM_FICHIER_2
```
### 2.2 Édition et lecture de fichier:

Pour écrire une phrase dans un fichier en écrasant son contenu:
```
echo hello world > NOM_FICHIER
```
Pour écrire dans un fichier en préservant son contenu dejà existant:
```
echo hello world >> NOM_FICHIER
```
Pour imprimer la sortie d'une commande dans un fichier, nous utilisons _>_ : 
```
ls / > NOM_FICHIER
```
Pour afficher le contenu d'un fichier sur le terminal:
```
cat NOM_FICHIER
```
Pour affciher que quelques lignes (2 pour cet exemple) du début :
```
head -n 2 file1
```

Pour afficher que quelques lignes (3 pour cette exemple) de la fin :
```
tail -n 3 file1
```
# 3. Les flux de redirection
### 3.1 Redirections des sorties
L'entrée standard, la sortie standard et l'erreur standard sont chacune associées à un descripteur de fichier.
 ```
 Entrée standard (stdin), son descripteur de fichier 0:   0< ou <  
 Sortie standard (stdout), son descripteur de fichier :    1> ou >
 Erreur standard (stderr), son descipteur de fichier 2:   2>
 ```
 
Pour rediriger le contenu du fichier log.txt vers la commande head :
```
head < log.txt
```
Nous créons un fichier file1 avec le contenu : "les entrees sorties sont magiques":
```
echo "les entrees sortie sont magique"  > file1
```
Pour afficher le contenu de file1 comme suit: 
```
cat file1 
```
Si nous executons la commande sur un fichier non existant, on aura une erreur 
```
cat no_file 
```
Pour rediriger la sortie d'erreur vers le fichier _error_file.txt_, nous devons executer la commande suivante : 
```
cat no_file 2> error_file.txt   
```

Nous pouvons définir que la sortie standard soit redirigée vers un premier fichier et que l'erreur soit redirigée vers un second fichier 
```
cat 1> business_log.txt 2> error_log.txt
```
Pour rediriger la sortie standard et la sortie d'erreur à la même sortie, nous executons la commande suivante : 
```
python script_python >> log.txt 2>&1    
```
# 4. Utilisateurs et droits

Linux est un système d'exploitation multi-utilisateurs.
Linux divise l'autorisation en 2 niveaux : La propriété (ownership) et les permissions.

### 4.1 La propriété : 
    La propriété est un aspect central de la gestion des fichiers et des répertoires. Elle permet de contrôler qui a accès à un fichier. Elle est étroitement liée aux concepts d'utilisateur (user), de groupe (group), et d'autres (others).

**Utilisateur** : est le propriétaire du fichier ou du répertoire
**Groupe** : est une collection d’utilisateurs. Chaque fichier est associé à un groupe.
**Autre** : représentent tous les autres utilisateurs du système qui ne sont ni le propriétaire, ni membres du groupe associé au fichier. 

### 4.2 la permission: 
    La permission determine quelles actions un utilisateur peut effectuer sur un fichier ou un  répertoire. 
Pour afficher les permission d'un fichier, lister les détails en format long: 
```
ls -l 
```
Si un fichier a ces permissions : **-rwxr-xr--** :
- Le signe **-** designe un fichier. Si c'était un répertoire, le charactère **d** l'aurait remplacé.
- Utilisateur (u): Le propriétaire a **rwx** (lecture, écriture, exécution). Il peut donc lire, modifier, et exécuter le fichier.
-Groupe (g):  Les membres du groupe ont **r-x** (lecture et exécution, mais pas écriture). Ils peuvent lire et exécuter, mais ne peuvent pas modifier le fichier.
-Autre (o) : Les autres utilisateurs ont **r - -** (lecture seulement). Ils peuvent uniquement lire le fichier.

Il est possible de changer le propriétaire et/ou le groupe d’un fichier ou d’un répertoire avec la commande **chown**.

Exemple de changer le propriétaire et le groupe à un fichier :
```   
sudo chown user2:group2 myfile.txt
```
Pour changer uniquement le groupe associé à un fichier ou un répertoire, utilisez **chgrp**.

Exemple de changer le groupe à un fichier 
```   
chgrp group2 myfile.txt
```

Pour changer les permissions d'un fichier, il faut utiliser la commande **chmod** :

```
chmod 777 file
```

Nous pouvons utiliser une représentation binaire des permissions : chaque chiffre correspond à un groupe d'utilisateurs:

    0 : - - -
    1 : - - x
    2 : - w -
    3 : - w x
    4 : r - -
    5 : r - x
    6 : r w -
    7 : r w x

La deuxième façon consiste à désigner le ou les groupes à qui l'on veut attribuer ou enlever des droits :
```
chmod a+rwx file
```

    a : les utilisateurs concernés par la modification a pour tous (all), u pour le propriétaire, g pour le groupe de l'utilisateur o pour les autres utilisateurs;
    + : est ce qu'on donne ou enlève des droits: + pour donner et - enlever ;
    rwx : Les droits à ajouter ou retirer.


### 4.3 Super utilisateur et sudo :

Le concept de super utilisateur et le sudo sont des éléments essentiels pour la gestion des droits et permissions

#### 4.3.1. Super utilisateur (root) :
Le super utilisateur, aussi appelé "**root**", est un compte spécial qui a tous les droits sur le système.
La commande pour se connecter en tant que super utilisateur est :
```
sudo su
```
#### 4.3.2. sudo : Superuser Do :
La commande **sudo** signifie "**Superuser Do**". Elle permet à un utilisateur normal d’exécuter des commandes avec les privilèges du super utilisateur, sans se connecter directement en tant que root.

Remarques :
 - utiliser sudo au lieu du compte root 
 - Le fichier de configuration /etc/sudoers permet de limiter les commandes qu’un utilisateur peut exécuter avec sudo.
 - Chaque commande exécutée avec sudo est enregistrée dans les logs.

# 5. Script Shell

## 5.1 Langage Bash
Un fichier bash contient une suite de lignes de codes écrites en Bash. Il contient à sa base, un shebang:
``` 
#!/bin/bash
```

Cela s'applique aussi sur un script Python par exemple, ou vous trouver une ligne du type 
```
#!/bin/python3
```
Pour executer le script bash, nous aurons besoin de lui affecter les droit comme suit :
```
chmod +x script.sh
```

## 5.2 Les bases en Bash

les Commentaires : utiliser  **#**
Les variables: eviter de l'espace, exp : 
```
my_var=Hello world!   #Doesn't work
```
S'il y a de l'esapce, utilisez des guillemets simples ou doubles :
```
my_var="Hello world!" 
```

Afficher une variable: 
```
echo $my_var
```

pour l'exécution des commandes nous pouvons utiliser :
1. les guillemets inversés `` appelés aussi (**backtiks**)
```
echo "Nous sommes le `date`"
```

2. Nous pouvons utiliser aussi $() :

```
echo "Nous sommes le $(date)"
```

## 5.3 Calcul arithmétique:
Nous utilisons **let** pour le calcul arithmétique.

```
let "a=1"
let b=2
```

Les guillemets ne sont nécessaires que lorsque l'expression est complèxe ou comporte plusieurs parties séparées par des espaces.

```
let "c = 1 + 2"
```

### Les tableaux : 
Déclarer un tableau : 
```
my_array=(hello world!)
```

Afficher un elément d'un tableau : 
```
echo ${my_array[0]}    #Affiche hello
```
Afficher le tableau complet : 
```
echo ${my_array[*]}
```

Pour attributer une nouvelle valaur au premier elément du tableau :
```
my_array[0]=Hi
```

nous pouvons attribuer des valeurs aux indices qui ne sont pas encore attribués dans le tableau :
```
my_array[5]=Cool
```

Remarque : les indices n'ont pas besoin de se suivre

### Boucles et conditions:
#### condition if:
    
Pour la condition if nous pouvons utiliser la structure  **if-then-fi** 
exemple:
```
prenom="Daniel"
if [ $prenom = "Daniel" ]
then
echo "Salut Daniel !"
fi
```
Avec **else**, l'exemple s'ecrit comme suit : 

```
prenom="Daniel"
if [ $prenom = "Daniel" ]
then
echo "Salut Daniel !"
else
echo "Bonjour" + $prenom +"!"
fi
```

Nous pouvons introduire plusiuers conditions avec **elif** 
```
prenom="Diane"
if [ $prenom = "Daniel" ]
then
echo "Salut Daniel ! "
elif [ $prenom = "Diane" ]
then
echo "Salut Diane"
else
echo "Bonjour" + $prenom +"!"
fi
```
Pour créer des conditions, nous pouvons utiliser : 

    $var1 = $var2   # teste l'égalité des tableaux de caractères ;
    $var1 != $var2  # teste l'inégalité des tableaux de caractères ;
    -z $variable    # teste si le tableau de caractères est vide ;
    -n $variable    # teste si le tableau de caractères n'est pas vide ;
    $var1 -eq $var2 # teste l'égalité de valeurs numériques ;
    $var1 -ne $var2 # teste l'inégalité de valeurs numériques ;
    $var1 -gt $var2 # teste var1 > var2 ;
    $var1 -lt $var2 # teste var1 < var2 ;
    $var1 -ge $var2 # teste var1 >= var2 ;
    $var1 -le $var2 # teste var1 <= var2 ;

Pour combiner deux conditions, nous pouvons utiliser les opérateurs logiques **&&** (ET),  **||** (OU):
```
prenom="Diane"
nom="Datascientest"
if [ $prenom="Daniel" ] && [ $nom="Dina" ]
then
echo "Bonjour Daniel Dina"
else
echo "Bonjour" + $prenom + $nom
fi
```

#### Boucle while:

```
let i=0
while [ $i -lt 10 ]
do
let "i=i+1"
done
echo $i
```

#### Boucle for
```
for x in '1st iteration' '2nd iteration' '3rd iteration'
do
echo $x
done
```

Pour générer une séquence de nombres nous pouvons utiliser la commande **seq** :
```
seq 3 10
```

Pour générer les nombres avec un pas nous utilisons la commande: 
```
seq [début] [pas] [fin]
```

La command seq peut être utlisée avec la boucle **for** comme suit:
```
for i in $(seq 1 5)
do
  echo "Nombre : $i"
done
```

#### Fonctions

Il y a deux façons pour définir une fonction :
```
my_function () {
echo "Nous pouvons faire quelque chose ici"
}
```

Ou 
```
function my_function {
echo "Nous pouvons faire quelque chose ici"
}
```

Les paramètres sont toujours référencés par leur position à l'aide des variables spéciales $1, $2, $3, etc.
```
function my_function {
echo "Premier argument"
echo $1
echo "Second argument"
echo $2
}

my_function "Dina" 24 # Exécuter la fonction 
```
# 6 Processus
Un processus est une instance d'un programme en cours d'exécution.
-Chaque processus est identifié par un numéro unique appelé PID.
-Un processus doit avoir un état, car il peut être en cours d'exécution, en attente (par exemple, en attente d'une ressource), ou terminé.
-Les processus peuvent être créés par d'autres processus (le processus parent crée un processus enfant).

Un processus peut être ecexuté en avant-plan (Foreground) ou en arriere-plan (Background).

## 6.1 Mettre un processus en arrière-plan :
 lancez un programme ou une commande, en ajoutant un **&** à la fin de la commande:
```
commande &
```

## 6.2 Mettre un processus en avant-plan :
Un processus peut être ramené en avant-plan à l'aide de la commande **fg** (foreground).
```
fg
```

Si plusieurs processus sont en arrière-plan, vous pouvez spécifier lequel ramener en avant-plan en donnant son numéro de travail:
```
fg %1
```

## 6.3 Mettre un processus en arrière-plan après l'avoir lancé en avant-plan :
    - Suspendre le processus avec Ctrl + Z. 
    - Mettre le processus en arrière-plan avec la commande : bg

### Outils suplementaires:

**htop**: Cet utilitaire informe l'utilisateur sur tous les processus en cours sur la machine Linux.
pour quiter il faut taper **q**.
```
htop
```

**ps**: pour affichier l'état des processus.

```
ps ux
```

## 7. Crontab

Crontab est un fichier de configuration utilisé pour programmer des tâches automatisées à exécuter à des moments spécifiques.
Ces tâches, appelées jobs cron, peuvent être des scripts, des commandes ou des programmes.

### 7.2 Syntaxe d'un Cron Job

voici la commande 
```
* * * * * command/script
```

De gauche à droite :

    Le premier * correspond aux Minutes (0-59) ;
    Le deuxième * correspond aux Heures (0-23) ;
    Le troisième * correspond au Jour du mois (1-31) ;
    Le quatrième * correspond au Mois de l'année (1-12) ;
    Le cinquième * correspond au Jour de la semaine (0-6, du dimanche au samedi).

Pour spécifier plusieurs valeurs dans un champ, utilisez les symboles d'opérateur suivants :

    Astérisque (*) : Pour spécifier toutes les valeurs possibles pour un champ ;
    Tiret (-) : Pour spécifier une plage de valeurs ;
    La virgule (,) : Pour spécifier une liste de valeurs ;
    Le séparateur (/) : Pour spécifier une valeur d'étape.

Voici quelques exemples grâce à la syntaxe ci-dessus :

Exécutez un Cron Job à 5h15 tous les jours :
```
15 5 * * * command/script
```
Exécutez un Cron Job à 5h15 chaque 2eme jour du mois :
```
15 5 2 * * command/script
```
Exécutez un Cron Job toutes les 5h :
```
0 */5 * * * command/script
```
Exécutez un Cron Job chaque lundi et mercredi du mois de janvier et février à minuit.
```
0 0 * jan,feb mon,wed command/script
```

### 7.4 Commandes usuelles
    crontab -e : Pour modifier le fichier crontab de l'utilisateur actuel ;
    crontab -l : Pour afficher le contenu du fichier crontab ;
    crontab -u [nom d'utilisateur] : Pour modifier le fichier crontab d'un autre utilisateur ;
    crontab -r : Pour supprimer le fichier crontab de l'utilisateur actuel ;
    crontab -i : Pour afficher une invite avant de supprimer le fichier crontab de l'utilisateur actuel.
