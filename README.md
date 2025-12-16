get_next_line est un projet du cursus 42 dont l’objectif est d’implémenter une fonction permettant de lire un fichier ligne par ligne à partir d’un descripteur de fichier.

À chaque appel, la fonction retourne la ligne suivante du fichier jusqu’à la fin du fichier (EOF).

Prototype
char *get_next_line(int fd);

Fonctionnement
La fonction utilise la fonction système read pour lire le fichier par blocs de taille BUFFER_SIZE.
Les données lues sont stockées dans un buffer statique afin de conserver les informations non encore traitées entre deux appels successifs à get_next_line.

La fonction retourne :

une ligne terminée par un caractère '\n' si celui-ci est présent

NULL lorsque la fin du fichier est atteinte ou en cas d’erreur

Organisation du code
get_next_line
Fonction principale qui orchestre la lecture du fichier, l’extraction de la ligne et la gestion du buffer.

read_file
Lit le fichier par blocs de taille BUFFER_SIZE et concatène les données jusqu’à trouver un caractère de fin de ligne ou atteindre la fin du fichier.

ft_line
Extrait depuis le buffer la ligne complète à retourner, incluant le caractère '\n' si présent.

ft_next
Conserve la partie du buffer située après la ligne extraite afin de préparer l’appel suivant à get_next_line.

ft_free
Concatène deux chaînes de caractères et libère l’ancienne zone mémoire afin d’éviter les fuites.

Gestion des buffers
Un buffer statique est utilisé pour mémoriser les données restantes entre deux appels.
Un buffer temporaire reçoit les données lues par la fonction read.
Toute la mémoire est allouée dynamiquement et correctement libérée.

Exemple d’utilisation
Ouverture d’un fichier avec open, appels successifs à get_next_line pour lire chaque ligne, libération de la mémoire retournée et fermeture du fichier à la fin.

Compilation
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c

Points importants
BUFFER_SIZE est défini à la compilation.
La fonction gère correctement plusieurs appels consécutifs.
Aucune fuite mémoire n’est présente.
Le comportement est conforme aux exigences du projet 42.
