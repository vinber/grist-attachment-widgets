<img width="100" height="100" alt="image" align="left" src="https://github.com/user-attachments/assets/aa0d6d54-e54d-4c6d-803b-5f8667baa98e" />

===============================

**Fait avec 💙 chez [OpenSourcePolitics](https://opensourcepolitics.eu/)**

===============================

# Le problème

Si vous êtes un utilisateur fréquent de Grist, vous avez probablement déjà utilisé la fonctionnalité "Pièce jointe".

Si c'est le cas, vous avez peut être remarqué qu'utiliser la pièce jointe autre part (dans Grist ou à l'exterieur) n'est pas évident.

> Comment afficher mes documents dans Grist 🤔 ?

> Comment générer des liens 🤷 ?

> Comment faire pour utiliser mes pièces jointes dans des templates HTML ou Markdown 😕 ?


Pas d'inquiétude, j'ai la solution pour vous !


# La solution

Ce dépôt contient plusieurs widgets selon votre cas d'usage.

Pour installer un de ces widgets, vous pouvez vous référer à [la documentation sur les widgets](https://support.getgrist.com/page-widgets/) et utiliser le widget "custom URL" en collant les URLs fournies plus bas.

## Voir des pièces jointes dans Grist

Ce widget affiche tous les documents dans la colonne sélectionnée.

Il permet de visionner:
- des images
- des PDFs

Et il n'est pas limité à un seul document, il est possible de naviguer parmi plusieurs pièces jointes.

Lien à copier-coller: 

`https://rambip.github.io/grist-attachment-widgets/viewer`


## Générer des URL pour utilisation dans Grist

Ce widget génère des liens à la volée à partir de l'API Grist. Vous pouvez utiliser ces liens dans des templates HTML ou markdown par exemple.

Lien à copier-coller: 

`https://rambip.github.io/grist-attachment-widgets/url-generator`

⚠️ Les urls générées sont temporaires. Vous ne pouvez les utiliser sur des sites externes, lisez la section suivante si c'est ce que vous voulez.

*Note: ce widget génère uniquement des liens pour la première pièce-jointe de la colonne*


## Générer des URLs pour utilisation externe.

Pas besoin de widget personnalisé pour ce cas d'usage !

Il suffit de:
1. Rendre votre document public (sinon, des sources externes ne peuvent pas accéder aux images)
2. Utiliser cette formule (remplacer $Attachment par le bon nom de colonne)

```python
# extract url and document ID
url, end = SELF_HYPERLINK().split("/o/docs")
doc_id = end.split("/")[1]
# extract first attachment.
if not $Attachment:
    return None
attach_id = $Attachment.id[0]
# use API to provide attachment URL
return f"{url}/api/docs/{doc_id}/attachments/{attach_id}/download"
```

*Note: cette formule génère uniquement des liens pour la première pièce-jointe de la colonne*

# Inspiration

Il y a beaucoup de discussion sur ce sujet dans le forums grist français et international:

- [inspiration for attachment viewer](https://community.getgrist.com/t/attachment-viewer-widget-needed/11558/3)
- [grist API funciton that makes it work](https://support.getgrist.com/code/modules/grist_plugin_api/#getaccesstoken)
