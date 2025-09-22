# Nog enkele interessante topics

## Jupyter Notebooks

### Wat zijn Jupyter Notebooks

Zie: https://jupyter.org/

Een notebook is een document dat zowel tekst als Pythoncode bevat. De tekst is geschreven in markdown (https://www.markdownguide.org/). De code kan onmiddellijk uitgevoerd worden en de output verschijnt onmiddellijk in de notebook.

Een notebook kan gemakkelijk omgezet worden naar een html-document.

Deze notebooks worden veel gebruikt in data-analyse, wetenschappelijk  onderzoek, en onderwijs om code, uitleg en resultaten op een  overzichtelijke manier bij elkaar te presenteren. Het is een populair  hulpmiddel in het veld van data science en machine learning.

Naast Python ondersteunen Jupyter notbooks ook R  (maar intussen ook andere talen)

### Hoe voer je een notebook uit?

Een Jupyter notebook bewerken en uitvoeren gaat als volgt:

1. **Installatie**:

   - Installeer Jupyter via pip:

     ```
     pip install jupyter
     ```

1. **Opstarten**:
   - Open een terminal of command prompt.
   - Navigeer naar de gewenste map of blijf in de huidige directory.
   - Typ `jupyter notebook` en druk op Enter.
   - Dit start de Jupyter server op en opent een webpagina in je standaard webbrowser met een overzicht van de beschikbare notebooks en bestanden.
2. **Een nieuw notebook maken**:
   - Klik in de Jupyter interface op de knop 'New' en kies het gewenste programmeertaal (meestal Python).
3. **Bewerken**:
   - Een notebook bestaat uit cellen die ofwel code ofwel opgemaakte tekst (Markdown) bevatten.
   - Klik op een cel om deze te bewerken.
   - Voor het invoeren van code: typ je code gewoon in een code-cel.
   - Voor tekst: wissel de cel naar 'Markdown' modus (te vinden in het dropdown-menu bovenaan) en voer je opgemaakte tekst in.
4. **Uitvoeren**:
   - Voer een cel uit door erop te klikken en op de 'Run' knop te drukken bovenaan, of gebruik de sneltoets `Shift + Enter`.
   - De output van de code verschijnt direct onder de betreffende cel.
   - Je kunt meerdere cellen achter elkaar uitvoeren en zo een reeks berekeningen of analyses stap voor stap doorlopen.
5. **Opslaan**:
   - Het notebook wordt automatisch op gezette tijden opgeslagen.
   - Je kunt ook op de 'Save' knop drukken (ziet eruit als een floppy disk) bovenaan de interface of de sneltoets `Ctrl + S` (of `Cmd + S` op Mac) gebruiken.
6. **Aanvullende mogelijkheden**:
   - Je kunt cellen verplaatsen, verwijderen of toevoegen met behulp van de toolbar bovenaan.
   - De Jupyter interface biedt ook mogelijkheden voor het in- en uitzoomen van cellen, het zoeken in het notebook, en andere nuttige functies.
7. **Afsluiten**:
   - Sluit het notebook door op de 'Close and Halt' optie in het 'File' menu te klikken.
   - Stop de Jupyter server door in je terminal of command prompt `Ctrl + C` in te drukken en te bevestigen.

Naast de basis Jupyter notebook interface is er ook JupyterLab, een uitgebreidere en meer geïntegreerde omgeving voor Jupyter notebooks met aanvullende functies en een meer modulaire interface.



ChatGPT may produce inaccurate information about people, places, or facts. [ChatGPT September 25 Version](https://help.openai.com/en/articles/6825453-chatgpt-release-notes)

### Hoe voer je een notbook uit in Visual Studio Code?

Visual Studio Code (VS Code) heeft ondersteuning voor Jupyter notebooks via de Python-extensie. Hier is een stapsgewijze handleiding om een Jupyter notebook uit te voeren in VS Code:

1. **Installeer Visual Studio Code**:
   - Als je VS Code nog niet hebt geïnstalleerd, download en installeer het van de [officiële website](https://code.visualstudio.com/).
2. **Installeer de Python-extensie**:
   - Open VS Code.
   - Ga naar de Extensions view door te klikken op het vierkante icoon (of het icoon dat lijkt op blokken) in de zijbalk aan de linkerkant of druk op `Ctrl + Shift + X`.
   - Zoek naar "Python" en installeer de extensie die wordt aangeboden door Microsoft.
3. **Open een Jupyter notebook**:
   - Je kunt een bestaand `.ipynb` bestand openen of een nieuw bestand maken met de extensie `.ipynb`.
   - Wanneer je een `.ipynb` bestand opent in VS Code, zal het automatisch de notebook interface tonen.
4. **Celbewerking**:
   - Je kunt cellen toevoegen, bewerken en verwijderen zoals je zou doen in de traditionele Jupyter omgeving.
   - Elke cel in het notebook kan afzonderlijk worden uitgevoerd door op de groene "play" knop aan de linkerkant van de cel te klikken of door de sneltoets `Shift + Enter` te gebruiken.
5. **Kernel beheren**:
   - Rechtsboven in de notebook interface zie je de huidige kernel (bijv. Python 3). Hier kun je de kernel kiezen, stoppen, herstarten, of een nieuwe kernel toevoegen.
   - Als je voor de eerste keer een notebook uitvoert, moet je mogelijk eerst een Jupyter kernel installeren.
6. **Visualisaties en output**:
   - De output van cellen, inclusief grafieken en visualisaties, wordt direct onder de cel weergegeven, net zoals in een standaard Jupyter notebook.
7. **Opslaan en sluiten**:
   - Je kunt je notebook op elk gewenst moment opslaan met `Ctrl + S` of via het File-menu.
   - Sluit het notebook-tabblad om het notebook te sluiten.
8. **Aanvullende integraties**:
   - Een voordeel van het gebruik van Jupyter notebooks in VS Code is de diepe integratie met de rest van de editor. Dit betekent dat je toegang hebt tot functies zoals IntelliSense, de debugger, en de terminal, allemaal binnen hetzelfde venster.

Door Jupyter notebooks in VS Code te gebruiken, kun je profiteren van de krachtige bewerkings- en ontwikkelingsfuncties van de editor terwijl je interactieve analyses uitvoert.


