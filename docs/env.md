# Environnement d'exécution

Dans l'espace, le nanosatellite sera équipé d'une puce matérielle pour encoder une vidéo à partir d'images brutes. Notre client, Mr. Cassagne, nous a mis à disposition l'EM780, une machine distante située au Laboratoire d'Informatique de Paris 6.

## Procédure pour utiliser la puce matérielle

### Copier les images sur la machine EM780

Nous avons des vidéos de météores en local, nous allons copier les vidéos sur le disque dur de l'EM780 qui a des encodeurs similaires à ceux que l'on aura sur le satellite.

Pour se connecter à la machine :

```
ssh em780.mono.lip6.ext
```

Puis on copie les vidéos de la manière suivante :

(en local) scp fichier-sur-la-machine em780.mono.lip6.ext:~/
(sur l'em780) mv v03.mp4 /scratch/<\username>-nfs
De plus, FFMPEG est déjà installé sur la machine, on pourra donc utiliser directement les commandes FFMPEG depuis la machine.

### Transformer une vidéo compressée au format ppm

Pour le moment nous avons des vidéos de météores dans des formats compressés (H.264 ou MPEG-4) que nous avons pu récupérer sur l'EM780. Or la caméra du satellite récupère des images au format ppm (format brut). Nous voulons donc transformer nos vidéos compressées en images au format ppm pour ensuite donner ces images à la puce afin qu'elle les compresse. La commande suivante permet de le faire en créant un répertoire stockant les images :

```
mkdir -p output_images && ffmpeg -i video.mpg output_images/image%d.ppm
```
### Compresser les images ppm

Enfin pour compresser les images nous allons adresser l'un des deux GPUs présent sur l'EM780 :

adresser la puce sur le GPU embarqué AMD Radeon 780M (avec VAAPI)
adresser la puce sur le GPU externe NVidia GeForce RTX 3090 (dans ce cas il faut utiliser NVENC)
L'option 1 est la meilleure car la puce est sur le SoC, c'est-à-dire que le GPU est directement sur la puce ce qui est plus proche de la réalité dans un nano-satellite. L'option 2 est certainement plus facile car NVENC est bien supporté et documenté en général.

## Utilisation des GPUs

### NVidia GeForce RTX 3090

Nous avons réussi à utiliser le GPU Nvidia avec la commande suivante :

```
ffmpeg -hwaccel cuda -framerate 30 -i output_images/image%d.ppm -c:v h264_nvenc -preset fast -b:v 5M compressed_video.mp4 -loglevel verbose
```

Ce qui est important à retenir est -hwaccel cuda qui active l'accélération matérielle CUDA pour optimiser le traitement ainsi que -c:v h264_nvenc qui utilise NVENC pour encoder la vidéo au format H.264. Dans la commande on donne le répertoire avec les images au format ppm et on indique le nom et le format de la vidéo en sortie.

On peut aussi regarder l'utilisation du GPU en parallèle avec nvidia-smi et comparer la consommation d'énergie avant et pendant la compression. Nous trouvons une consommation de 28W sans processus en cours tandis que la consommation est de 108W en lançant notre algorithme. Il y a donc une augmentation de 80 watts, nous pouvons donc conclure que FFMPEG utilise bien le GPU. Cela nous permettra de simuler la compression dans l'espace.

### AMD Radeon 780M

Pour utiliser le GPU AMD Radeon on va essayer d'utiliser la bibliothèque VAAPI. Avec la commande suivante on adresse l'AMD Radeon 780M :

```
ffmpeg -vaapi_device /dev/dri/renderD128 -i output_images/image%d.ppm -vf 'format=nv12,hwupload' -c:v h264_vaapi -qp 24 -preset fast compressed_video.mp4
```

L'idée est la même que précédemment avec -vaapi_device /dev/dri/renderD128 qui spécifie le périphérique VAAPI à utiliser, -vf 'format=nv12,hwupload' qui convertit les images au format compatible VAAPI (nv12) et les télécharge sur le GPU. Et enfin -c:v h264_vaapi qui utilise VAAPI pour encoder en H.264.

Nous n'avons pas réussi à utiliser l'AMD Radeon du fait de bibliothèques trop compliquées à installer. Pour la suite nous utiliserons donc uniquement le GPU NVidia GeForce RTX 3090.