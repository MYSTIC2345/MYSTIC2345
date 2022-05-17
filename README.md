- 👋 Hi, I’m @MYSTIC2345
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
MYSTIC2345/MYSTIC2345 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
/**********************************************************************************************************************************************************************************************

Name - Vishwas Jajpura
Roll number - 21AE10041
Section - 1
PDS LAB Assignment 6

************************************************************************************************************************************************************************************************/



#include <stdio.h>
#include<stdlib.h>
#include<string.h>
int table1[1000];
char names[1000] = "RamAliEmaAmyAlfAcyLeoMaxJayDexLeeReyIra";
void generatedata(int n){
    int p;
    for(int i=0;i<n;i++){
        p= 22*i;
        //generating ID number
        table1[p] = 0;
        if(i>10){
            table1[p+1] = 1;
            table1[p+2] = i%10;
        }else{
            table1[p+1] = 0;
            table1[p+2] = i+1;
        }
        //generating Account number
        for(int j=p+3;j<p+19;j++){
            table1[j] = rand()%10;
            if(table1[j]<0){
                table1[j] = -1*table1[j];
            }
        }
        //generating balance
        for(int j=p+19;j<p+22;j++){
            table1[j] = rand()%10;
            if(table1[j]<0){
                table1[j] = -1*table1[j];
            }
        }
    }

}
void printdata(int n){
    int o,u,k;
    //printing table1
    printf("Table1:\n");
    for(int i=0;i<n;i++){
        o = i*22;
        printf("ID = %d%d%d  Card Number= ",table1[o],table1[o+1],table1[o+2]);
        //printing card number
        for(int j=o+3;j<o+19;j++){
            printf("%d",table1[j]);
        }
        printf("  Balance = %d%d%d\n",table1[o+19],table1[o+20],table1[o+21]);
    }
    //printing table2
    printf("\nTable2:\n");
    for(int i=0;i<n;i++){
        u = i*22;
        k = i*3;
        printf("ID = %d%d%d  Name:",table1[u],table1[u+1],table1[u+2]);
        for(int j=k;j<k+3;j++){
            printf("%c",names[j]);
        }
        printf("\n");
    }
}
//search function
void search(int n){
    int in,id1,id2,id3,l,m,t1,t2,t3;
    char name[30];
    char nam1[30],nams1[30];
    printf("Enter 1 to search by ID and 2 to search by name\nEnter your choice:");
    scanf("%d",&in);
    if(in==1){
        printf("Please enter an ID(last digit):");
        scanf("%d",&id3);
        printf("Id = 00%d  Name:",id3);
        for(int i=0;i<n;i++){
            l= i*22;
            if(id3 ==table1[l+2]){

                for(int y=3*i;y<3*i+3;y++){
                    printf("%c",names[y]);
                }
                printf("  Card Number:");
                for(int j=l+3;j<l+19;j++){
                    printf("%d",table1[j]);
                }
                printf("  Balance = %d%d%d\n",table1[l+19],table1[l+20],table1[l+21]);
                break;
            }
        }
    }else if(in==2){
        printf("\nPlease enter a Name:");
        scanf("%s",name);
        for(int i=0;i<n;i++){
            l= i*22;
            m = i*3;
            nams1[0] = names[m];
            nams1[1] = names[m+1];
            nams1[2] = names[m+2];
            t1 = strcmp(nams1,name);
            if(t1==0){
                printf("Id = %d%d%d  Name:",table1[l],table1[l+1],table1[l+2]);
                for(int y=3*i;y<3*i+3;y++){
                    printf("%c",names[y]);
                }
                printf("  Card Number:");
                for(int j=l+3;j<l+19;j++){
                    printf("%d",table1[j]);
                }
                printf("  Balance = %d%d%d\n",table1[l+19],table1[l+20],table1[l+21]);
                break;
            }
        }
    }
}
void updateamt(int n){
    int i1,am1,am2,am3,l,m,k;
    char namr[30],name2[30];
    printf("\nPlease enter your name: ");
    scanf("%s",namr);
    for(int i=0;i<n;i++){
            l= i*22;
            m = i*3;
            name2[0] = names[m];
            name2[1] = names[m+1];
            name2[2] = names[m+2];
            k = strcmp(name2,namr);
            if(k==0){
                printf("\nPlease enter new Limit(with space between digits):");
                scanf("%d %d %d",&am1,&am2,&am3);
                table1[l+19] = am1;
                table1[l+20] = am2;
                table1[l+21] = am3;
                printf("\n");
                break;
            }

    }
    printf("\nAmount Successfully Updated!\n");
    printf("\n");
}
void usecard(int n){
    int arr[40],arr1[40],flag=0,a,amt1,amt2,amt3,iniamt=0,newamt=0,finalamt=0,arr2[30],r=2,l;
    char str[40];
    for(int i=0;i<40;i++){
        arr[i]=0;
    }
    printf("Enter card number:");
    scanf("%s",str);
    for(int i=0;i<16;i++){
        arr[i] = str[i] - '0';
        }

    for(int j=0;j<16;j++){
        printf("%d",arr[j]);
    }
    for(int i=0;i<n;i++){
        l= i*22+3;
        if(table1[l]==arr[0] && table1[l+1]==arr[1] && table1[l+2]==arr[2]){
            a=i+1;
            flag=1;
            break;
        }
    }
    if(flag==1){
        a = (a-1)*22+19;
        iniamt = 100*(table1[a]%10) + 10*(table1[a+1]%10) + table1[a+2]%10;
        printf("\nAvailable Balance is Rs.%d",iniamt);
        printf("\nEnter the amount for widthdraw: ");
        scanf("%d",&newamt);
        finalamt = iniamt - newamt;
        if(finalamt<0){
            printf("\nInSufficient Balance.");
        }else{
        //updating amount
            if(finalamt<10){
                table1[a] = 0;
                table1[a+1] = 0;
                table1[a+2] = finalamt;

            }else if(finalamt<100){
                table1[a] = 0;
                table1[a+1] = (finalamt - (finalamt%10))/10;
                table1[a+2] = finalamt%10;
            }else{
                while(finalamt>0 && r>=0){
                    table1[a+r]= finalamt%10;
                    finalamt = finalamt/10;
                    r = r-1;
                }
            }
        }
        printf("\nTransaction Successful!\n");
    }else{
        printf("\nInvalid Card Number\n");
    }
}

int main() {
    int n,input;
    printf("Please enter n= ");
    scanf("%d",&n);
    generatedata(n);
    printdata(n);
    do{
        printf("\n\nEnter 1 to Search\nEnter 2 to Update\nEnter 3 to Use card\nEnter 4 to exit\n\nPlease enter your choice:");
        scanf("%d",&input);
        if(input==1){
            search(n);
        }else if(input==2){
            updateamt(n);
        }else if(input==3){
            usecard(n);
        }
    }while(input != 4);
    return 0;
