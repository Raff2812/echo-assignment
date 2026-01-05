# Echo assignment

Pipeline di Machine Learning per la classificazione binaria del dataset **Breast Cancer Wisconsin (Diagnostic)** https://www.kaggle.com/datasets/uciml/breast-cancer-wisconsin-data. 
Il notebook esplora diverse strategie di preprocessing (inclusi Scaling, SMOTE e PCA) e confronta vari modelli di 
classificazione (SVC, Random Forest, ecc.), analizzando le performance sia con parametri di default che ottimizzati.

## Installazione ed esecuzione

Per garantire la riproducibilità dell'ambiente e l'esecuzione corretta del codice, seguire questi passaggi:

### 1. Installazione dipendenze
Prima di avviare il notebook, assicurarsi di aver installato tutte le librerie necessarie elencate nel file `requirements.txt`.
Eseguire il seguente comando:

```bash
pip install -r requirements.txt
```

### 2. Avvio notebook
Una volta installate le dipendenze, aprire ed eseguire il notebook principale:

```bash
jupyter notebook echo_assignment.ipynb
```

### Gestione iperparametri
Il progetto include un sistema di "caching" per i risultati dell'ottimizzazione degli iperparametri, al fine di evitare 
lunghi tempi di ricalcolo ad ogni esecuzione.

Nella directory principale del progetto è presenta una cartella denominata `hyperparameters`.
Questa cartella contiene file **.json** che salvano la configurazione ottimale (best parameters) trovata tramite 
`GridSearchCV`. Durante l'esecuzione, il notebook controlla se questi file esistono per caricare istantaneamente 
i parametri migliori senza rieseguire il training della GridSearch.

#### Forzare un nuovo fine-tuning
Per ricalcolare da zero l'ottimizzazione degli iperparametri (ad esempio, dopo aver modificato la griglia di 
ricerca), è possibile utilizzare due metodi:

1. All'interno del notebook, imposta la variabile `FINETUNING_FLAG` su True.
Impostando questo flag a True, il codice ignorerà i file JSON esistenti, eseguirà nuovamente `GridSearchCV` e 
sovrascriverà i file di configurazione con i nuovi risultati.

```Python
FINETUNING_FLAG = True
```


2. Eliminare manualmente la cartella `hyperparameters`. Alla successiva esecuzione, il notebook non troverà i file 
salvati e avvierà automaticamente il processo di ottimizzazione, ricreando la cartella e i file al termine.

## Struttura del Progetto

```Plaintext
├── echo_assignment.ipynb          # notebook principale per esecuzione pipeline
├── requirements.txt               # elenco dipendenze
├── hyperparameters/               # cartella per configurazione ottimale degli iperparametri
│   ├── basic_hyperparameters.json # file per pipeline "Basic"
│   ├── pca_hyperparameters.json   # file per pipeline "SMOTE + PCA"
│   └── smote_hyperparameters.json # file per pipeline "Select + SMOTE"
└── README.md                       # documentazione progetto
```
