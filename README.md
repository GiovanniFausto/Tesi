# Link Prediction using Geometric Deep Learning

Lo scopo di questa tesi è dimostrare come sia possibile fare link prediction usando quello che è il deep learning di tipo geometrico.

# Link prediction

L'obiettivo principale alla base del link prediction e prevedere l'esistenza o la non esistenza di un link all'interno della network.

Per questo scopo è stato scelto di usare modelli basati sul Geometric Deep Learning, che riescono ad ottenere migliori risultati quando si usano su dati non euclidei come i grafi.

# Il problema

Il problema principale è quello di prevedere, dati due nodi qualsiasi di una rete, l’esistenza di un collegamento tra di essi. Questo problema può essere risolto usando tecniche e approcci diversi in base al campo di applicazione e al risultato che si vuole ottenere.

# Obiettivo

L’obiettivo è presentare un modello di deep-learning geometrico che faccia queste predizioni. 

Per questo motivo sono stati testati diversi modelli su svariate reti di diverse dimensioni e caratteristiche. 

Per raggiungere i risultati migliori sono stati variati di volta in volta i parametri dei modelli per renderli più performanti.
Per misurare le prestazioni sono state considerate l’accuratezza e l’AUC.

# Geometric deep learning

La maggioranza del deep learning viene effettuate su dati euclidei, come ad esempio immagini o testi, questi sono dati a una o due dimensioni.

Tutto ciò che possiamo osservare lo osserviamo in tre dimensioni e quindi i nostri dati dovrebbero riflettere questa caratteristica, ma è difficile rappresentarli in modo euclideo. 

Le reti sono un esempio di dati non euclidei, e sono quelle maggiormente usate nel campo del link prediction, quindi è stato usato il Geometric Deep Learning per far fronte alla limitazioni del deep learning tradizionale.

Più precisamente, dato che si parla di grafi, sono state usate una categoria particolare delle Graph Neural Network, che sono le Graph Attention Network.

# Graph Attention Network

Le GAT operano su dati strutturati a grafo, sfruttando i livelli di self-attention.

In particolare, vengono sovrapposti dei layer in cui i nodi sono in grado di contribuire alle feature dei nodi vicini. 

L’idea è calcolare le rappresentazioni nascoste di ogni nodo del grafo prestando, quindi, attenzione al suo vicinato.

GAT accetta come input le feature di tutti i nodi della rete e per prima cosa applica una trasformazione lineare, in base alla matrice dei pesi, per calcolare il coefficiente di attenzione tra i nodi.
A questo punto aggrega le feature dei nodi come una combinazione dei loro vicini, al quale è applicata una funzione sigmoid. 

Infine, impiega l’attenzione multi-head per stabilizzare il processo di apprendimento dei coefficienti di attenzione e le feature di output dei nodi adiacente sono concatenate o mediate per ottenere le feature finali di output.

# Il modello

Il cuore del modello sono appunto i livelli GAT.

Le GAT sono i livelli iniziali del modello, a questi è stata applicata una funzione di attivazione ELU tra ogni livello.

Con l’output dei livelli GAT è stato calcolato il prodotto di Hadamard su dei nodi di interesse, che erano stati scelti precedentemente in modo casuale per formare i dataset di train, validazione e test. 

Successivamente il risultato ottenuto viene fatto passare attraverso un fully connected layer composto da livelli lineari che hanno una funzione di attivazione RELU.

Per finire dato che si vuole calcolare una probabilità viene usata una sigmoid. 

# Esperimenti 

Gli esperimenti sono stati condotti su due reti: Cora e Citeseer. 

Queste reti sono diverse per quanto riguarda numero di nodi, numero di feature per ogni nodo e per numero di edge. 

Sono stati testati circa 100 modelli, ogni modello aveva un numero diverso di livelli GAT, di livelli lineari e di head tra i livelli GAT. 

Più precisamente, i livelli GAT sono stati fatti variare da un minimo di un livello a un massimo di quattro livelli, mentre i livelli lineari da uno a tre. Le head scelte sono state una e quattro. 

È stato fatto un train di 100 epoche su tutti i modelli per avere risultati consistenti. Per quanto riguarda la loss è stata considerata la Binary Cross Entropy.

# Risultati 

I risultati ottenuti sono paragonabili, e a volte superiori, ai modelli già esistenti.

Più precisamente, abbiamo ottenuto un valore di AUC pari a 0.90 Cora e 0.91 per quello di Citeseer.

Per Cora, si nota un trend per i modelli che hanno tra due e tre livelli GAT.

Mentre per Citeseer l’AUC è sempre elevata e solo in un caso scende drasticamente.

I  modelli migliori per i due dataset sono diversi. Infatti per Cora il modello migliore ha 4 livelli GAT, mentre per Citeseer è quello con 2 livelli GAT. In questo ultimo caso, con la metà dei livelli si riescono ad ottenere ottimi risultati. Probabilmente, questo è dovuto anche al fatto che Citeseer ha molti più nodi e molte più feature di Cora. 


![alt text](https://github.com/GiovanniFausto/Tesi/blob/master/plot/Cora/totali/gat/coraBestAucVariazioneGAT.png)


![alt text](https://github.com/GiovanniFausto/Tesi/blob/master/plot/Citeseer/totali/gat/citeseerBestAucVariazioneGAT.png)

# Conclusioni 
Con questa tesi abbiamo analizzato il problema del link prediction tramite l’uso del Geometric Deep Learning, analizzando e risolvendo i problemi principali legati a questo tema, ed esplorando le metodologie usate fino ad ora in letteratura, usando modelli basati sull’architettura GAT.

È stato dimostrato come si possono ottenere ottimi risultati in questo ambito tramite l’uso delle GAT selezionando i giusti parametri del modello.

Essendo un campo molto recente ed in continua evoluzione, si possono fare molti altri studi prendendo in considerazione modelli e reti diverse, ma anche approcci diversi come quelli basati unicamente sulla topologia della rete e che quindi non tengono conto delle feature dei nodi.



