# Valutazione Danni Post-Sisma tramite Segmentazione Semantica UAV

Questo repository contiene il codice sorgente sviluppato a supporto della tesi magistrale relativa alla classificazione dei danni strutturali post-evento sismico. Il progetto sfrutta reti neurali convoluzionali per la segmentazione semantica di immagini zenitali acquisite da Aeromobili a Pilotaggio Remoto (APR/UAV).

L'obiettivo algoritmico è superare i limiti delle metriche di valutazione globali, implementando un indice di severità del danno basato sui criteri normativi ufficiali italiani (scheda AeDES e scala macrosismica EMS-98).

## Struttura del Repository

Il flusso di lavoro è suddiviso in tre *notebook* principali, ottimizzati per l'esecuzione su ambiente Google Colab:

*   **1. RescueNet_TRAINING_DA_ZERO_res713.ipynb**
    [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/GiacomoSilvello/UAV-damage-assessment/blob/main/RescueNet_TRAINING_DA_ZERO_res713.ipynb)
    Gestisce la fase di addestramento iniziale del modello. Opera al regime di alta risoluzione (713x713 pixel), vincolo imprescindibile nel *disaster management* per catturare le eterogeneità strutturali necessarie e superare il *trade-off* computazionale valutato rispetto a varianti più leggere.

*   **2. RescueNet_TRAINING_INCREMENTALE_res713.ipynb**
    [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/GiacomoSilvello/UAV-damage-assessment/blob/main/RescueNet_TRAINING_INCREMENTALE_res713.ipynb)
    Script dedicato alla fase di addestramento incrementale e al progressivo raffinamento dei pesi della rete, utile a minimizzare l'errore sui confini semantici e stabilizzare la curva di apprendimento.

*   **3. Analisi_Modello_Segmentazione.ipynb**
    [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/GiacomoSilvello/UAV-damage-assessment/blob/main/Analisi_Modello_Segmentazione.ipynb)
    Contiene l'intera *pipeline* di inferenza e valutazione quantitativa. Include l'analisi del *class imbalance* (es. l'estrema polarizzazione tra classi maggioritarie come "Albero" e micro-oggetti come "Veicolo"), l'estrazione delle doppie matrici di confusione (normalizzate per riga per la *Recall* e per colonna per la *Precision*), il calcolo del grado AeDES assegnato a ciascuna immagine, l'interfaccia completa di analisi e classificazione dell'immagine scattata e infine una validazione della pipeline sul campo.

## Metodologia e Calcolo del Danno

A differenza degli approcci standard basati sull'accuratezza globale a livello di immagine, questo progetto deduce la severità dell'evento calcolando l'incidenza percentuale delle classi di danno rispetto all'area totale degli edifici. 
La classificazione dei pixel predetti viene pesata proporzionalmente (da 0 per nessun danno fino a 3 per la distruzione totale), rispecchiando la perdita di capacità portante e lo sforzo di messa in sicurezza delineati dai parametri AeDES.

## Dipendenze e Dataset Originale

I dati di partenza e l'infrastruttura di base richiamata in questi script appartengono al progetto **RescueNet**. Il codice clona automaticamente il loro repository ufficiale per importare l'architettura dei dati. Si prega di fare riferimento alla loro documentazione ufficiale per le licenze, i crediti e i vincoli di utilizzo relativi al dataset di immagini originale.

## Dichiarazione sull'utilizzo dell'Intelligenza Artificiale (AI Act)

Nel rispetto dei principi di trasparenza promossi dall'AI Act europeo e dalle vigenti direttive di integrità accademica, si dichiara che alcune porzioni del codice sorgente sono state sviluppate con il supporto di sistemi di Intelligenza Artificiale generativa (Google Gemini). Tutti gli output prodotti sono stati sottoposti a una sistematica e rigorosa revisione umana, validati tecnicamente e rielaborati personalmente per aderire ai requisiti del dominio ingegneristico. L'autore assume la totale responsabilità intellettuale, logica e funzionale dell'intero progetto, garantendo la correttezza metodologica dei risultati presentati.

## Licenza

Il codice sorgente e i *notebook* presenti in questo repository sono rilasciati sotto [MIT License](LICENSE).
