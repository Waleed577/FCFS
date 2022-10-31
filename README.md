// C++ program for implementation of FCFS  
// scheduling 

//First Come First Serve (FCFS) is an operating system scheduling algorithm that 
//automatically executes queued requests and processes in order of their arrival. 
//This is managed with a FIFO queue.

//As the process enters the ready queue, its PCB (Process Control Block) is 
//linked with the tail of the queue and, when the CPU becomes free, it should be
//assigned to the process at the beginning of the queue.


#inlcude<conio.h>
#include<iostream> 
using namespace std; 
  
// Function to find the waiting time for all  
void findWaitingTime(int processes[], int n,  
                          int bt[], int wt[]) 
{ 
    // waiting time for first process is 0 
    wt[0] = 0; 
  
    // calculating waiting time 
    for (int  i = 1; i < n ; i++ ) 
        wt[i] =  bt[i-1] + wt[i-1] ; 
} 
  
// Function to calculate turn around time 
void findTurnAroundTime( int processes[], int n,  
                  int bt[], int wt[], int tat[]) 
{ 
    // calculating turnaround time by adding 
    // bt[i] + wt[i] 
    for (int  i = 0; i < n ; i++) 
        tat[i] = bt[i] + wt[i]; 
} 
  
//Function to calculate average time 
void findavgTime( int processes[], int n, int bt[]) 
{ 
    int wt[n], tat[n], total_wt = 0, total_tat = 0; 
  
    //Function to find waiting time of all processes 
    findWaitingTime(processes, n, bt, wt); 
  
    //Function to find turn around time for all processes 
    findTurnAroundTime(processes, n, bt, wt, tat); 
  
    //Display processes along with all details 
    cout << "Processes  "<< " Burst time  "
         << " Waiting time  " << " Turn around time\n"; 
  
    // Calculate total waiting time and total turn  
    // around time 
    for (int  i=0; i<n; i++) 
    { 
        total_wt = total_wt + wt[i]; 
        total_tat = total_tat + tat[i]; 
        cout << "   " << i+1 << "\t\t" << bt[i] <<"\t    "
            << wt[i] <<"\t\t  " << tat[i] <<endl; 
    } 
  
    cout << "Average waiting time = " 
         << (float)total_wt / (float)n; 
    cout << "\nAverage turn around time = " 
         << (float)total_tat / (float)n; 
} 
  
// Driver code 
int main() 
{ 
    //process id's in form of array
    int processes[] = { 1, 2, 3, 4, 5}; 
    int n = sizeof processes / sizeof processes[0]; 
  
    //Burst time of all processes 
    int  burst_time[] = {10, 5, 8, 4, 123}; 
  
    findavgTime(processes, n,  burst_time); 
    return 0; 
} 
