# FacturX Converter — Guide d'installation et d'utilisation

## Prérequis
- macOS 12 ou supérieur
- FileMaker Pro 2025

## Installation

1. Décompresse le fichier `FacturX-Installer.zip` sur ton Bureau
2. Ouvre le dossier `FacturX-Installer`
3. Double-clique sur `Lancer l'installation.command`

   *Ou depuis le Terminal :*
```
cd ~/Desktop/FacturX-Installer && bash install.sh
```

4. Suis les instructions à l'écran

## Tester le script depuis le Terminal (optionnel)

Si tu souhaites vérifier que la conversion fonctionne correctement avant de configurer FileMaker, tu peux tester le script directement depuis le Terminal :

```bash
/Applications/FacturX/convertFacturX.sh \
    "/chemin/vers/ta/facture.pdf" \
    "/chemin/vers/ton/facturx.xml" \
    "/chemin/vers/ton/fichier_sortie.pdf"
```

Si tout fonctionne correctement, tu devrais voir `OK:/chemin/vers/ton/fichier_sortie.pdf` à la fin de l'affichage.

## Configuration FileMaker

Dans ton ScriptMaker, crée un script avec ces étapes :

**1. Définir variable `$Executable`**
```
"/Applications/FacturX/convertFacturX.sh"
```

**2. Définir variable `$pdf`**
```
MaTable::ChampCheminPDF
```

**3. Définir variable `$xml`**
```
MaTable::ChampCheminXML
```

**4. Définir variable `$out`**
```
MaTable::ChampCheminSortie
```

**5. Définir variable `$cmd`**
```
"\"" & $Executable & "\"" & " " & 
"\"" & $pdf & "\"" & " " & 
"\"" & $xml & "\"" & " " & 
"\"" & $out & "\""
```

**6. Exécuter AppleScript (calculé)**
```
"do shell script " & Quote($cmd)
```

## Résultat
Le fichier PDF/A-3b avec XML Factur-X embarqué est créé au chemin défini dans `$out`.

## Support
En cas de problème, vérifiez que Java et Ghostscript sont bien installés :
```
java -version
gs --version
```

## Licences

Ce script `convertFacturX.sh` est distribué sous licence MIT.
Copyright (c) 2026 Théophile Megny-Marquet

Les outils intégrés sont soumis à leurs licences respectives :
- **Ghostscript** : GNU AGPL v3 — usage gratuit autorisé, code source disponible
- **Mustang-CLI** : Apache 2.0 — usage commercial autorisé
- **Java (OpenJDK)** : GPL v2 avec exception Classpath — usage commercial autorisé

### Note sur Ghostscript
Ghostscript est distribué sous licence GNU AGPL v3. Si vous souhaitez
intégrer cet outil dans un produit commercial, une licence commerciale
est disponible auprès d'Artifex Software (artifex.com).