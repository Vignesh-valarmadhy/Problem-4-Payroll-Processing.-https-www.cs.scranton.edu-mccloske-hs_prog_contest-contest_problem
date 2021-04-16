# Problem-4-Payroll-Processing.-https-www.cs.scranton.edu-mccloske-hs_prog_contest-contest_problem

#include <stdio.h>
#include <string.h>

typedef struct employee
{
    char Name[100];
    float hwage;
    float minutes;
    float hour;
    float pay;
    
}employee;





employee input1()
{
    employee e;
    
    printf("Enter Name & Hourly Wage: ");
    scanf("%s %f",e.Name, &e.hwage);
    e.minutes=0;
    return e;
}

void inputnemp(employee emp[],int n)
{
    for(int i=0;i<n;i++)
    {
        printf("\n\nEnter the Details of Employee %d :\n",i+1);
        emp[i]=input1();
    }
}


void timecardprocessing(employee emp[],int n,int m)
{
    for(int i=0;i<m;i++)
    {
        char ename[100];
        float min; 
        printf("\n\nEnter the Employee Name and Minutes for Employee: %d :\n",i+1);
        scanf("%s %f",ename, &min);
        
        for(int j=0;j<n;j++)
        {
            
            if(strcmp(ename, emp[j].Name)==0)
            {
                emp[j].minutes += min;
                break;
            }
        }
        
    }
    for(int i=0;i<n;i++)
        {
            emp[i].hour= emp[i].minutes/60;
        }
    
    
}


float calc1(employee e)
{
    float p=0;
    
    if(e.hour>40)
    {
        p = 40*e.hwage;
        p += (e.hour-40)*1.5*e.hwage;
        
    }
    else
    {
        p = e.hour*e.hwage;
    }
    return (p);
}


void calcn(employee emp[],int n)
{
    for(int i=0;i<n;i++)
    {   
        emp[i].pay= calc1(emp[i]);
    }
}


void print(employee e)
{
    if(e.hour==0)
    {
        return;
    }
    printf("%s  %0.2f hours, $%0.2f\n",e.Name,e.hour,e.pay);
}





void printn(employee emp[],int n)
{
    for(int i=0;i<n;i++)
    {
        print(emp[i]);
    }
}


int main()
{
    int n;
    printf("Enter Total Employee : ");
    scanf("%d",&n);
    
    employee emp[n];
    
    inputnemp(emp,n);
    
    printf("\n\nEnter Number of time Cards: ");
    int m;
    scanf("%d",&m);
    
    
    
    timecardprocessing(emp,n,m);
    
    calcn(emp,n);
    
    printn(emp,n);
    
    return 0;
    
}
