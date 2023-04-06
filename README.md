#include <stdio.h>

#include <stdlib.h>


void swap(int id[], int at[], int bt[], int n) {
  int ind, min, k, f, i, j, m;

  for (i = 0; i < n; i++) {
    m = at[i];
    ind = i;
    for (int j = i + 1; j < n; j++) {
      if (at[j] < m) {
        ind = j;
        m = at[j];
      }

    }
    //printf("%d\t",m);
    min = at[i];
    at[i] = at[ind];
    at[ind] = min;
    min = id[i];
    id[i] = id[ind];
    id[ind] = min;
    min = bt[i];
    bt[i] = bt[ind];
    bt[ind] = min;
  }
}

void swap(int id[], int at[], int n) {
  int ind, min, k, f, i, j, m;

  for (i = 0; i < n; i++) {
    m = at[i];
    ind = i;
    for (int j = i + 1; j < n; j++) {
      if (at[j] < m) {
        ind = j;
        m = at[j];
      }

    }
    //printf("%d\t",m);
    min = at[i];
    at[i] = at[ind];
    at[ind] = min;
    min = id[i];
    id[i] = id[ind];
    id[ind] = min;
    //	min=bt[i];
    //	bt[i]=bt[ind];
    //	bt[ind]=min;
  }
}

main() {
  int n1, i;
  printf("enter the number of process you want to entered");
  scanf("%d", & n1);
  int id1[n1], at1[n1], bt1[n1], c[n1];

  for (i = 0; i < n1; i++) {
    printf("enter the process id  \n");
    scanf("%d", & id1[i]);
    printf("enter the arrival time of process %d\n", id1[i]);
    scanf("%d", & at1[i]);
    printf("enter the burst time of process %d\n", id1[i]);
    scanf("%d", & bt1[i]);
  }

  swap(id1, at1, bt1, n1);

  printf("process id\tarrival time\tburst time\n");
  int e;
  for (i = 0; i < n1; i++) {
    printf("    %d    \t     %d     \t     %d\n", id1[i], at1[i], bt1[i]);
    e = e + bt1[i];
    c[i] = bt1[i];
  }

  int in = 0, va = bt1[0], te[e], w[n1];
  for (int b = 0; b < (e - 1) / 2; b++) {

    for (int q = 0; q < n1; q++) {

      if (bt1[q] == 0) {

        //printf("%d %d\n",va,in);
        continue;
      }

      if (at1[q] <= b) {

        if (bt1[q] != 0 && bt1[q] <= va) {

          in = q;
          va = bt1[q];
          printf("%d %d\n", va, in);

        } else {
          if (bt1[q] != 0 && va == 0) {
            in = q;
            va = bt1[q];
          }
        }
      }

    }
    //	printf("%d %d\n",va,in);  
    printf("\n");
    bt1[in] = bt1[in] - 2;
    //	w[in]=id1[in];
    if (bt1[in] < 0) {
      bt1[in] = 0;
    }
    te[b] = id1[in];
    va = bt1[in];

    printf("process id\tarrival time\tburst time\n");

    for (int i = 0; i < n1; i++) {
      printf("    %d    \t     %d     \t     %d\n", id1[i], at1[i], bt1[i]);
    }
  }

  for (int i = 0; i < e / 2; i++) {
    printf("%d\t", te[i]);
  }
  printf("\n");

  for (int i = 0; i < n1; i++) {
    for (int j = 0; j < e / 2; j++) {
      if (te[j] == id1[i]) {
        w[i] = (j + 1) * 2;
      }
    }
  }
  for (int i = 0; i < n1; i++) {
    printf("%d\t", w[i]);
  }

  int tt[n1], wt[n1];
  float avw = 0.0, avt = 0.0;
  for (i = 0; i < n1; i++) {
    tt[i] = w[i] - at1[i];
    wt[i] = tt[i] - c[i];
    avw = avw + wt[i];

  }
  printf("\n");

  printf("process id\tarrival time\tburst time\tturnaround\twaiting time\n");
  for (i = 0; i < n1; i++) { //to display the result of the sorting 
    printf("    %d    \t     %d     \t    %d     \t    %d    \t     %d  \n", id1[i], at1[i], c[i], tt[i], wt[i]); //the complexity of the loop is n
    avt = avt + tt[i];
  }

  printf("average waiting time is -: %f\n", avw / n1);
  printf("average turn around time is -: %f\n", avt / n1);

}
