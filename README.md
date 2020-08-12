#include <stdio.h>
#include <stdlib.h>
#include <string.h>
void double dabble(int n, const unsigned int *arr, char **result)
{
int nbits=16*n;
int nscratch=nbits/3;
char *scratch=calloc(1+ nscratch, sizeof *scratch);
int i, j, k;
int smin=nscratch-2;
for (i=0; i<n; ++i)
{
for (j=0; j<16; ++j) 
{
int shifted_in= (arr[i] &(1<<(15-j)))?1:0;
for (k=smin; k < nscratch; ++k)
scratch[k] +=(scratch[k] >=5)? 3:0;
if (scratch[smin]>=8)
smin -=1;
for (k=smin; k< nscratch-1; ++k)
{
scratch[k]<<=1;
scratch[k]&=0xF;

scratch[k] |= shifted_in;
}
scratch[nscratch-1]<<=1;
scratch[nscratch-1]&=0xF;

scratch[nscratch-1] |= shifted_in;
}
}
for (k=0; k< nscratch-1; ++k)
if(scratch[k]!=0)break;
nscratch-= k;
memmove(scratch, scratch+k, nscratch+1);
for (k=0; k< nscratch; ++k)
scrtch[k]+= ‘0’;
*result = realloc(scratch, nscratch+1);
return;
}
int main(void)
{
unsigned int arr[]={333,65784,1};
char *text = NULL;
int i;
for(i=0; i <3; ++i)
{
double dabble(i+1, arr, &text);
printf(“%s\n”, text);
free(text);
}
return 0;
}




