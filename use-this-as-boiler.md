# Boiler Admin – Template Repo

Detta repo används som en **mall (template)** för nya projekt.

Repo: :contentReference[oaicite:0]{index=0}

---

# 🚀 Skapa ett nytt projekt från mallen

## 1. Klona template-repot

```bash
git clone git@github.com:Jojjeboy/boiler-admin.git my-new-project
cd my-new-project
```

---

## 2. Koppla bort origin och lägg till nytt repo

Skapa först ett nytt tomt repo på GitHub (utan README), och kör sedan:

```bash
git remote rename origin template
git remote add origin git@github.com:YOUR-ORG/my-new-project.git
```

Nu har du:

- `origin` → ditt nya projekt
- `template` → boiler-admin (mallen)

---

# 🔍 Verifiera remotes

```bash
git remote -v
```

Du ska se något i stil med:

```
origin    git@github.com:YOUR-ORG/my-new-project.git (fetch)
origin    git@github.com:YOUR-ORG/my-new-project.git (push)
template  git@github.com:Jojjeboy/boiler-admin.git (fetch)
template  git@github.com:Jojjeboy/boiler-admin.git (push)
```

---

# 🔄 Hämta uppdateringar från mallen

När boiler-admin uppdateras kan du ta in förbättringar i ditt projekt.

## 1. Hämta senaste ändringar

```bash
git fetch template
```

---

## 2. Slå ihop med ditt projekt

```bash
git merge template/main
```

Alternativt (om du vill ha rak historik):

```bash
git rebase template/main
```

---

# ⚠️ Viktigt

- Ändringar i ditt projekt påverkar inte template-repot
- Uppdateringar i template kommer inte automatiskt in i projektet
- Konflikter kan uppstå om samma filer ändrats i båda

---

# 💡 Rekommenderad arbetsmodell

- `boiler-admin` = standardstruktur och gemensamma verktyg
- Projektet = egen produktlogik
- Uppdateringar hämtas in manuellt vid behov

---

# 🧭 Snabbkommando

```bash
git fetch template && git merge template/main
```