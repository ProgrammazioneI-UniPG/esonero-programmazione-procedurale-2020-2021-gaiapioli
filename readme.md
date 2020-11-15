nome: Gaia
Cognome: Pioli
n° matricola 330140


#include <stdio.h>  //tutti i programmi
#include <string.h> //lettura delle stringhe
#include <stdlib.h> //lettura di rend() e srend()
#include <time.h> //per utilizzare time()

int main (void){

  char M[128]; //array M
  printf("Inserisci una stringa M di massimo 128 caratteri. \nIl resto dei caratteri verrà scartato.\n" );
  fgets(M, 128, stdin);
  fflush(stdin);  //per eliminare i caratteri maggiori di 128

  int lunghezzaM;
  lunghezzaM= strlen(M)-1; //lughezza di M

  if(lunghezzaM<126)
    {
      printf("\nLa lunghezza di M è %d \n", lunghezzaM);
      printf("Come vuoi procedere? \nDigita '1' per scegliere la chiave, oppure '2' per generare la chiave in modo random. \n");
    }

  //char unodue; //indica la scelta eseguita dall'utente
  //scanf("%hhd", &unodue);
  int unodue;
  scanf("%d", &unodue);


  char k[128];  //array della chiave k

  int chiave; //una chiave: caso 1 o 2
  while ((chiave= getchar()) !='\n' && chiave!=EOF); //input
  putchar(chiave);  //output
   {
     switch (unodue) //collegato con la scelta effettuata dall'utente
      {
        case 1: //caso 1
            printf("Inserire una stringa k da cifrare con M, che sia di lunghezza maggiore o uguale a M.\n");
            fgets(k, 128, stdin); //memorizza k

            int lunghezzak;
            lunghezzak= strlen(k)-1;  //lunghezza di k
            printf("La lunghezza di k è %d \n", lunghezzak);
            while (lunghezzak < lunghezzaM)
              {
                printf("Reinserire una stringa k da cifrare con M, che sia di lunghezza maggiore o uguale a M.\n");
                fgets(k, 128, stdin); //memorizza il nuovo k
                lunghezzak= strlen(k)-1;  //lunghezza di k
                printf("La lunghezza di k è %d \n", lunghezzak);
              }   //fine while

            {
              char testocifrato[128]; //testo cifrato
              int a;  //variabile per cifrare il testo
              printf("Il messaggio cifrato è: ");
              for(a=0; a<=lunghezzaM; a++)
                {
                  testocifrato[a]=M[a] ^ k[a];
                  printf("%d", testocifrato[a]);
                }

              char testoriginale[128];  //testo originale
              for(a=0; a<=lunghezzaM; a++)
                {
                  testoriginale[a]=testocifrato[a] ^ k[a];
                }
              printf("\nIl messaggio originale è: %s \n", testoriginale);
            }
        break;  //per uscire dallo switch case 1

        case 2: //caso 2
            printf("Il programma ha generato una chiave in modo random.\n");
            time_t random; //inizio random
            srand((unsigned) time(&random));  //genera il random

            printf("La chiave scelta in modo random è %s", k);
            for(int i=0; i<lunghezzaM; i++)
              {
                printf("%c", 32+ rand() %96);  //stampa random --> 97+rand() %25
              }
            printf("\n");

            {
              char testocifrato[128]; //testo cifrato
              int a;  //variabile per cifrare il testo
              for(a=0; a<=lunghezzaM; a++)
                {
                  testocifrato[a]=M[a] ^ k[a];
                }

              printf("Il messaggio cifrato è: ");
              for(a=0; a<=lunghezzaM; a++)
                {
                  testocifrato[a]=M[a] ^ k[a];
                  printf("%d", testocifrato[a]);
                }

              char testoriginale[128];  //testo originale
              for(a=0; a<=lunghezzaM; a++)
                {
                  testoriginale[a]=testocifrato[a] ^ k[a];
                }
              printf("\nIl messaggio originale è: %s \n", testoriginale);
            }
            break;  //per uscire dallo switch case 2

            default:  //tutti gli altri caratteri
              printf("E' un carattere non accettato dal programma.\nRiavvia il programma.\n");
            break;
              } //fine switch
          } // fine while
    return 0;
}
