---
title: Trucs et astuces sur l'encodage de textes hiéroglyphiques
taxonomy:
    category: docs
---


Avant de décrire le manuel de codage lui-même, j'aimerais faire une ou deux remarques sur la façon dont on devrait encoder un texte hiéroglyphique.

Typiquement, vous avez une source, qui peut être a) une source imprimée, avec des hiéroglyphes composés, b) une photographie ou un fac-similé fidèle du texte original, ou c) des hiéroglyphes manuscrits tirés d'une publication égyptologique (par exemple, les *Urkunden*).

Vous devez décider à quel point vous devez être fidèle à l'original, et ce n'est pas une question simple. Le premier point est que vous pouvez être sûr que **votre texte en Manuel de Codage ne peut pas être un fac-similé**, donc, d'une manière ou d'une autre, il trahira l'original. Si le texte est finalement un texte hiératique, vous créez déjà quelque chose de complètement différent de toute façon.

Maintenant, lorsque vous avez un signe, devez-vous rechercher la variante la plus précise ou en utiliser une en quelque sorte standardisée ? Pour y répondre, il faut se demander si cette variante est pertinente, dans le texte et dans l'usage que l'on entend en faire. Par exemple, dans les textes de Kanaïs de Séthi Ier, le pronom à la première personne utilise de nombreuses variantes de A40 <span class='mdc'>A40</span>. Si vous destinez le texte à une étude grammaticale, ce n'est pas très pertinent. Si vous vous demandez s'il s'agit d'un jeu libre visant à ajouter de la diversité au texte, alors vous pouvez prendre le temps d'encoder les variantes.

En règle générale, **si vous êtes débutant en égyptien,** je vous conseille d'encoder le signe « standard », car il vous obligera à **lire le texte, et non à copier des signes**. Le problème que vous rencontrez quand vous voulez être très précis, c'est que vous trouverez de nombreux cas de variantes qui n'ont de toute façon aucun encodage, et vous prenez le risque de tromper vos lecteurs en donnant une fausse impression de précision... et souvent, de choisir un signe sans rapport qui ressemble simplement à celui que vous voulez.

Lorsque votre source est une version manuscrite d'un texte, comme dans les *Urkunden*, méfiez-vous d'un point : à moins qu'un signe ne soit très particulier, un égyptologue dessinera généralement ses glyphes de la manière la plus simple. Cela signifie, par exemple, qu'il utilisera V23A (<span class='mdc'>V23A</span>) au lieu de V22 (<span class='mdc'>V22</span>), qui est le signe hiéroglyphique normal. Vous devez comprendre cela, et lorsqu'un choix de signe est simplement causé par la main individuelle de l'auteur, rendez-le avec le signe « standard ». En revanche, lorsque l'auteur a dessiné une forme de signe très spécifique, il peut être intéressant de lui accorder plus d'attention.

## Encodage de textes hiératiques


La règle ci-dessus est encore plus forte pour les textes hiératiques. Il ne sert à rien de faire une distinction entre <span class='mdc'>V23A</span> et <span class='mdc'>V22</span>, car les deux sont rendus de la même manière en hiératique !

Or, il y a un certain nombre de particularités du hiératique qui méritent plus d'attention. Celles-ci ont été identifiées par sir Alan Gardiner dans son article [« The Transcription of New Kingdom Hieratic », *JEA* 15 (1929), p. 48-55](https://www.jstor.org/stable/3854012). Le rendu des textes hiératiques doit faire allusion à la façon dont les signes originaux sont placés, afin de permettre au lecteur de comprendre la raison du rendu, et de revenir à l'original si nécessaire.

JSesh inclut un certain nombre de signes utiles pour le rendu des textes hiératiques :

| Signe                          | Code  | Utilisation                                                                                                                                                                                                                         |
| ------------------------------ | ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span class='mdc'>Ff1</span>   | Ff1   | un signe particulier aux textes ramessides, qui sert en quelque sorte de « joker ». C'est différent du signe Z5 (<span class='mdc'>Z5</span>). Vous pouvez l'obtenir dans JSesh en tapant « , » (virgule) puis la touche espace. |
| <span class='mdc'>Ff100</span> | Ff100 | un signe non standard, **bouche-trou en forme de point**. Utilisez-le pour rendre les différents points qu'un scribe peut utiliser, lorsqu'ils ne sont pas une ponctuation.                                                          |
| <span class='mdc'>Ff101</span> | Ff101 | un signe non standard, **bouche-trou horizontal**. Utilisez-le pour rendre divers signes horizontaux dénués de sens que le scribe peut utiliser pour combler les vides.                                                              |

JSesh inclut également des signes spécifiques pour les nombres dans les textes hiératiques. Dans ces textes, le « déterminatif » Z1 est souvent plus petit que le « chiffre » Z1. Un rendu négligent peut entraîner la lecture de <span class='mdc'>h:r-W:ra-Z1-Z1-Z1</span> comme hrw 3 alors que l'original a <span class='mdc'>h:r-W:ra-Z1-Ff302</span>, qui est clairement hrw 2.

## Disposition des signes

Utilisez les différentes capacités de « ligature » de JSesh, et **si tout le reste échoue,** optez pour l'« éditeur de groupe ». Ne perdez pas non plus votre temps à essayer d'obtenir exactement les mêmes tailles et proportions de signes que dans l'original, sauf si vous comptez les discuter.

Quelques points intéressants :

Dans le groupe « M17-M17 », les signes doivent souvent être plus proches que ne le permet l'espacement standard de JSesh (en fait, cela est déjà indiqué par sir A. Gardiner dans le catalogue de ses polices). Si l'on écrit `i*i:k` (c'est-à-dire deux yods groupés horizontalement et un « k » en dessous), le groupe créé par JSesh est ![](pAyk2.png?classes=inline). Pour obtenir la meilleure mise en page : ![](pAyk1.png?classes=inline), c'est simple : il suffit de ligaturer les deux yods (tapez « i » « & » « i », par exemple).
