# os-project
# include<stdio.h>
#include<string.h>

struct process_Struct {
    char process_name[20];
    int arrival_time, burst_time, completion_time, remaining, turn_around_time, waiting_time;
}temp_Struct;


void calculate(int no_of_process) {

    int count, quantum_time;
    struct process_Struct faculty_Process[no_of_process];

    puts("\n\t\t\t*********************");
    puts("\t\t\t***   ASSUME ARRIVAL TIME OF ALL QUERIES IS 'O'   ***");
    puts("\t\t\t*********************\n");  

    for(count = 0; count < no_of_process; count++) {
         
        printf("Enter the details of Process[%d]", count+1);
        puts("");        
        printf("\nProcess Name : ");
        scanf("%s", faculty_Process[count].process_name);

        faculty_Process[count].arrival_time = 0;

        printf("\nBurst Time : ");
        scanf("%d", &faculty_Process[count].burst_time);
        puts("");
    }
    printf("Now, enter the quantum time : ");
    scanf("%d", &quantum_time);

    
    // initialy all the burst time is remaining and completion of process is zero.
    for(count = 0; count < no_of_process; count++) {
        faculty_Process[count].remaining = faculty_Process[count].burst_time;
        faculty_Process[count].completion_time = 0;
    }

    int total_time =0;
    
    while(1) {

        int done =1;
        for(count = 0; count < no_of_process; count++){
        
            if(faculty_Process[count].remaining > 0)
            {
                done =0;
    
                if(faculty_Process[count].remaining > quantum_time){
                    total_time += quantum_time;
                    faculty_Process[count].remaining -= quantum_time;
                    
                }
                else {
                    total_time += faculty_Process[count].remaining;
                    faculty_Process[count].completion_time= total_time;
                    faculty_Process[count].turn_around_time= total_time - faculty_Process[count].arrival_time;
                    faculty_Process[count].waiting_time= faculty_Process[count].turn_around_time  - faculty_Process[count].burst_time;
                    faculty_Process[count].remaining = 0;
                }
            }
    }
    if(done == 1)
            break;

    }
    

    puts("\n\t\t\t****************");
    puts("\t\t\t***   ROUND ROBIN ALGORITHM OUTPUT   ***");
    puts("\t\t\t****************\n");
    printf("\n|\tProcess Name\t|\tArrival Time\t|\tBurst Time\t|\tCompletion Time\t|\tTotal Time\t|\n");

    int sum=0;
    for(count = 0; count < no_of_process; count++){
        //waiting_time = faculty_Process[count].completion_time - faculty_Process[count].burst_time - faculty_Process[count].arrival_time;
        sum+= faculty_Process[count].turn_around_time;
        printf("\n|\t%s\t\t|\t%d\t\t|\t%d\t\t|\t%d\t\t|\t%d\t\t|\n", faculty_Process[count].process_name, faculty_Process[count].arrival_time, faculty_Process[count].burst_time, faculty_Process[count].completion_time, faculty_Process[count].turn_around_time);
    }
    printf("\nAverage Query Time : %.4f\n\n",(float)sum/no_of_process);
}

void faculty_Queue(int no_of_process) {

    calculate(no_of_process);
}


void student_Queue(int no_of_process) {

    calculate(no_of_process);

}


int main(int argc, char const *argv[]) {
    int select_queue, no_of_process;

    puts("Please choose a queue to post your query : ");
    puts("1. FACULTY queue.");
    puts("2. STUDENT queue.");
    printf("> ");
    scanf("%d", &select_queue);

    switch(select_queue) {
        case 1 :
                printf("Enter number of process for FACULTY queue : ");
                scanf("%d", &no_of_process);
                
                faculty_Queue(no_of_process);
                
                break;

        case 2 :
                printf("Enter number of process for STUDENT queue : ");
                scanf("%d", &no_of_process);

                student_Queue(no_of_process);
                
                break;

        default : 
                printf("Please selet the correct option by running the program again.");
    }

    return 0;
}
