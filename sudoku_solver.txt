#include<iostream>
#include<bits/stdc++.h>
#include<math.h>
using namespace std;
int N=9;
int sol[9][9]={ { 3, 0, 6, 5, 0, 8, 4, 0, 0 },
                       { 5, 2, 0, 0, 0, 0, 0, 0, 0 },
                       { 0, 8, 7, 0, 0, 0, 0, 3, 1 },
                       { 0, 0, 3, 0, 1, 0, 0, 8, 0 },
                       { 9, 0, 0, 8, 6, 3, 0, 0, 5 },
                       { 0, 5, 0, 0, 9, 0, 6, 0, 0 },
                       { 1, 3, 0, 0, 0, 0, 2, 5, 0 },
                       { 0, 0, 0, 0, 0, 0, 0, 7, 4 },
                       { 0, 0, 5, 2, 0, 6, 3, 0, 0 } };
bool issafe(int i,int j,int n)
{
   for(int k=0;k<N;k++)
   {
       if(sol[k][j]==n || sol[i][k]==n)
        return false;
   }
   int s=sqrt(N);
   int rs=i-i%s;
   int cs=j-j%s;
   for(int i=0;i<s;i++)
    for(int j=0;j<s;j++)
    {
        if(sol[i+rs][j+cs]==n)
            return false;
    }

   return true;
}

bool solve()
{
    bool swapped=false;
    int i,j;
    for(i=0;i<N;i++)
    {
         for(j=0;j<N;j++)
        {
           if(sol[i][j]==0)
           {
               swapped=true;
                break;
           }

        }
        if(swapped==true)
            break;
    }


    if(i==N && j==N)
        return true;
    for(int n=1;n<=N;n++)
    {
        if(issafe(i,j,n)==true)
        {
        sol[i][j]=n;
        if(solve()==true)
            return true;
        sol[i][j]=0;
        }


    }
    return false;

}

int main()
{

cout<<(solve()?"yes":"no");
cout<<endl;
    for(int i=0;i<N;i++)
    {
       for(int j=0;j<N;j++)
            cout<<sol[i][j]<<" ";
        cout<<endl;
    }


    return 0;
}


