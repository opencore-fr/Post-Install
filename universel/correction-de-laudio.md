# Correction de l'audio

## Correction de l'audio avec AppleALC <a href="#fixing-audio-with-applealc" id="fixing-audio-with-applealc"></a>

Pour commencer, nous supposerons que vous avez déjà installé Lilu et AppleALC, si vous ne savez pas s'il a été installé correctement, vous pouvez exécuter cette commande dans le terminal (cela vérifiera également si AppleHDA est chargé, car sans lui, AppleALC n'a rien à correctif):

```bash
kextstat | grep -E "AppleHDA|AppleALC|Lilu"
```

Si les 3 s'affichent, vous êtes prêt pour la suite. Assurez-vous que VoodooHDA n'est installé. Sinon, cela entrera en conflit avec AppleALC.

Si vous rencontrez des problèmes, consultez la section Dépannage

## Trouver votre ID&#x20;

Donc, pour cet exemple, nous supposerons que votre codec est ALC1220. Pour vérifier le vôtre, vous avez plusieurs options :



* Vérifié la page de spécifications de la carte mère ou le manuel
* Vérifiez le Gestionnaire de périphériques dans Windows
* Vérifiez HWInfo64 dans Windows
  * Assurez vous que "Résumé uniquement" et "Capteurs uniquement" sont désélectionnés lors de l'ouverture
* Vérifiez AIDA64 Extreme dans Windows
* Exécutez `cat` dans le terminal sous Linux
  * `cat /proc/asound/card0/codec#0 | less`

Maintenant, avec votre codec, nous chercher dans la liste des codecs pris en charge par AppleALC: [https://github.com/acidanthera/AppleALC/wiki/Supported-codecs](https://github.com/acidanthera/AppleALC/wiki/Supported-codecs)

Avec le codec l'ALC1220, nous obtenons :

```
0x100003, layout 1, 2, 3, 5, 7, 11, 13, 15, 16, 21, 27, 28, 29, 34
```

Donc, à partir de là, nous avons 2 choses:
