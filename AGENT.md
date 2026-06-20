# AGENT.md - Istruzioni per gli Agenti AI

Benvenuto! Questa repository è un ambiente di studio dedicato ai **Fondamenti del Machine Learning** (in lingua italiana).
Ogni agente AI che lavora su questa repository deve seguire le linee guida descritte in questo documento.

---

## 🎯 Obiettivo della Repository
Lo scopo principale del progetto è fornire materiale didattico chiaro, completo ed intuitivo per studenti che affrontano i concetti di base del Machine Learning:
- Preprocessing dei dati (scaling, encoding, train/test split).
- Regressione Lineare ed Overfitting.
- Tecniche di Regolarizzazione (Ridge, Lasso) e Learning Curves.
- Classificazione e Clustering.

---

## 📚 Linee Guida Pedagogiche (Per gli Agenti)
Quando ti viene chiesto di scrivere spiegazioni, commenti o documentazione per i notebook:
1. **Pensa come un Docente**: Spiega i concetti in modo chiaro, accessibile e strutturato per uno studente. Non limitarti a descrivere *cosa* fa il codice, spiega sempre il **perché**.
2. **Utilizza la Notazione Matematica (LaTeX)**: Rappresenta le formule matematiche e le loss function usando la sintassi LaTeX standard (es. per Ridge: $\text{Loss} = \text{MSE} + \alpha \sum w_j^2$) per assicurarne una visualizzazione ottimale in Jupyter/Google Colab.
3. **Fornisci Esempi Concreti e Contrasti**: Evidenzia il contrasto tra i modelli (es. OLS vs Ridge vs Lasso) analizzando le metriche reali ottenute sui dati.
4. **Prevenzione degli Errori Didattici**:
   - Spiega chiaramente l'importanza del seed (`RANDOM_SEED`) per la riproducibilità.
   - Metti in guardia lo studente sul **Data Leakage** (es. fittare lo scaler solo sul training set).

---

## 🛠️ Ambiente di Sviluppo e Comandi
- **Interprete Python**: Utilizza sempre l'interprete dell'ambiente virtuale locale: `file:///home/rares/project/python/professionAI/machine-learning-fondamenti/.venv/bin/python3`.
- **Dipendenze**: Definite nel file `requirements.txt`.
- **Note per Windows**: Se operi su sistemi Windows, usa `npx.cmd` al posto di `npx`.

---

## ⚡ Skill e Strumenti del Progetto
La repository dispone di una skill locale per automatizzare l'arricchimento didattico:

- **Skill di Arricchimento Didattico**: [.agents/notebook-pedagogical-enrichment/SKILL.md](file:///.agents/notebook-pedagogical-enrichment/SKILL.md)
- **Helper Script**: [.agents/notebook-pedagogical-enrichment/scripts/notebook_helper.py](file:///.agents/notebook-pedagogical-enrichment/scripts/notebook_helper.py)
  - Usa `inspect` per vedere la struttura e le celle del notebook:
    ```bash
    python3 .agents/notebook-pedagogical-enrichment/scripts/notebook_helper.py inspect <path_to_notebook.ipynb>
    ```
  - Usa `clear-outputs` per ripulire l'esecuzione del notebook prima di salvarlo o farne il commit:
    ```bash
    python3 .agents/notebook-pedagogical-enrichment/scripts/notebook_helper.py clear-outputs <path_to_notebook.ipynb>
    ```
