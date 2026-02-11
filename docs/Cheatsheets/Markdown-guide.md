# Markdown Cheat Sheet (MkDocs)

Cette page est ton antisèche. Copie le code pour l'utiliser dans tes write-ups.

---

## 1. Les Alertes (Admonitions)

### Ce que tu veux obtenir :
!!! note "Note"
    Ceci est une note simple.

!!! success "Validé"
    Ceci est un succès.

!!! danger "Critique"
    Attention danger.

### Le code à copier :
```markdown
!!! note "Titre"
    Ton texte ici (4 espaces au début).

!!! success "Succès"
    Bravo.

!!! danger "Attention"
    Danger.
```

---

## 2. Les Onglets (Tabs)

### Ce que tu veux obtenir :
=== "Linux"
    Utilise `nc` pour écouter.
=== "Windows"
    Utilise `powercat`.

### Le code à copier :
```markdown
=== "Linux"
    Contenu Linux.

=== "Windows"
    Contenu Windows.
```

---

## 3. Le Code Coloré

### Ce que tu veux obtenir :
```python
import os
print("Hello World")
```

### Le code à copier :
```markdown
```python
import os
print("Hello World")
```
*(Remplace python par `powershell`, `bash`, `html`, etc.)*

---


## 4. Les Boutons

### Ce que tu veux obtenir :
[Télécharger le PDF](https://google.com){ .md-button .md-button--primary }
[Lien simple](https://google.com){ .md-button }

### Le code à copier :
```markdown
[Texte Bouton](lien){ .md-button .md-button--primary }
[Bouton Secondaire](lien){ .md-button }
```

---

## 5. Les Tableaux

### Ce que tu veux obtenir :
| Service | Port |
| :--- | :--- |
| SSH | 22 |
| HTTP | 80 |

### Le code à copier :
```markdown
| Colonne 1 | Colonne 2 |
| :--- | :--- |
| Ligne 1 | Info |
| Ligne 2 | Info |
```
