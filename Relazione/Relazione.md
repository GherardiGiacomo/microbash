Gherardi Giacomo S4235299, Insinna Luca S4804022

# Relazione Microbash

## Considerazioni generali

L'implementazione di questa shell è stata particolarmente complicata. Inizialmente abbiamo incontrato delle difficoltà per quanto concerne l'utilizzo delle funzioni free e per la gestione dell'input/output redirection. In particolare, siamo rimasti "bloccati" durante i testing per il comando "ls -l | grep foo > bar" _(comando che: elenca i file e le directory nella directory corrente, quindi filtra solo le righe che contengono la parola "foo" e salva l'output filtrato nel file chiamato "bar")_ fornito come esempio nel testo del laboratorio.
Dopo numerosi tentativi e grazie all'aiuto del professor. Lagorio, abbiamo capito che l'errore riscontrato _(errore nella dup2)_ era causato da una cattiva gestione dell'apertura e chiusura dei file descriptor.

#
#
## Test effettuati

### Comandi funzionanti 

<b> ls | wc -l </b>
- <b> Scopo </b>: Conta del numero di file e directory presenti nella directory corrente
- <b> Situazione iniziale </b>: Directory corrente con n file
- <b> Linea inviata alla microbash</b>: ls | wc -l 
- <b> Risultato atteso </b>: Numero file presenti nella directory

<b> ls | sort | uniq </b>
- <b> Scopo </b>: Elenco ordinato e unico dei file e delle directory presenti nella directory corrente
- <b> Situazione iniziale </b>: Directory corrente con n file
- <b> Linea inviata alla microbash </b>: ls | sort | uniq
- <b> Risultato atteso </b>: Elenco ordinato e senza duplicati dei file e delle directory presenti nella directory corrente

<b> echo "PROVA CIAO PROVA" | wc -w </b>
- <b> Scopo </b>: Conta il numero di parole nella stringa "PROVA CIAO PROVA"
- <b> Situazione iniziale </b>: - 
- <b> Linea inviata alla microbash</b>: echo "PROVA CIAO PROVA" | wc -w 
- <b> Risultato atteso </b>: 3

<b>  ls | grep ".pdf" | wc -l </b>
- <b> Scopo </b>: Conta il numero di file con formato .pdf presenti nella directory corrente 
- <b> Situazione iniziale </b>: Directory corrente 
- <b> Linea inviata alla microbash</b>: ls | grep ".pdf" | wc -l
- <b> Risultato atteso </b>: Numero dei file .pdf

#

### Comandi che restituiscono errori

<b> ls directory_non_esistente </b>
- <b> Scopo </b>: Testare il comportamento quando si prova a visualizzare il contenuto di una directory inesistente.
- <b> Situazione iniziale </b>: Una qualsiasi directory
- <b> Linea inviata alla microbash </b>: ls directory_non_esistente
- <b> Risultato atteso </b>: ls: impossibile accedere a 'directory_non_esistente': File o directory non esistente


<b> cat file_non_esistente | grep pattern </b>

- <b> Scopo </b>: Verificare la gestione di un file inesistente all'interno di una pipeline.
- <b> Situazione iniziale </b>: Directory corrente con alcuni file e directory.
- <b> Linea inviata alla microbash: </b> cat file_non_esistente | grep pattern
- <b> Risultato atteso </b>: _Messaggio di errore_ "cat: file_non_esistente: File o directory non esistente"


<b> ls | grep | wc -l </b>
- <b> Scopo </b>: Testare il comportamento quando manca il pattern di ricerca per il comando grep in una pipeline.
- <b> Situazione iniziale </b>: Directory corrente con alcuni file e directory.
- <b> Linea inviata alla microbash: </b>: ls | grep | wc -l
- <b> Risultato atteso: </b> Uso: grep [OPZIONE]... MODELLI [FILE]...
Usare "grep --help" per ulteriori informazioni.
0

<b> cat file_non_esistente | grep pattern | wc -l </b>
- <b> Scopo </b>: Testare la gestione di un file inesistente all'interno di una pipeline
- <b> Situazione iniziale </b>: Directory corrente con alcuni file e directory.
- <b> Linea inviata alla microbash </b>: cat file_non_esistente | grep pattern | wc -l
- <b> Risultato atteso </b>: cat: non_existent_file: File o directory non esistente
0