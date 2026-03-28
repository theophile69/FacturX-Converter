# FacturX Converter — Installation and Usage Guide

## Requirements
- macOS 12 or higher
- FileMaker Pro 2025

## Installation

1. Unzip the `FacturX-Installer.zip` file on your Desktop
2. Open the `FacturX-Installer` folder
3. Double-click on `Lancer l'installation.command`

   *Or from the Terminal:*
```
cd ~/Desktop/FacturX-Installer && bash install.sh
```

4. Follow the on-screen instructions

## FileMaker Configuration

In your ScriptMaker, create a script with the following steps:

**1. Set variable `$Executable`**
```
"/Applications/FacturX/convertFacturX.sh"
```

**2. Set variable `$pdf`**
```
MyTable::PDFPathField
```

**3. Set variable `$xml`**
```
MyTable::XMLPathField
```

**4. Set variable `$out`**
```
MyTable::OutputPathField
```

**5. Set variable `$cmd`**
```
"\"" & $Executable & "\"" & " " & 
"\"" & $pdf & "\"" & " " & 
"\"" & $xml & "\"" & " " & 
"\"" & $out & "\""
```

**6. Perform AppleScript (calculated)**
```
"do shell script " & Quote($cmd)
```

## Testing the script from the Terminal (optional)

If you wish to verify that the conversion works correctly before configuring FileMaker, you can test the script directly from the Terminal:

```bash
/Applications/FacturX/convertFacturX.sh \
    "/path/to/your/invoice.pdf" \
    "/path/to/your/facturx.xml" \
    "/path/to/your/output.pdf"
```

If everything works correctly, you should see `OK:/path/to/your/output.pdf` at the end of the output.

## Result
The PDF/A-3b file with embedded Factur-X XML is created at the path defined in `$out`.

## Support
If you encounter any issues, verify that Java and Ghostscript are properly installed:
```
java -version
gs --version
```

## Licenses

This `convertFacturX.sh` script is distributed under the MIT License.
Copyright (c) 2026 Théophile Megny-Marquet

The integrated tools are subject to their respective licenses:
- **Ghostscript**: GNU AGPL v3 — free use permitted, source code available
- **Mustang-CLI**: Apache 2.0 — commercial use permitted
- **Java (OpenJDK)**: GPL v2 with Classpath Exception — commercial use permitted

### Note on Ghostscript
Ghostscript is distributed under the GNU AGPL v3 license. If you wish to
integrate this tool into a commercial product, a commercial license is
available from Artifex Software (artifex.com).
