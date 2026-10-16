# ffmpegcmd

> Générateur de commandes FFmpeg pour Windows : choisis le format, le codec et la qualité, copie la commande prête à coller dans CMD ou PowerShell.

![Platform](https://img.shields.io/badge/platform-Web%20%2F%20Windows-informational) ![Stack](https://img.shields.io/badge/stack-HTML%20%2F%20CSS%20%2F%20JS-orange)

## À propos

**FFmpeg Generator** est une page HTML autonome qui construit des commandes de conversion vidéo FFmpeg sans avoir à retenir la syntaxe. Elle vise Windows : les chemins collés via « Copier comme chemin d'accès » sont nettoyés automatiquement, et le mode dossier génère une boucle PowerShell pour convertir plusieurs fichiers d'un coup.

## Fonctionnalités

- Deux modes : **Fichier unique** ou **Dossier (batch PowerShell)**.
- Chemin de l'exécutable FFmpeg configurable (par défaut `C:\ffmpeg\bin\ffmpeg.exe`).
- Suppression automatique des guillemets autour des chemins collés.
- Conteneurs de sortie et codecs proposés :

| Conteneur | Codecs vidéo | Audio |
|---|---|---|
| MP4 | H.264 (libx264), H.265 / HEVC (libx265) | AAC 320k, AAC 192k, copie |
| MKV | H.264, H.265 / HEVC, VP9 (libvpx-vp9) | AAC 320k, AAC 192k, Opus 192k, copie |
| WebM | VP9 (libvpx-vp9), VP8 (libvpx) | Opus 192k, Vorbis 192k, copie |
| MOV | H.264, H.265 / HEVC | AAC 320k, AAC 192k, copie |

- Qualité CRF : 17 (ultra haute), 20 (excellente), 23 (standard), 28 (fichier léger).
- Preset de vitesse : ultrafast, medium, slow (désactivé pour WebM ; VP8/VP9 utilisent `-b:v 0 -crf`).
- Fichier de sortie nommé `<nom>_HQ.<format>` à côté de la source.
- Bouton **⧉ Copier la commande** vers le presse-papiers.

## Installation

Prérequis : [FFmpeg](https://ffmpeg.org/) installé sur la machine qui exécutera la commande.

Ouvre `index.html` dans un navigateur — aucune dépendance, aucun build.

## Utilisation

1. Choisis le **mode** (fichier unique ou dossier).
2. Indique le chemin de l'**exécutable FFmpeg** et le **fichier** ou **dossier source** (avec ou sans guillemets).
3. Sélectionne le **conteneur**, le **codec vidéo**, l'**audio**, la **qualité (CRF)** et le **preset**.
4. Clique sur **⧉ Copier la commande** et colle-la dans CMD ou PowerShell (le mode dossier nécessite PowerShell).

Exemple de commande générée (fichier unique, valeurs par défaut) :

```
"C:\ffmpeg\bin\ffmpeg.exe" -i "C:\Users\Ellie\Downloads\video.mkv" -c:v libx264 -crf 23 -preset slow -c:a aac -b:a 320k "C:\Users\Ellie\Downloads\video_HQ.mp4"
```

En mode dossier, tous les fichiers `*.mkv, *.mp4, *.mov, *.avi, *.webm, *.flv, *.m4v, *.ts` du dossier sont convertis via `Get-ChildItem … | ForEach-Object { … }`.

## Stack technique

HTML, CSS, JavaScript vanilla (fichier unique `index.html`).

## Crédits & licence

Utilise [FFmpeg](https://ffmpeg.org/) (non inclus).

Aucune licence n'est spécifiée — tous droits réservés.

---

<p align="center">
  Fait par <a href="https://github.com/elisalien">Élisalien</a> ·
  <a href="https://gitlab.com/elisalien/catalog">Catalogue des shaders, sources & logiciels</a>
</p>
