   ///*** FCFS implementation when Arrival Time of each process is same.***///
#include<stdio.h>

 // prototype of function that print  all results.
void printResult(int np, int burstTime[],int waitingTime[], int turnAroundTime[],
                  int completionTime[],float avg_wt, float avg_tat);
                 
     // Main function
int main()
{
	printf("\t\t\tFCFS when arrival time is same for every process.\n\n ");
	
	//taking number of processes form user.
	int np;
	printf("Enter number of processes you want : ");
	scanf("%d",&np);
	
	// taking burst time of each process.
	printf("\n\tGive Burst time of each process :\n");
	int i , burstTime[25];
	for(i = 0; i < np; i++)
	{
	  printf("Burst time of process %d = ",i+1);
        scanf("%d",&burstTime[i]);	
	}
	 
	 // calculation of waiting time of each process.
	int waitingTime[25];
	 waitingTime [0] = 0; //1st process doesn't wait as there is no prev process.
	 for(i = 1;i< np; i++)
	{
	    waitingTime[i] = burstTime[i-1]+ waitingTime[i-1];	
	}
	
      // calculation of average waiting time;	
	   int total_wt = 0;
      for(i =0;i< np; i++)
	  {
	  	total_wt = total_wt + waitingTime[i];
	  }
	       
	  float avg_wt = (float)total_wt / (float)np;

	// calculation of turn around time of each process.
	int turnAroundTime[25];
	 
	 for(i =0;i< np; i++)
	{
	    turnAroundTime[i] = burstTime[i]+ waitingTime[i];	
	}
	
	// calculation of average Turn around time;	
	   int total_tat = 0;
      for(i =0;i < np; i++)
	  {
	  	total_tat = total_tat + turnAroundTime[i];
	  }
	       
	  float avg_tat = (float)total_tat / (float)np;
	
	// calculation of Completion time of each process.
    int completionTime[25], l = 0;
       completionTime[0] = burstTime[0]; // as ct[prev] = 0 for 1st process
    for(i = 1; i < np; i++)
	{
		l = l + completionTime[i-1];
	   completionTime[i] = l  + burstTime[i];
	   
    }
  
     // paramter passing to printResult and calling to print all above results.
    printResult(np, burstTime, waitingTime, turnAroundTime,
	             completionTime, avg_wt, avg_tat);
	return 0;
}

// printResult function definition:
void printResult(int np, int burstTime[],int waitingTime[],int turnAroundTime[],
                  int completionTime[],float avg_wt, float avg_tat)
 {
 	 
	 
	 // for output of all calculations
 	printf("\nProcess No.\tBurst Time\tWaiting Time\tTurn Around Time\t"
	        "Completion Time");
	        
   for(int i =1; i <=np; i++)
   {
   	printf("\n%d\t\t%d\t\t%d\t\t\t%d\t\t%d", i,burstTime[i-1],waitingTime[i-1],
   	         turnAroundTime[i-1], completionTime[i-1]);
   }
   
   // printing  Average waiting and Turn around time
   printf("\n Average waiting time = %f", avg_wt);
   printf("\n Average Turn Around Time = %f", avg_tat);
 
 }

