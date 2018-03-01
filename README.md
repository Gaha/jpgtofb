# Préparation des photos pour Facebook

## Réduction de la photo

La photo sera redimentionné avec 2000px pour le plus grand coté

```bash
convert $IMAGE_SOURCE -resize 2000*2000 $IMAGE_DEST
```

## Ajout de la signature

Une fichier .png sera ajouté en bas à droite de l'image

```bash
composite -dissolve 70 signature.jpg $IMAGE_SOURCE -gravity SouthEast -geometry +0+20 $IMAGE_DEST
```

## Ajout du copyright

Ajout d'une image copyricht en bas à droite de l'image

```bash
composite -dissolve 20 copyright.png $IMAGE_SOURCE -gravity SouthWest -geometry +5+5 $IMAGE_DEST
```

## Font utilisé

https://www.dafont.com/fr/lovely-home.font?text=Vincent+Desessard
https://www.dafont.com/fr/back-to-black.font?text=Vincent+Desessard
https://www.dafont.com/fr/bite-chocolate.font?text=Vince%7Bnt+Desess%5Dard

## EXIF

Utilisation de l'outils ExifTool

A VOIR : utilisation d'un fichier XML pour ajouter toutes les options en une seule fois

### Suppression des exif

```bash
exiftool -all= $FILE
```

### Ajout de l'auteur

```bash
exiftool -Artist="Vincent Desessard" $FILE
exiftool -XPAuthor="Vincent Desessard" $FILE
```

### Ajout du Copyright

```bash
exiftool -CopyrightNotice="Creative Commons (BY NC SA)" $FILE
exiftool -Copyright="Creative Commons (BY NC SA)" $FILE
```
### Ajout des mots clé

```bash
exiftool -Keywords="VNVB, Volley, Vandoeuvre" $FILE
exiftool -XPKeywords="VNVB;Volley;Vandoeuvre" $FILE
```

### autres ajout?

* Title
* XP Title

0x9003 Date and Time (Original)
0x9004 Date and Time (Digitized)
Prise de vue (ne pas supprimer)

https://mirrors.creativecommons.org/presskit/buttons/88x31/png/by-nc-sa.eu.png

convert 2018-EDF.jpg -mattecolor "#414141" -frame 5 DSC_9471bis.jp

convert by-nc-sa.eu.png -resize 100x100 copy.png

composite -dissolve 20 copy.png 2018-EDF.jpg -gravity SouthWest -geometry +5+5 test2.jpg

## Script final

```bash
#/bin/sh

for fichier in *.jpg
do
	fichier2=`echo $fichier | cut -d'.' -f1`\_reduit.`echo $fichier | cut -d'.' -f2`
	convert $fichier -resize 995 -crop 995x1280+0-0 $fichier2
done
```
