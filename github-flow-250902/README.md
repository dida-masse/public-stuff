# GitHub Flow exempel

Till detta exempel finns en presentation av GitHub flow [här](https://dida-masse.github.io/public-stuff/github-flow-250902/github_flow_intro_1.html)  


## Innehåll

> Detta är ett par enkla exempel för att praktiskt visa hur man kan använda Github Flow i ett litet team.
> 
> Första exemplet visa hur ett repo skapas, hur collaborators bjuds in, skapa feature branch, samt gör ett PR.
> 
> Andra exemplet visar en konflikt, där ändringar görs i samma fil, och hur man skulle kunna lösa den.


**Team:**
- Person A (msc)
- Person B (efo)

# EXEMPEL skapa repo och branches samt PR 
Vi ska skapa ett repo, en feature branch, göra en uppdatering och slutligen göra ett PR som merge:as.

Person A får vara den som skapar repot.  
Person B är den som ska göra en feature branch, göra en uppdatering och sedan skapa ett PR.  


## Person A - Skapa och förbereda repositoryt

### 1: Skapa nytt repository på GitHub
1. Gå till GitHub.com
2. Klicka på "New repository"
3. Namnge det till något som passar
4. Markera "Add a README file"
5. Markera "Add .gitignore" → och tex välj "Node"
6. Klicka "Create repository"

### 2: Klona repositoryt lokalt
```bash
git clone https://github.com/[DITT-ANVÄNDARNAMN]/kursschema-webapp.git
cd kursschema-webapp
```

### 3: Vi skapar en fil och lägger till i repot
```bash
# i detta exempel gör vi bara en fil
touch index.html
```

### 4: vi lägger till lite innehåll till filen

**index.html:**
```html
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="UTF-8">
    <title>Testar GHF</title>

</head>
<body>
    <header>
        <h1>hello world</h1>
    </header>

    <main>

    </main>

</body>
</html>
```

---

### 5: Initial commit och push
```bash
git add .
git commit -m "Initial commit: första filen"
git push origin main
```

### 6: Lägg till Person B som collaborator på github.com
1. Gå till repot på GitHub
2. Klicka "Settings" → "Collaborators and teams"
3. Klicka "Add people"
4. Lägg till Person B:s GitHub-användarnamn

---

## Person B - Första feature branch

Person B ska börja "arbeta i repot" genom att skapa en feature-branch.  
Kom ihåg att vi INTE arbetar direkt på main - vi gör all utveckling i feature branches.

### 1: Klona repot

Enklast är att gå in på repot och kopiera korrekt url (klicka på 'Code' och ta ssh-url:en).

```bash
git clone https://github.com/[PERSON-A-ANVÄNDARNAMN]/NAMN-PÅ-REPOT.git
cd namn-på-repot
```

---

### 2: Skapa feature branch
```bash
# Kontrollera att du är på main och har senaste versionen
git checkout main
git pull origin main

# Skapa och växla till ny feature branch
git checkout -b feature/passande-namn-på-det-som-ska-utvecklas
```

---

### 3: Lägg till innehåll i koden (t ex i detta exempel i index.html)
Uppdatera **index.html**
```html
<!-- <main> -->
<h2>Hej jag heter 'namn på Person B'</h2>
```

---

### 4: Commit:a ändringarna
```bash
git add .
git commit -m "Koncist och passande commit message."
```

### 7: Pusha feature branch

I detta steg "skickar" vi uppdateringarna till fjärr-repot (GitHub).

```bash
git push origin feature/passande-namn-på-det-som-ska-utvecklas
```

---

### 6: Skapa Pull Request på GitHub

Viär klara med en del i vår utveckling av vår feature.  
I detta fall är vi klara med hela branchen.

1. Gå till repositoryt på GitHub
2. GitHub visar automatiskt "Compare & pull request" - klicka på den
3. Fyll i PR-information, t ex som nedan. Bara det är tydligt och konkret, t ex:
   - **Title:** "La till mitt namn i index.html"
   - **Description:**
   ```
   ## Ändringar
   - Lagt till mitt namn i index.html

   ## Test
   - [x] Sidan laddas korrekt
   ```
4. Klicka "Create pull request"

---

## Person A OCH Person B - Code Review (granska PR)

### 1: Granska/review Pull Request
1. Gå till "Pull requests" tab
2. Öppna PR:n från Person B
3. Här kan vi gå igenom de ändringar/tillägg som har gjorts i detta PR.
4. Lägg till kommentarer (om man vill göra det):
   - **Positiv feedback:** "Bra struktur på filen!"
   - **Förslag:** "Kanske vi kan lägga till error handling här?"

### 2: Testa ändringarna lokalt (om det finns tester som ska köras)

detta steget gör vi inte eftersom vi inte har några tester.

```bash
# Hämta PR-branchen för lokal testning
git fetch origin
git checkout feature/namn-på-feature-branchen
```

### 3: Godkänn och merge:a PR
1. I PR:n, klicka "Review changes"
2. Välj "Approve"
3. Skriv passande kommentare, t ex: "Ser bra ut! Tack för den snygga implementeringen."
Följande alternativ finns nu:
   - **Merge:** Klicka "Merge pull request"
   - **Squash and merge:** Klicka "Squash and merge" (för att hålla historiken ren)
   - **Rebase and merge:** Klicka "Rebase and merge" (för att hålla historiken ren)

### 4: (optional) ta bort feature branch

Om man vill ta bort branchen i projektet så kan man göra det - det är upp till teamet.  
Notera dock att efter ett tag kan det bli väldigt många branches som "ligger och skräpar".  
För att ta bort:  
1. Tar bort branchen från remote:
```bash
git push origin --delete feature/namn-på-feature-branchen
```

Eller så tar vi bort branches direkt på GitHub (om man nu vill ta bort dom).  


2. Och så synkar vi med main:
```bash
git checkout main
git pull origin main
```

---
---
---

# EXEMPEL - konflikt

I det här exemplet ska både Person A och Person B skapa varsin feature branch. Bägge personerna gör förändringar i samma fil.  
Bägger personer ska sedan göra ett PR men en av dem kommer att få en merge-konflikt.  
Exemplet är tänkt att visa hur man skulle kunna lösa en sådan konflikt.


## Person A - gör en ny feature branch

Person A ska alltså göra ny funktionalitet.  
För säkerhets skull så synkar vi först mot main med en pull;

### 1: Synka lokal main branch
```bash
git checkout main
git pull origin main
```

### 2: Skapa ny feature branch
```bash
git checkout -b feature/adding-my-name
```

### 3: Uppdatera och skriva ny kod
Person A gör lite valfria uppdateringar i index.html för det här exemplets skull, t ex lägger till sitt namn;

```html
<h1>Hej jag heter Masse</h1>
```

---

### 4: Commit och push
detta commitar och pushar Person A:

```bash
git add .
git commit -m "Lagt till mitt namn"

git push origin feature/adding-my-name
```

---

### 5: Person A skapar ett Pull Request

Person A är i detta fallet klar med sin branch och gör ett PR.  

---

## Person B - "Samtidig utveckling"

Samtidigt/under tiden gör Person B en egen feature branch.

### 1: Person B skapar ny branch (medan Person A:s PR väntar)

Person B ser till att denna är på main och hämta "det senaste";  
```bash
git checkout main
git pull origin main
git checkout -b feature/ghf-reading-tips
```

### 2: Person B ändrar i index.html

Person B gör ändringar i index.html - detta kommer innebära en konflikt.

T ex i index.html;

```html
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <title>GH Flow</title>
</head>
<body>
    <header>
        <h1>Lästips om GitHub Flow</h1>

    </header>

    <main>
        <ul>
            <li><a href="https://davidregalado255.medium.com/what-is-github-flow-49fdda7be1b1">what-is-github-flow</a></li>
            <li><a href="https://docs.github.com/en/get-started/using-github/github-flow">docs.github.com/en/get-started/using-github/github-flow</a></li>
            <li><a href="https://githubflow.github.io/">githubflow.github.io/</a></li>
            <li><a href="https://medium.com/@YodgorbekKomilo/the-complete-guide-to-github-flow-a-practical-tutorial-for-developers-0ea8e5ad1c1e">the-complete-guide-to-github-flow-a-practical-tutorial-for-developers</a></li>
        </ul>
    </main>

</body>
</html>
```

---

### 3: Commit och push

Person B commitar och pushar

```bash
git add .
git commit -m "Let us completely change the content of our landing page"

git push origin feature/ghf-reading-tips
```

---

## 4: Merge conflict

När nu Person B gör ett PR kommer en konflikt ske.  
Den, Person A, som är först med sitt PR kommer inte att få konflikt - denna är ju klar med ett mergat PR.  
För den andra, Person B, som gör sitt PR senare kommer nu att få konflikt vilket måste lösas.

Det finns ett antal olika vägar att gå, det viktiga här är att man är överens om vilken, dvs vilka ändringar som ska godtas.  

För exemplets skull vill vi ha Person B:s förändringar, men vi godkände alltså först Person A:s PR.  


### Person B:s PR får merge conflict
1. När Person B nu gör ett PR så kommer det att bli konflikt/conflict.
2. Person B måste (bör) lösa konflikten i samråd med Person A...

Man kan antingen lösa konflikten i PR:t på GitHub.com eller lokalt.
På GitHub blir det i så fall i webb-gränssnittet.
Lokalt gör man det med git-kommandon och att editera filerna.

> [!TIP]
> På GitHub och inne på själva sidan för PR finns instruktioner för hur man gör det via command line
> länken heter något i stil med _View command line instructions_

Person B väljer att lösa konflikten lokalt;
- eftersom vi har ett redan mergat PR behöver Person B synka main
- efter att ha hämtat hem senaste förändringarna ska sedan main mergas med B's branch.
- gör ändringarna och pusha sedan

```bash
# vi ställer oss i main (för att hämta senaste i o m att vi har ett annat PR mergat)
git checkout main
# hämta de senaste ändringarna från main
git pull origin main  

# nu checkar vi ut vår feature branch som vi precis arbetade i
git checkout feature/ghf-reading-tips

# och nu ska vi merga vår feature branch mot main.
# här kommer konflikten
git merge main
# nu får vi öppna de filer som innehåller konflikter och 
# "rätta till" så att det blir som "det ska vara".
# när man är klar;
git add .
git commit - m "conflict solved"
# pusha ändringarna till vår feature branch (Person A's PR i nu mergat i vårt PR)
# -u sätter också upp tracking
git push -u origin feature/person-b

# gå till PR:t på GitHub och detta kan mergas (borde alltså vara ok)
```

Här kan man läsa mer om att lösa konflikter via terminalen;  
https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line 

## 5: "Final review" och merge av PR

Nu har vi löst konflikten och Person B har ett öppet PR som skulle kunna mergas.  
Gå igenom/Code review "som vanligt" med det öppna PR:et.  

Till sist så är det viktigt att alla team-medlemmar "städar upp", så att alla har alla ändringar;

```bash
# Båda personerna kör:
git checkout main
git pull origin main

# och eventuellt städa upp branches lokalt
git branch -d feature/namn-på-feature
```

---

## Sammanfattning av GitHub Flow

1. **main branch** är alltid deploybar
2. **Feature branches** skapas för varje ny funktion
3. **Descriptive commits** med tydliga meddelanden
4. **Pull Requests** för kodgranskning
5. **Code review** före merge
6. **Merge och cleanup** av branches


## Slutligen några tips

- Använd gärna beskrivande och tydliga branch-namn
- Skriv tydliga commit-meddelanden
- Gör små, atomära Pull Requests (så att det inte blir alldeles för stor kodmassa)
- Granska ändringar tillsammans - gör Code review på alla PR
- Kommunicera med andra teamet vid merge konflikter
