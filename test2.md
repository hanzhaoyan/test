#include<stdio.h>
int main()
{
  int a[5],b[5][5];
  int i,j,sum,max,m,n;
  printf("shuru5gezhengshu\n");
  for(i=0;i<5;i++)
    scanf("%d",&a[i]);
  for(i=0;i<5;i++)
  {
    sum=0;
    for(j=i;j<5;j++)
    {
      sum+=a[j];
      b[i][j]=sum;
    }
  }
  max=b[0][0];
  for(i=0;i<5;i++)
    for(j=i;j<5;j++)
    {
      if(b[i][j]>max)
      {
        max=b[i][j];
        m=i+1;
        n=j+1;
      }
    }
  }
  printf("max:%d  %d %d \n",max,m,n); 
  return 0;
}
