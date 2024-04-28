# sys
// Write a program to use fork system call to create 5 child processes and assign 5 operations
// to childs.

#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/wait.h>
#include<string.h>


int main()
{
    for(int i=1;i<=5;i++)
    {
        int pid = fork();
        if(pid == 0)
        {
            if(i == 1)
            {
                printf("Child %d: %d + %d = %d\n",i,10,20,10+20);
            }
            else if(i == 2)
            {
                printf("Child %d: %d - %d = %d\n",i,30,20,30-20);
            }
            else if(i == 3)
            {
                printf("Child %d: %d * %d = %d\n",i,10,20,10*20);
            }
            else if(i == 4)
            {
                printf("Child %d: %d / %d = %d\n",i,20,10,20/10);
            }
            else if(i == 5)
            {
                printf("Child %d: %d %% %d = %d\n",i,20,10,20%10);
            }
            exit(0);
        }
    }
}

// Write a program to use vfork system call(login name by child and password by parent)


#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<fcntl.h>

int main(int argc, char *argv[]) {
    
    int pid=vfork();
    if(pid==0) {
         printf("Enter Your Name");
        char name[100];
        scanf("%s",name);
    }
    else
    {
        wait(NULL);

        printf("Enter Your Password");
        char name[100];
        scanf("%s",name);
        exit(0);

    }



}

// Write a program to open any application using fork sysem call.

#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<math.h>
#include<time.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<fcntl.h>


int main(int argc,char *argv[])
{
    int pid=fork();
    if(pid==0)
    {
        printf("I am the child process\n");
        // execlp("Visual Studio Code","Visual Studio Code",NULL);
        // execlp("gedit","gedit",NULL);
        // execlp("firefox", "firefox", NULL);
        execlp("google-chrome","google-chrome",NULL);
        exit(0);

    }
}

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main() {
    int pid = vfork();
    if (pid == 0) {
        // Child process
        execlp("gedit", "gedit", NULL);
        // If execlp fails, print an error message
        perror("execlp");
        // Terminate child process
        _exit(EXIT_FAILURE);
    } else if (pid > 0) {
        // Parent process
        // Wait for the child process to finish
        int status;
        waitpid(pid, &status, 0);
        printf("Child process finished\n");
    } else {
        // vfork() failed
        perror("vfork");
        exit(EXIT_FAILURE);
    }

    return 0;
}

// Write a program to demonstrate the wait use with fork sysem call.

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main() {
    pid_t pid = fork();
    if (pid == -1) {
        // Error occurred
        perror("fork");
        exit(0);
    } else if (pid == 0) {
        // Child process
        printf("Child process started\n");
        // Simulate some work in the child process
        for (int i = 0; i < 5; i++) {
            printf("Child: %d\n", i);
            sleep(1);
        }
        printf("Child process finished\n");
        exit(1);
    } else {
        // Parent process
        printf("Parent process waiting for child\n");
        
        wait(NULL); // Wait for child to finish
        printf("Parent process: Child finished with status ");
    }
    return 0;
}
modified:
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main() {
    pid_t pid = fork();
    if (pid == -1) {
        // Error occurred
        perror("fork");
        exit(0);
    } else if (pid == 0) {
        // Child process
        printf("Child process started\n");
        // Simulate some work in the child process
        for (int i = 0; i < 5; i++) {
            printf("Child: %d\n", i);
            sleep(1);
        }
        printf("Child process finished\n");
        exit(1);
    } else {
        // Parent process
        printf("Parent process waiting for child\n");
        
        wait(NULL); // Wait for child to finish
        printf("Parent process: Child finished with status ");
    }
    return 0;
}

// Write a program to demonstrate the variations exec system call.

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    char *const args[] = {"ls", "-l", NULL};
    char *const env[] = {"PATH=/bin:/usr/bin", NULL};

    // execl: Pass each argument separately
    printf("Using execl\n");
    execl("/bin/ls", "ls", "-l", NULL);

    // execv: Pass arguments as an array
    printf("Using execv\n");
    execv("/bin/ls", args);

    // execle: Pass environment variables as argument
    printf("Using execle\n");
    execle("/bin/ls", "ls", "-l", NULL, env);

    // execve: Pass both arguments and environment variables
    printf("Using execve\n");
    execve("/bin/ls", args, env);

    // execlp: Search for executable in PATH environment variable
    printf("Using execlp\n");
    execlp("ls", "ls", "-l", NULL);

    // execvp: Search for executable in PATH and pass arguments as an array
    printf("Using execvp\n");
    execvp("ls", args);

    // If any of the exec calls above fail, print an error message
    perror("exec");
    
    return 0;
}

// Write a program to demonstrate the exit system call use with wait & fork sysem call.

#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/wait.h>

int main()
{
    int pid=fork();
    if(pid==0)
    {
        printf("child process\n");
        for(int i=0;i<10;i++)
        {
            printf("%d\n",i);
            sleep(1);
        }
        exit(0);
    }
    else
    {
        printf("parent process\n");
        wait(NULL);
        
        printf("child process terminated\n");
    }
}



assignment 08 two codes open in two terminals
// Write a program to demonstrate the kill system call to send signals between unrelated
// processes(fork).

#include <iostream>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <signal.h>

// Signal handler function
void signal_handler(int signum) {
    std::cout << "Received signal " << signum << std::endl;
}

int main() {
    int pid = fork();

    if (pid == -1) {
        // Fork failed
        perror("fork");
        exit(EXIT_FAILURE);
    } else if (pid == 0) {
        // Child process
        std::cout << "Child process running" << std::endl;

        // Register signal handler for SIGUSR1
        signal(SIGUSR1, signal_handler);

        std::cout << "Child process waiting for signal" << std::endl;
        // Child process waits indefinitely
        while (1) {
            sleep(1);
        }
    } else {
        // Parent process
        std::cout << "Parent process running" << std::endl;

        // Wait for a moment to ensure child is ready
        sleep(1);

        // Send SIGUSR1 signal to the child process
        std::cout << "Sending SIGUSR1 signal to child process" << std::endl;
        if (kill(pid, SIGUSR1) == -1) {
            perror("kill");
            exit(EXIT_FAILURE);
        }

        // Wait for the child process to finish
        wait(NULL);
    }

    return 0;
}
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>

// Signal handler function
void signal_handler(int signum) {
    printf("Received signal %d\n", signum);
}

int main() {
    // Register the signal handler
    signal(SIGINT, signal_handler);

    printf("Waiting for signals...\n");

    // Loop infinitely
    while(1) {
        sleep(1); // Sleep to avoid busy-waiting
    }

    return 0;
}

modified from internet:
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <signal.h>
#include <sys/types.h>

void signal_handler(int signum) {
    if (signum == SIGUSR1) {
        printf("Signal SIGUSR1 received\n");
    } else if (signum == SIGUSR2) {
        printf("Signal SIGUSR2 received\n");
    }
}

int main() {
    pid_t childPid;

    // Register signal handlers
    signal(SIGUSR1, signal_handler);
    signal(SIGUSR2, signal_handler);

    // Create a child process
    childPid = fork();

    if (childPid == -1) {
        perror("fork failed");
        return 1;
    } else if (childPid == 0) { // Child process
        printf("Child process (PID: %d) is running\n", getpid());
        // Sleep for a while to ensure parent process sets up signal handlers
        sleep(1);
        // Send SIGUSR1 signal to the parent process
        kill(getppid(), SIGUSR1);
        // Sleep for a while before exiting
        sleep(1);
        printf("Child process exiting\n");
    } else { // Parent process
        printf("Parent process (PID: %d) is running\n", getpid());
        // Sleep for a while to ensure child process sends the signal
        sleep(1);
        // Send SIGUSR2 signal to the child process
        kill(childPid, SIGUSR2);
        // Wait for child process to exit
        wait(NULL);
        printf("Parent process exiting\n");
    }

    return 0;
}
// Write a program to demonstrate the kill system call to send signals between related
// processes(fork).

#include <iostream>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <signal.h>

// Signal handler function
void signal_handler(int signum) {
    std::cout << "Received signal " << signum << std::endl;
}

int main() {
    int pid = fork();

    if (pid == -1) {
        // Fork failed
        perror("fork");
        exit(EXIT_FAILURE);
    } else if (pid == 0) {
        // Child process
        std::cout << "Child process running" << std::endl;

        // Register signal handler for SIGUSR1
        signal(SIGUSR1, signal_handler);

        std::cout << "Child process waiting for signal" << std::endl;
        // Child process waits indefinitely
        while (1) {
            sleep(1);
        }
    } else {
        // Parent process
        std::cout << "Parent process running" << std::endl;

        // Wait for a moment to ensure child is ready
        sleep(1);

        // Send SIGUSR1 signal to the child process
        std::cout << "Sending SIGUSR1 signal to child process" << std::endl;
        if (kill(pid, SIGUSR1) == -1) {
            perror("kill");
            exit(EXIT_FAILURE);
        }

        // Wait for the child process to finish
        wait(NULL);
    }

    return 0;
}
modified:
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>
// Signal handler functions
void sighup_handler(int signum);
void sigint_handler(int signum);
void sigquit_handler(int signum);
int main() {
pid_t pid;
// Fork a child process
if ((pid = fork()) < 0) {
perror("fork");
exit(1);
}
if (pid == 0) {
// Child process
// Register signal handlers for SIGHUP, SIGINT, and SIGQUIT
signal(SIGHUP, sighup_handler);
signal(SIGINT, sigint_handler);
signal(SIGQUIT, sigquit_handler);
printf("Child process running with PID: %d\n", getpid());
for (;;)
; // infinite loop
} else {
// Parent process
printf("Parent process running with PID: %d\n", getpid());
printf("Sending SIGHUP to child...\n");
// Send SIGHUP signal to child process
kill(pid, SIGHUP);
sleep(3);
printf("Sending SIGINT to child...\n");
// Send SIGINT signal to child process
kill(pid, SIGINT);
sleep(3);
printf("Sending SIGQUIT to child...\n");
// Send SIGQUIT signal to child process
kill(pid, SIGQUIT);
sleep(3);
}
return 0;
}
// Signal handler function for SIGHUP
void sighup_handler(int signum) {
printf("Child: Received SIGHUP\n");
}
// Signal handler function for SIGINT
void sigint_handler(int signum) {
printf("Child: Received SIGINT\n");
}
// Signal handler function for SIGQUIT
void sigquit_handler(int signum) {
printf("Child: Received SIGQUIT\n");
exit(0);
}
// Write a program to use alarm and signal sytem call(check i/p from user within time)

#include<bits/stdc++.h>
using namespace std;

void signalHandler(int signum)
{
    cout << "data is not inputted" << endl;
    exit(0);

}

int main()
{
    signal(SIGALRM,signalHandler);
    alarm(5);
    cout<<"Enter command within 5 second"<<endl;
    string command;
    cin>>command;
    cout<<"data insrted"<<command<<endl;
    exit(0);
    return 0;

}

Write a program for alarm clock using alarm and signal system call
#include<bits/stdc++.h>
using namespace std;

void alarmHandler(int signum)
{
    cout<<"Alarm Occured please wake up"<<endl;
    exit(0);
}
int main(int argc,int *argv)
{
    signal(SIGALRM,alarmHandler);
    int second;

    cout<<"Setup time in seconds so that "<<endl;

    cin>>second;

    alarm(second);

    cout<<"Alarm set"<<endl;

    while(1);

    return 0;
    

}


// Write a program to give statistics of a given file using stat system call. (few imp field like
// FAP, file type)


#include<bits/stdc++.h>
using namespace std;
#include <sys/types.h>
#include <sys/stat.h>
#include <unistd.h>
#include <cstring>


int main()
{
    struct stat file_stat;

    if(stat("file.txt",&file_stat)==-1)
    {
        cout<<"File not found"<<endl;
        return 0;
    }

// st_ino: This field represents the inode number of the file. Inodes are data structures used by filesystems to represent files and directories. Each file or directory on a Unix-like filesystem is identified by a unique inode number.
// st_mode: This field represents the file mode and permissions. It contains information about the type of the file (e.g., regular file, directory, symbolic link) and the access permissions (e.g., read, write, execute) for the owner, group, and others.
// st_nlink: This field represents the number of hard links to the file. Hard links are additional directory entries that point to the same inode. The link count indicates how many hard links exist for the file. When a file is created, its link count is set to 1. Each time a hard link is created to the file, the link count is incremented by 1. When a hard link is removed, the link count is decremented by 1. When the link count reaches 0, the file is deleted.
// st_uid: This field represents the user ID of the owner of the file.
// st_gid: This field represents the group ID of the group that owns the file.
// st_rdev: This field represents the device ID for special files. For regular files, it is set to 0. For character and block special files, it contains the device numbers of the associated device. This field is used for device files like /dev/tty, /dev/null, etc.
    cout<<file_stat.st_ino<<endl;
    cout<<file_stat.st_mode<<endl;
    cout<<file_stat.st_nlink<<endl;
    cout<<file_stat.st_uid<<endl;
    cout<<file_stat.st_gid<<endl;
    cout<<file_stat.st_rdev<<endl;




}


// Write a program to give statistics of a given file using fstat system call. (few imp field like
// FAP, file type)

#include<bits/stdc++.h>
#include<sys/types.h>
#include<unistd.h>
#include<sys/stat.h>
#include<fcntl.h>

using namespace std;


int main(int argc,int *argv)
{
    struct stat st;
    int fd=open("file.txt",O_RDONLY);
    if(fstat(fd,&st)==-1)
    {
        cout<<"Error in fstat"<<endl;
        return -1;
    }
    cout<<"file inode number"<<st.st_ino<<endl;
    cout<<"Size of the file is : "<<st.st_size<<endl;
    cout<<"File type is : "<<st.st_mode<<endl;
    return 0;
}

assignment 14 of chattin by java is not present


asignment15
// Write a program to create 3 threads, first thread printing even no, second thread printing odd no.
// and third thread printing prime no.

import java.io.*;

class odd extends Thread {

    public void run()
    {
        for(int i=1;i<=10;i++)
        {
            if(i%2!=0)
            {
                System.out.println("Odd: "+i);
            }
        }
    }
}

class even extends Thread
{
    public void run()
    {
        for(int i=1;i<=10;i++)
        {
            if(i%2==0)
            {
                System.out.println("Even: "+i);
            }
        }
    }

}

class prime extends Thread
{
    public void run()
    {
        for(int i=1;i<=10;i++)
        {
            int count=0;
            for(int j=1;j<=i;j++)
            {
                if(i%j==0)
                {
                    count++;
                }
            }
            if(count==2)
            {
                System.out.println("Prime: "+i);
            }
        }
    }
}
public class assignment15
{
    public static void main(String [] args)
    {
        odd o=new odd();
        even e=new even();
        prime p=new prime();
        o.start();
        e.start();
        p.start();
    }
}


#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>

#define NUM_THREADS 2
#define NUM_INCREMENTS 1000000

// Shared global counter
int counter = 0;

// Mutex for synchronizing access to the counter
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;

// Function for the threads to execute
void *thread_function(void *arg) {
    int i;
    for (i = 0; i < NUM_INCREMENTS; i++) {
        // Lock the mutex before accessing the shared counter
        pthread_mutex_lock(&mutex);
        
        // Increment the counter
        counter++;
        
        // Unlock the mutex after accessing the shared counter
        pthread_mutex_unlock(&mutex);
    }
    pthread_exit(NULL);
}

int main() {
    pthread_t threads[NUM_THREADS];
    int i, status;

    // Create thread s
    for (i = 0; i < NUM_THREADS; i++) {
        status = pthread_create(&threads[i], NULL, thread_function, NULL);
        if (status != 0) {
            fprintf(stderr, "Error creating thread %d. Exiting...\n", i);
            exit(EXIT_FAILURE);
        }
    }

    // Join threads
    for (i = 0; i < NUM_THREADS; i++) {
        status = pthread_join(threads[i], NULL);
        if (status != 0) {
            fprintf(stderr, "Error joining thread %d. Exiting...\n", i);
            exit(EXIT_FAILURE);
        }
    }

    // Print the final value of the counter
    printf("Final counter value: %d\n", counter);

    return 0;
}


// producer consumer problem in java

import java.util.LinkedList;

class ProducerConsumer {
    private LinkedList<Integer> buffer = new LinkedList<>();
    private int capacity;

    public ProducerConsumer(int capacity) {
        this.capacity = capacity;
    }

    public void produce() throws InterruptedException {
        int value = 0;
        while (true) {
            synchronized (this) {
                while (buffer.size() == capacity) {
                    wait();
                }

                System.out.println("Producer produced: " + value);
                buffer.add(value++);
                notify();

                Thread.sleep(1000);
            }
        }
    }

    public void consume() throws InterruptedException {
        while (true) {
            synchronized (this) {
                while (buffer.isEmpty()) {
                    wait();
                }

                int value = buffer.removeFirst();
                System.out.println("Consumer consumed: " + value);
                notify();

                Thread.sleep(1000);
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        ProducerConsumer pc = new ProducerConsumer(5);

        Thread producerThread = new Thread(() -> {
            try {
                pc.produce();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        Thread consumerThread = new Thread(() -> {
            try {
                pc.consume();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        producerThread.start();
        consumerThread.start();
    }
}

calculator code


#!/bin/bash

echo "enter your number a"
read a

echo "enter your number b"
read b

echo "choose 1 for addition"
echo "choose 2 for subtraction"
echo "choose 3 for multiplication"
echo "enter your choice"
read choice

if [[ $choice == '1' ]]; then 
    answer=$((a + b))
    echo "Result: $answer"
elif [[ $choice == '2' ]]; then
    answer=$((a - b))
    echo "Result: $answer"
elif [[ $choice == '3' ]]; then
    answer=$((a * b))
    echo "Result: $answer"
else
    echo "Invalid choice"
fi

digital 

# Write a program to implement digital clock using shell script.
#!/bin/bash

while true; 
do
    clear
    echo "$(date +"%T")"
    sleep 1
done



# Write a program to check whether system is in network or not using ’ping’ command using shell
# script.
#!/bin/bash

# Define the IP address or domain name to ping
target="www.google.com"

# Ping the target
ping -c 1 $target 

# Check the exit status of the ping command
if [ $? == 0 ]; then
    echo "System is connected to the network."
else
    echo "System is not connected to the network."
fi




# Write a program to sort 10 the given 10 numbers in ascending order using shell.

#!/bin/bash

echo "Sorting 10 numbers using shell..."

myarr=(10 9 8 7 6 5 4 3 2 1)

for ((i = 0; i < 10; i++)); do
    min_index=$i
    for ((j = i + 1; j < 10; j++)); do
        if [[ ${myarr[j]} -lt ${myarr[min_index]} ]]; then
            min_index=$j
        fi
    done
    if [[ $min_index -ne $i ]]; then
        temp=${myarr[i]}
        myarr[i]=${myarr[min_index]}
        myarr[min_index]=$temp
    fi
done

echo "Sorted numbers in ascending order:"
for ((i = 0; i < 10; i++)); do
    echo "${myarr[i]}"
done

# Write a program to print “Hello World” message in bold, blink effect, and in different colors like
# red, blue etc.

#!/bin/bash

# ANSI escape codes for formatting
BOLD='\033[1m'
BLINK='\033[5m'
RED='\033[31m'
BLUE='\033[34m'
RESET='\033[0m'

# Print "Hello World" in bold, blink effect, and in different colors

while true; do
    echo -e "${BOLD}${BLINK}${RED}Hello World${RESET}"
    sleep 1
    echo -e "${BOLD}${BLINK}${BLUE}Hello World${RESET}"
    sleep 1
done

# . Write a shell script to find whether given file exist or not in folder or on drive.

#!/bin/bash




echo "Enter the file name"
read fileName

echo "Enter the directory name"
read dirName

if [[ -e "${dirName}/${fileName}" ]]
then
    echo "File exist"
else
    echo "File does not exist"
fi


# Write a shell script to show the disk partitions and their size and disk usage i.e free space.

#!/bin/bash

# Display disk partitions and their sizes
echo "Disk partitions and their sizes:"
df -h

# Display disk usage (free space)
echo "Disk usage (free space):"
du -h /


# Write a shell script to find the given file in the system using find or locate command.

#!/bin/bash

# Main program
echo "Enter the name of the file to search:"
read file_to_search

echo "Searching for '$file_to_search' using find command:"
find / -name "$file_to_search" 2>/dev/null




# Write a shell script to download a webpage from given URL . (Using wget command).


#!/bin/bash

# Main program
echo "Enter the URL of the webpage to download:"
read url

echo "Downloading webpage from '$url'..."

# Download the webpage using wget command
wget "$url" -O webpage.html

echo "Webpage downloaded successfully!"




# Write a shell script to display the users on the system . (Using finger or who command).


#!/bin/bash

# Display the users on the system using the who command
echo "Users currently logged in to the system:"
who


assignment 29
# Write a python recursive function for prime number input limit in as parameter to
# it.

def is_prime(n,divisor=2):
    if n <= 2:
        return n == 2
    if n % divisor == 0:
        return False
    if divisor * divisor > n:
        return True
    return is_prime(n, divisor + 1)


def generate(limit,start=2):
    if(start<=limit):
        if(is_prime(start)):
            print(start)
        generate(limit,start+1)
    

limit=int(input("Enter Limut"))
generate(limit)

assignment 30:
. Write a program to display the following pyramid. The number of lines in the
pyramid should not be hard-coded. It should be obtained from the user. The
pyramid should appear as close to the center of the screen as possible.
(Hint: Basics n loops)

#include <iostream>
#include <iomanip>

using namespace std;

int main() {
    int numLines;
    
    cout << "Enter the number of lines in the pyramid: ";
    cin >> numLines;
    
    // Display the pyramid
    for(int i = 1; i <= numLines; ++i) {
        // Print leading spaces
        cout << setw(numLines - i + 1);
        
        // Print left half of the pyramid
        for(int j = 1; j <= i; ++j) {
            cout << j << " ";
        }
        
        // Print right half of the pyramid
        for(int j = i - 1; j >= 1; --j) {
            cout << j << " ";
        }
        
        cout << endl;
    }
    
    return 0;
}


take any txt file and count word frequencies in a file.(hint : file handling + basics )

#include <iostream>
#include <fstream>
#include <map>
#include <string>
#include <sstream>
#include <cctype>

using namespace std;

// Function to remove punctuation from a word
string removePunctuation(const string& word) {
    string result = "";
    for(char c : word) {
        if(isalpha(c)) {
            result += tolower(c);
        }
    }
    return result;
}

int main() {
    // Open the text file
    ifstream inputFile("input.txt");
    if (!inputFile) {
        cerr << "Error opening file." << endl;
        return 1;
    }
    
    // Map to store word frequencies
    map<string, int> wordFrequency;
    string line;
    
    // Read the file line by line
    while(getline(inputFile, line)) {
        // Tokenize the line
        istringstream iss(line);
        string word;
        while(iss >> word) {
            // Remove punctuation and convert to lowercase
            word = removePunctuation(word);
            
            // Increment the word frequency count
            if(!word.empty()) {
                wordFrequency[word]++;
            }
        }
    }
    
    // Close the file
    inputFile.close();
    
    // Print the word frequencies
    cout << "Word frequencies:" << endl;
    for(const auto& pair : wordFrequency) {
        cout << pair.first << ": " << pair.second << endl;
    }
    
    return 0;
}

31. Take any txt file and count word frequencies in a file.(hint : file handling + basics )
# Open the file and read its contents into a string
with open("text_file.txt", "r") as file:
    text = file.read()

# Remove any punctuation from the text
punctuations = '''!()-[]{};:'"\,<>./?@#$%^&*_~'''
for char in text:
    if char in punctuations:
        text = text.replace(char, "")

# Split the text into a list of words
words = text.split()

# Create a dictionary to store the word frequencies
word_freq = {}

# Count the frequency of each word
for word in words:
    if word.lower() in word_freq:
        word_freq[word.lower()] += 1
    else:
        word_freq[word.lower()] = 1

# Print the word frequencies
for word in sorted(word_freq):
    print(word, word_freq[word])

Gedit command_frequnecy.py
python command_frequency.py



32. Generate a frequency list of all the commands you have used, and show the top 5 commands along with their count. (Hint: history command hist will give you a list of all commands used.)

import os
from collections import Counter

def get_bash_history_commands():
    history_file = os.path.expanduser("~/.bash_history")
    with open(history_file, "r", encoding="utf-8") as file:
        commands = file.readlines()
    return [command.strip() for command in commands if command.strip()]

commands = get_bash_history_commands()
command_freq = Counter(commands)

print("Top 5 commands:")
for command, count in command_freq.most_common(5):
    print(f"{count}: {command}")

gedit command_frequency.py
python3 command_frequency.py



33. Write a shell script that will take a filename as input and check if it is executable. 2. Modify the script in the previous question, to remove the execute permissions, if the file is executable.

To accomplish this objective, we can write a shell script that takes a filename as input and checks if it is executable. If the file is executable, the script will remove its execute permissions. Here's the shell script:

#!/bin/bash

# Function to check if a file is executable and remove execute permissions if it is
check_and_remove_execute_permissions() {
    filename="$1"
    
    # Check if the file is executable
    if [ -x "$filename" ]; then
        echo "$filename is executable."
        # Remove execute permissions
        chmod -x "$filename"
        echo "Execute permissions removed from $filename."
    else
        echo "$filename is not executable."
    fi
}

# Main script
# Check if filename is provided as argument
if [ $# -ne 1 ]; then
    echo "Usage: $0 <filename>"
    exit 1
fi

# Get the filename from command-line argument
filename="$1"

# Call the function to check and remove execute permissions
check_and_remove_execute_permissions "$filename"

gedit check_permissions.sh
chmod +x check_permissions.sh
./check_permissions.sh filename(filename give exec file to check permission)

34. Generate a word frequency list for wonderland.txt. Hint: use grep, tr, sort, uniq (or anything else that you want)

Just take wonderland.txt and directly run this

grep -oE '\b\w+\b' wonderland.txt | tr '[:upper:]' '[:lower:]' | sort | uniq -c

Use this command where wonderland.txt is novel so it will give word frequency list for wonderland.txt

35. Write a bash script that takes 2 or more arguments, i)All arguments are filenames ii)If fewer than two arguments are given, print an error message iii)If the files do not exist, print error message iv)Otherwise concatenate files 

#!/bin/bash

# Function to concatenate files
concatenate_files() {
    # Concatenate all files into a new file named "output.txt"
    cat "$@" > output.txt
    echo "Files concatenated successfully. Result saved in output.txt"
}

# Main script
# Check if at least two filenames are provided as arguments
if [ $# -lt 2 ]; then
    echo "Error: At least two filenames are required."
    exit 1
fi

# Check if all provided filenames exist
for filename in "$@"; do
    if [ ! -e "$filename" ]; then
        echo "Error: File '$filename' does not exist."
        exit 1
    fi
done

# Call the function to concatenate files
concatenate_files "$@"


Save filename concat_files.sh
Create any file1.txt file2.txt 
chmod +x concat_files.sh
./concat_files.sh file1.txt file2.txt file3.txt ...





36. Write a python function for merge/quick sort for integer list as parameter to it.
merge

def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    
    # Split the array into two halves
    mid = len(arr) // 2
    left_half = arr[:mid]
    right_half = arr[mid:]
    
    # Recursively sort each half
    left_half = merge_sort(left_half)
    right_half = merge_sort(right_half)
    
    # Merge the sorted halves
    return merge(left_half, right_half)

def merge(left, right):
    merged = []
    left_index = right_index = 0
    
    # Merge the two halves into a single sorted array
    while left_index < len(left) and right_index < len(right):
        if left[left_index] < right[right_index]:
            merged.append(left[left_index])
            left_index += 1
        else:
            merged.append(right[right_index])
            right_index += 1
    
    # Add remaining elements from left or right half
    merged.extend(left[left_index:])
    merged.extend(right[right_index:])
    
    return merged

# Input from the user
n = int(input("Enter the number of integers: "))
input_str = input(f"Enter {n} space-separated integers: ")
arr = [int(x) for x in input_str.split()]

# Check if the number of integers provided is equal to n
if len(arr) != n:
    print(f"Error: Expected {n} integers.")
else:
    # Sort the array using merge sort
    sorted_arr = merge_sort(arr)
    print("Sorted array:", sorted_arr)

Gedit merge.py
Python3 merge.py


Quick

def quick_sort(arr):
    if len(arr) <= 1:
        return arr

    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]

    return quick_sort(left) + middle + quick_sort(right)

# Input from the user
n = int(input("Enter the number of integers: "))
input_str = input(f"Enter {n} space-separated integers: ")
arr = [int(x) for x in input_str.split()]

# Check if the number of integers provided is equal to n
if len(arr) != n:
    print(f"Error: Expected {n} integers.")
else:
    # Sort the array using quick sort
    sorted_arr = quick_sort(arr)
    print("Sorted array:", sorted_arr)
Gedit quick.py
Python3 quick.py

37. Write a shell script to download a given file from ftp://10.10.13.16 if it exists on ftp. (use lftp, get and mget commands). 

You can use the lftp command-line tool to achieve this. Below is a shell script that downloads a given file from the FTP server at ftp://10.10.13.16 if it exists:

#!/bin/bash

# Function to download a file from FTP
download_file() {
    # FTP URL and filename
    ftp_url="ftp://10.10.13.16"
    filename="$1"

    # Check if the file exists on FTP
    echo "Checking if $filename exists on FTP..."
    if lftp -e "find $filename; exit" "$ftp_url" | grep -q "$filename"; then
        # Download the file
        echo "Downloading $filename from FTP..."
        lftp -e "get $filename; exit" "$ftp_url"
        echo "Download complete."
    else
        echo "Error: $filename does not exist on FTP."
    fi
}

# Main script
# Check if filename is provided as argument
if [ $# -ne 1 ]; then
    echo "Usage: $0 <filename>"
    exit 1
fi

# Get the filename from command-line argument
filename="$1"

# Call the function to download the file from FTP
download_file "$filename”

Gedit download_from_ftp.sh
chmod +x download_from_ftp.sh
./download_from_ftp.sh filename(filename you want to download from ftp)


38. Write program to implement producer consumer problem using semaphore.h in C/JAVA

#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>
#include <unistd.h>
#include <pthread.h>
#include <semaphore.h>

pthread_t *producers;
pthread_t *consumers;
sem_t buf_mutex, empty_count, fill_count;
int *buf, buf_pos = -1, prod_count, con_count, buf_len;

int produce(pthread_t self) {
    int i = 0;
    int p = 1 + rand() % 40;
    while (!pthread_equal(*(producers + i), self) && i < prod_count) {
        i++;
    }
    printf("Producer %d produced %d \n", i + 1, p);
    return p;
}

void consume(int p, pthread_t self) {
    int i = 0;
    while (!pthread_equal(*(consumers + i), self) && i < con_count) {
        i++;
    }
    printf("Buffer:");
    for (i = 0; i <= buf_pos; ++i)
        printf("%d ", *(buf + i));
    printf("\nConsumer %d consumed %d \nCurrent buffer len: %d\n", i + 1, p, buf_pos);
}

void* producer(void *args) {
    while (1) {
        int p = produce(pthread_self());
        sem_wait(&empty_count);
        sem_wait(&buf_mutex);
        ++buf_pos; // critical section
        *(buf + buf_pos) = p;
        sem_post(&buf_mutex);
        sem_post(&fill_count);
        sleep(1 + rand() % 3);
    }
    return NULL;
}

void* consumer(void *args) {
    int c;
    while (1) {
        sem_wait(&fill_count);
        sem_wait(&buf_mutex);
        c = *(buf + buf_pos);
        consume(c, pthread_self());
        --buf_pos;
        sem_post(&buf_mutex);
        sem_post(&empty_count);
        sleep(1 + rand() % 5);
    }
    return NULL;
}

int main(void) {
    int i, err;
    srand(time(NULL));
    sem_init(&buf_mutex, 0, 1);
    sem_init(&fill_count, 0, 0);
    printf("Enter the number of Producers:");
    scanf("%d", &prod_count);
    producers = (pthread_t*) malloc(prod_count * sizeof(pthread_t));
    printf("Enter the number of Consumers:");
    scanf("%d", &con_count);
    consumers = (pthread_t*) malloc(con_count * sizeof(pthread_t));
    printf("Enter buffer capacity:");
    scanf("%d", &buf_len);
    buf = (int*) malloc(buf_len * sizeof(int));
    sem_init(&empty_count, 0, buf_len);
    for (i = 0; i < prod_count; i++) {
        err = pthread_create(producers + i, NULL, &producer, NULL);
        if (err != 0) {
            fprintf(stderr, "Error creating producer %d: %s\n", i + 1, strerror(err));
        } else {
            printf("Successfully created producer %d\n", i + 1);
        }
    }
    for (i = 0; i < con_count; i++) {
        err = pthread_create(consumers + i, NULL, &consumer, NULL);
        if (err != 0) {
            fprintf(stderr, "Error creating consumer %d: %s\n", i + 1, strerror(err));
        } else {
            printf("Successfully created consumer %d\n", i + 1);
        }
    }
    for (i = 0; i < prod_count; i++) {
        pthread_join(*(producers + i), NULL);
    }
    for (i = 0; i < con_count; i++) {
        pthread_join(*(consumers + i), NULL);
    }
    return 0;
}
gedit producer_consumer.c
gcc -pthread producer_consumer.c -o producer_consumer
./producer_consumer


39. Write a program to implement reader-writers problem using semaphore.  

The reader-writers problem involves multiple readers and writers accessing a shared resource (e.g., a file, database, etc.). Readers can access the resource simultaneously, while writers must have exclusive access to the resource. We can use semaphores to solve this problem by ensuring that writers have exclusive access while allowing multiple readers to access the resource concurrently.

Here's a basic implementation of the reader-writers problem using semaphores in C:

c
Copy code
#include <stdio.h>
#include <pthread.h>
#include <semaphore.h>

#define NUM_READERS 3
#define NUM_WRITERS 2

sem_t mutex, write_block;
int data = 0, reader_count = 0;

void *reader(void *arg) {
    int reader_id = *(int *)arg;
    while (1) {
        sem_wait(&mutex);
        reader_count++;
        if (reader_count == 1) {
            sem_wait(&write_block);
        }
        sem_post(&mutex);

        printf("Reader %d read data: %d\n", reader_id, data);

        sem_wait(&mutex);
        reader_count--;
        if (reader_count == 0) {
            sem_post(&write_block);
        }
        sem_post(&mutex);
    }
    pthread_exit(NULL);
}

void *writer(void *arg) {
    int writer_id = *(int *)arg;
    while (1) {
        sem_wait(&write_block);
        data++;
        printf("Writer %d wrote data: %d\n", writer_id, data);
        sem_post(&write_block);
    }
    pthread_exit(NULL);
}

int main() {
    pthread_t readers[NUM_READERS], writers[NUM_WRITERS];
    int reader_ids[NUM_READERS], writer_ids[NUM_WRITERS];
    int i;

    // Initialize semaphores
    sem_init(&mutex, 0, 1);
    sem_init(&write_block, 0, 1);

    // Create reader threads
    for (i = 0; i < NUM_READERS; i++) {
        reader_ids[i] = i + 1;
        pthread_create(&readers[i], NULL, reader, &reader_ids[i]);
    }

    // Create writer threads
    for (i = 0; i < NUM_WRITERS; i++) {
        writer_ids[i] = i + 1;
        pthread_create(&writers[i], NULL, writer, &writer_ids[i]);
    }

    // Join reader threads
    for (i = 0; i < NUM_READERS; i++) {
        pthread_join(readers[i], NULL);
    }

    // Join writer threads
    for (i = 0; i < NUM_WRITERS; i++) {
        pthread_join(writers[i], NULL);
    }

    // Destroy semaphores
    sem_destroy(&mutex);
    sem_destroy(&write_block);

    return 0;
}
Gedit reader_writers.c
gcc -pthread reader_writers.c -o reader_writers
./reader_writers

modified:
#include <stdio.h>
#include <pthread.h>
#include <semaphore.h>
#include <unistd.h>

#define NUM_READERS 3
#define NUM_WRITERS 2
#define MAX_ITERATIONS 5

sem_t mutex, resource;
int readers_count = 0;

void *reader(void *arg) {
    int reader_id = *(int *)arg;
    for (int i = 0; i < MAX_ITERATIONS; i++) {
        // Entry section
        sem_wait(&mutex);
        readers_count++;
        if (readers_count == 1) {
            sem_wait(&resource);
        }
        sem_post(&mutex);

        // Critical section (reading)
        printf("Reader %d is reading (Iteration %d)\n", reader_id, i + 1);
        sleep(1); // Sleep for simulation

        // Exit section
        sem_wait(&mutex);
        readers_count--;
        if (readers_count == 0) {
            sem_post(&resource);
        }
        sem_post(&mutex);

        // Non-critical section
        sleep(1); // Sleep for simulation
    }
    pthread_exit(NULL);
}

void *writer(void *arg) {
    int writer_id = *(int *)arg;
    for (int i = 0; i < MAX_ITERATIONS; i++) {
        // Critical section (writing)
        sem_wait(&resource);
        printf("Writer %d is writing (Iteration %d)\n", writer_id, i + 1);
        sem_post(&resource);
        
        // Non-critical section
        sleep(1); // Sleep for simulation
    }
    pthread_exit(NULL);
}

int main() {
    pthread_t readers[NUM_READERS], writers[NUM_WRITERS];
    int reader_ids[NUM_READERS], writer_ids[NUM_WRITERS];

    // Initialize semaphores
    sem_init(&mutex, 0, 1);
    sem_init(&resource, 0, 1);

    // Create reader threads
    for (int i = 0; i < NUM_READERS; i++) {
        reader_ids[i] = i + 1;
        pthread_create(&readers[i], NULL, reader, &reader_ids[i]);
    }

    // Create writer threads
    for (int i = 0; i < NUM_WRITERS; i++) {
        writer_ids[i] = i + 1;
        pthread_create(&writers[i], NULL, writer, &writer_ids[i]);
    }

    // Join reader threads
    for (int i = 0; i < NUM_READERS; i++) {
        pthread_join(readers[i], NULL);
    }

    // Join writer threads
    for (int i = 0; i < NUM_WRITERS; i++) {
        pthread_join(writers[i], NULL);
    }

    // Destroy semaphores
    sem_destroy(&mutex);
    sem_destroy(&resource);

    return 0;
}


40. Write a program for chatting between two/three users to demonstrate IPC using message passing (msgget, msgsnd, msgrcv ).  

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <sys/ipc.h>
#include <sys/msg.h>

#define MAX_MESSAGE_SIZE 1024

// Define structure for message
struct message_buffer {
    long message_type;
    char message_text[MAX_MESSAGE_SIZE];
};

int main() {
    int message_queue_id;
    struct message_buffer message;

    // Create a unique key for the message queue
    key_t key = ftok("/tmp", 'a');

    // Create a message queue, or get the ID of an existing one
    message_queue_id = msgget(key, 0666 | IPC_CREAT);
    if (message_queue_id == -1) {
        perror("msgget failed");
        exit(EXIT_FAILURE);
    }

    // Fork a child process for sending messages
    pid_t child_pid = fork();
    if (child_pid == -1) {
        perror("fork failed");
        exit(EXIT_FAILURE);
    }

    // Child process (Sender)
    if (child_pid == 0) {
        while (1) {
            printf("Sender: ");
            fgets(message.message_text, MAX_MESSAGE_SIZE, stdin);
            // Set message type as 1
            message.message_type = 1;
            // Send the message
            if (msgsnd(message_queue_id, &message, sizeof(message), 0) == -1) {
                perror("msgsnd failed");
                exit(EXIT_FAILURE);
            }
        }
    }
    // Parent process (Receiver)
    else {
        while (1) {
            // Receive the message
            if (msgrcv(message_queue_id, &message, sizeof(message), 1, 0) == -1) {
                perror("msgrcv failed");
                exit(EXIT_FAILURE);
            }
            // Print the received message
            printf("Receiver: %s", message.message_text);
        }
    }

    // Remove the message queue
    if (msgctl(message_queue_id, IPC_RMID, NULL) == -1) {
        perror("msgctl failed");
        exit(EXIT_FAILURE);
    }

    return 0;
}

 gedit message_queue.c
gcc message_queue.c -o message_queue
./message_queue











assignment55

// Write a program using PIPE, to Send data from parent to child over a pipe. 

#include<stdio.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<fcntl.h>
#include<stdlib.h>
#include<string.h>



int main()
{
    int pid;
    int x,y;
    int fd[2];
    // 0 th fild descriptor used for redaing data and 1 decriptor used for writing data
    if(pipe(fd)==-1)
    {
        printf("Error in pipe\n");
        return 1;
    }
    pid=fork();

    if(pid==0)
    {
        printf("currently in child process\n");
        close(fd[0]);
        // reading data 

        printf("Entering the data for the yx\n");
        scanf("%d",&x);
        write(fd[1],&x,sizeof(int));
        close(fd[1]);
    }
    else
    {
        close(fd[1]);
        printf("reading data from the child process\n");
        read(fd[0],&y,sizeof(int));
        printf("The value of y is %d\n",y);
        close(fd[0]);
    }

}


// Write a program using FIFO, to Send data from parent to child over a pipe. (named
// pipe)


#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <string.h>

#define FIFO_PATH "my_pipe"

void parent_process() {
    int fd;
    char data[] = "Hello from parent!";

    // Create the FIFO named pipe
    mkfifo(FIFO_PATH, 0666);

    // Open the pipe for writing
    fd = open(FIFO_PATH, O_WRONLY);
    if (fd == -1) {
        perror("open");
        exit(EXIT_FAILURE);
    }

    // Send data to the child process
    printf("Parent process sending: %s\n", data);
    write(fd, data, strlen(data) + 1);

    // Close the pipe
    close(fd);

    printf("Parent process finished sending data.\n");
}

void child_process() {
    int fd;
    char buffer[256];

    // Open the pipe for reading
    fd = open(FIFO_PATH, O_RDONLY);
    if (fd == -1) {
        perror("open");
        exit(EXIT_FAILURE);
    }

    // Read data sent by the parent process
    read(fd, buffer, sizeof(buffer));
    printf("Child process received: %s\n", buffer);

    // Close the pipe
    close(fd);

    printf("Child process finished receiving data.\n");
}

int main() {
    // Create a child process
    int pid = fork();

    if (pid == -1) {
        perror("fork");
        exit(EXIT_FAILURE);
    } else if (pid == 0) {
        // Child process
        child_process();
    } else {
        // Parent process
        parent_process();
    }

    return 0;
}


#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

#define BUFFER_SIZE 1024

int main(int argc, char *argv[]) {
    if (argc != 2) {
        fprintf(stderr, "Usage: %s <filename>\n", argv[0]);
        return EXIT_FAILURE;
    }

    // Open the specified file for reading
    FILE *file = fopen(argv[1], "rb");
    if (file == NULL) {
        perror("fopen");
        return EXIT_FAILURE;
    }

    // Create a pipe
    int pipe_fd[2];
    if (pipe(pipe_fd) == -1) {
        perror("pipe");
        return EXIT_FAILURE;
    }

    // Fork a child process
    pid_t pid = fork();
    if (pid == -1) {
        perror("fork");
        return EXIT_FAILURE;
    }

    if (pid == 0) {
        // Child process
        close(pipe_fd[1]); // Close the write end of the pipe in the child

        // Redirect stdin to read from the pipe
        dup2(pipe_fd[0], STDIN_FILENO);

        // Execute a program to receive the file (e.g., cat)
        execlp("cat", "cat", NULL);
        perror("execlp");
        return EXIT_FAILURE;
    } else {
        // Parent process
        close(pipe_fd[0]); // Close the read end of the pipe in the parent

        char buffer[BUFFER_SIZE];
        size_t bytes_read;

        // Read data from the file and write it to the pipe
        while ((bytes_read = fread(buffer, 1, BUFFER_SIZE, file)) > 0) {
            write(pipe_fd[1], buffer, bytes_read);
        }

        // Close the write end of the pipe to signal EOF to the child
        close(pipe_fd[1]);

        // Wait for the child process to finish
        wait(NULL);
    }

    // Close the file
    fclose(file);
    return EXIT_SUCCESS;
}


#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>

#define FIFO_PATH "my_pipe"
#define BUFFER_SIZE 1024

void parent_process(const char *filename) {
    // Create the FIFO named pipe
    mkfifo(FIFO_PATH, 0666);

    // Open the pipe for writing
    int fd = open(FIFO_PATH, O_WRONLY);
    if (fd == -1) {
        perror("open");
        exit(EXIT_FAILURE);
    }

    // Open the file for reading
    FILE *file = fopen(filename, "rb");
    if (file == NULL) {
        perror("fopen");
        exit(EXIT_FAILURE);
    }

    // Read data from the file and write it to the pipe
    char buffer[BUFFER_SIZE];
    size_t bytes_read;
    while ((bytes_read = fread(buffer, 1, BUFFER_SIZE, file)) > 0) {
        write(fd, buffer, bytes_read);
    }

    // Close the file and the pipe
    fclose(file);
    close(fd);

    // Remove the FIFO named pipe
    unlink(FIFO_PATH);
}

void child_process() {
    // Open the pipe for reading
    int fd = open(FIFO_PATH, O_RDONLY);
    if (fd == -1) {
        perror("open");
        exit(EXIT_FAILURE);
    }

    // Read data from the pipe and write it to stdout
    char buffer[BUFFER_SIZE];
    ssize_t bytes_read;
    while ((bytes_read = read(fd, buffer, BUFFER_SIZE)) > 0) {
        write(STDOUT_FILENO, buffer, bytes_read);
    }

    // Close the pipe
    close(fd);
}

int main(int argc, char *argv[]) {
    if (argc != 2) {
        fprintf(stderr, "Usage: %s <filename>\n", argv[0]);
        return EXIT_FAILURE;
    }

    // Create a child process
    pid_t pid = fork();

    if (pid == -1) {
        perror("fork");
        return EXIT_FAILURE;
    } else if (pid == 0) {
        // Child process
        child_process();
    } else {
        // Parent process
        parent_process(argv[1]);
    }

    return EXIT_SUCCESS;
}


#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <ctype.h>
#include <sys/types.h>
#include <sys/wait.h>

#define BUFFER_SIZE 1024

void to_lowercase(FILE *input_file) {
    char buffer[BUFFER_SIZE];
    ssize_t bytes_read;

    // Read from input file and convert to lowercase
    while ((bytes_read = fread(buffer, 1, BUFFER_SIZE, input_file)) > 0) {
        for (ssize_t i = 0; i < bytes_read; i++) {
            buffer[i] = tolower(buffer[i]);
        }
        write(STDOUT_FILENO, buffer, bytes_read);
    }
}

int main(int argc, char *argv[]) {
    if (argc != 2) {
        fprintf(stderr, "Usage: %s <filename>\n", argv[0]);
        return EXIT_FAILURE;
    }

    // Open the input file for reading
    FILE *input_file = fopen(argv[1], "r");
    if (input_file == NULL) {
        perror("fopen");
        return EXIT_FAILURE;
    }

    // Create a pipe
    int pipe_fd[2];
    if (pipe(pipe_fd) == -1) {
        perror("pipe");
        return EXIT_FAILURE;
    }

    // Fork a child process
    pid_t pid = fork();
    if (pid == -1) {
        perror("fork");
        return EXIT_FAILURE;
    }

    if (pid == 0) {
        // Child process
        close(pipe_fd[1]); // Close the write end of the pipe in the child

        // Redirect stdin to read from the pipe
        dup2(pipe_fd[0], STDIN_FILENO);

        // Close the read end of the pipe
        close(pipe_fd[0]);

        // Execute the filter (convert to lowercase)
        execlp("tr", "tr", "[:upper:]", "[:lower:]", NULL);
        perror("execlp");
        return EXIT_FAILURE;
    } else {
        // Parent process
        close(pipe_fd[0]); // Close the read end of the pipe in the parent

        // Redirect stdout to write to the pipe
        dup2(pipe_fd[1], STDOUT_FILENO);

        // Close the write end of the pipe
        close(pipe_fd[1]);

        // Call the function to convert to lowercase and write to pipe
        to_lowercase(input_file);

        // Close the input file
        fclose(input_file);

        // Wait for the child process to finish
        wait(NULL);
    }

    return EXIT_SUCCESS;
}



Write a program to illustrate the semaphore concept. Use fork so that 2 process running
simultaneously and communicate via semaphore. (give diff between sem.h/semaphore.h)

#include <iostream>
#include <unistd.h>
#include <semaphore.h>
#include <sys/wait.h>

using namespace std;

int main() {
    // Create a semaphore
    sem_t semaphore;
    sem_init(&semaphore, 0, 1); // Initialize the semaphore with initial value 1

    // Fork a child process
    pid_t pid = fork();

    if (pid == -1) {
        cerr << "Failed to fork." << endl;
        return 1;
    } else if (pid == 0) {
        // Child process
        sem_wait(&semaphore); // Wait for the semaphore
        cout << "Child process is running." << endl;
        sem_post(&semaphore); // Release the semaphore
    } else {
        // Parent process
        sem_wait(&semaphore); // Wait for the semaphore
        cout << "Parent process is running." << endl;
        sem_post(&semaphore); // Release the semaphore
        wait(NULL); // Wait for the child process to finish
    }

    // Destroy the semaphore
    sem_destroy(&semaphore);

    return 0;
}


61. Write 3 programs separately, 1st program will initialize the semaphore and display the
semaphore ID. 2nd program will perform the P operation and print message accordingly. 3rd
program will perform the V operation print the message accordingly for the same
semaphore declared in the 1st program.



program1:nto run process 
Program to initialize the semaphore and display its ID:

#include <iostream>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/sem.h>

using namespace std;

int main() {
    // Create a key for the semaphore
    key_t key = ftok("/tmp", 'S');
    if (key == -1) {
        perror("ftok");
        return 1;
    }

    // Create the semaphore
    int semaphoreID = semget(key, 1, IPC_CREAT | 0666);
    if (semaphoreID == -1) {
        perror("semget");
        return 1;
    }

    cout << "Semaphore created with ID: " << semaphoreID << endl;

    return 0;
}
Program to perform the "P" operation (wait) on the semaphore:
cpp
Copy code
#include <iostream>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/sem.h>

using namespace std;

int main() {
    // Get the key for the semaphore
    key_t key = ftok("/tmp", 'S');
    if (key == -1) {
        perror("ftok");
        return 1;
    }

    // Get the semaphore ID
    int semaphoreID = semget(key, 1, 0);
    if (semaphoreID == -1) {
        perror("semget");
        return 1;
    }

    // Perform the P operation
    struct sembuf operation;
    operation.sem_num = 0;  // Semaphore index
    operation.sem_op = -1;  // P operation
    operation.sem_flg = 0;  // No flags

    if (semop(semaphoreID, &operation, 1) == -1) {
        perror("semop P");
        return 1;
    }

    cout << "P operation performed successfully." << endl;

    return 0;
}


perform v operation

#include <iostream>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/sem.h>

using namespace std;

int main() {
    // Get the key for the semaphore
    key_t key = ftok("/tmp", 'S');
    if (key == -1) {
        perror("ftok");
        return 1;
    }

    // Get the semaphore ID
    int semaphoreID = semget(key, 1, 0);
    if (semaphoreID == -1) {
        perror("semget");
        return 1;
    }

    // Perform the V operation
    struct sembuf operation;
    operation.sem_num = 0;  // Semaphore index
    operation.sem_op = 1;   // V operation
    operation.sem_flg = 0;  // No flags

    if (semop(semaphoreID, &operation, 1) == -1) {
        perror("semop V");
        return 1;
    }

    cout << "V operation performed successfully." << endl;

    return 0;
}
 command:g++ initialize_semaphore.cpp -o initialize_semaphore
g++ perform_P_operation.cpp -o perform_P_operation
g++ perform_V_operation.cpp -o perform_V_operation

execution:
./initialize_semaphore
./perform_P_operation
./perform_V_operation

modified:
initial:
#include <stdio.h>
#include <stdlib.h>
#include <semaphore.h>
#include <fcntl.h>
#include <sys/stat.h>

#define SEM_NAME "/my_semaphore"
#define INITIAL_VALUE 1

int main() {
    sem_t *sem;

    // Create a named semaphore (if not already existing)
    sem = sem_open(SEM_NAME, O_CREAT | O_EXCL, S_IRUSR | S_IWUSR, INITIAL_VALUE);
    if (sem == SEM_FAILED) {
        perror("sem_open");
        exit(EXIT_FAILURE);
    }

    // Display the semaphore ID (address)
    printf("Semaphore ID: %p\n", (void *)sem);

    // Close the semaphore
    sem_close(sem);

    return EXIT_SUCCESS;
}
p:
#include <stdio.h>
#include <stdlib.h>
#include <semaphore.h>

#define SEM_NAME "/my_semaphore"

int main() {
    sem_t *sem;

    // Open the existing named semaphore
    sem = sem_open(SEM_NAME, 0);
    if (sem == SEM_FAILED) {
        perror("sem_open");
        exit(EXIT_FAILURE);
    }

    // Perform the P operation (wait)
    printf("Program 2: Attempting P operation (wait) on semaphore...\n");
    if (sem_wait(sem) == -1) {
        perror("sem_wait");
        sem_close(sem);
        exit(EXIT_FAILURE);
    }

    printf("Program 2: Semaphore acquired (P operation successful)\n");

    // Close the semaphore
    sem_close(sem);

    return EXIT_SUCCESS;
}
v:
#include <stdio.h>
#include <stdlib.h>
#include <semaphore.h>

#define SEM_NAME "/my_semaphore"

int main() {
    sem_t *sem;

    // Open the existing named semaphore
    sem = sem_open(SEM_NAME, 0);
    if (sem == SEM_FAILED) {
        perror("sem_open");
        exit(EXIT_FAILURE);
    }

    // Perform the V operation (signal)
    printf("Program 3: Performing V operation (signal) on semaphore...\n");
    if (sem_post(sem) == -1) {
        perror("sem_post");
        sem_close(sem);
        exit(EXIT_FAILURE);
    }

    printf("Program 3: Semaphore released (V operation successful)\n");

    // Close the semaphore
    sem_close(sem);

    return EXIT_SUCCESS;
}



. Write a program to demonstrate the lockf system call for locking.

#include <iostream>
#include <unistd.h>
#include <fcntl.h>
#include <cstring>
#include <cstdlib>

using namespace std;

int main() {
    // Open a file
    int fd = open("example.txt", O_RDWR | O_CREAT, 0644);
    if (fd == -1) {
        perror("open");
        return 1;
    }

    // Lock the file
    if (lockf(fd, F_LOCK, 0) == -1) {
        perror("lockf");
        close(fd);
        return 1;
    }

    // Write to the locked file
    const char *message = "This is a locked file.";
    if (write(fd, message, strlen(message)) == -1) {
        perror("write");
        close(fd);
        return 1;
    }

    cout << "File locked and written successfully." << endl;

    // Unlock the file
    if (lockf(fd, F_ULOCK, 0) == -1) {
        perror("lockf");
        close(fd);
        return 1;
    }

    cout << "File unlocked." << endl;

    // Close the file
    close(fd);

    return 0;
}


Write a program to demonstrate the flock system call for locking.


#include <iostream>
#include <unistd.h>
#include <fcntl.h>
#include <cstring>
#include <cstdlib>

using namespace std;

int main() {
    // Open a file
    int fd = open("example.txt", O_RDWR | O_CREAT, 0644);
    if (fd == -1) {
        perror("open");
        return 1;
    }

    // Lock the file
    struct flock fl;
    fl.l_type = F_WRLCK;  // Exclusive write lock
    fl.l_whence = SEEK_SET;
    fl.l_start = 0;  // Start from the beginning of the file
    fl.l_len = 0;    // Lock the entire file

    if (fcntl(fd, F_SETLKW, &fl) == -1) {
        perror("fcntl");
        close(fd);
        return 1;
    }

    cout << "File locked." << endl;

    // Write to the locked file
    const char *message = "This is a locked file.";
    if (write(fd, message, strlen(message)) == -1) {
        perror("write");
        close(fd);
        return 1;
    }

    cout << "Message written to the locked file." << endl;

    // Unlock the file
    fl.l_type = F_UNLCK;

    if (fcntl(fd, F_SETLK, &fl) == -1) {
        perror("fcntl");
        close(fd);
        return 1;
    }

    cout << "File unlocked." << endl;

    // Close the file
    close(fd);

    return 0;
}





Q Write a program for TCP to demonstrate the socket system calls in c/python

Client

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

#define PORT 8080
#define BUFFER_SIZE 1024

int main() {
    int sock = 0, valread;
    struct sockaddr_in serv_addr;
    char *message = "Hello from client";
    char buffer[BUFFER_SIZE] = {0};

    // Create socket file descriptor
    if ((sock = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
        perror("Socket creation failed");
        exit(EXIT_FAILURE);
    }

    serv_addr.sin_family = AF_INET;
    serv_addr.sin_port = htons(PORT);

    // Convert IPv4 and IPv6 addresses from text to binary form
    if (inet_pton(AF_INET, "127.0.0.1", &serv_addr.sin_addr) <= 0) {
        perror("Invalid address/ Address not supported");
        exit(EXIT_FAILURE);
    }

    // Connect to server
    if (connect(sock, (struct sockaddr *)&serv_addr, sizeof(serv_addr)) < 0) {
        perror("Connection failed");
        exit(EXIT_FAILURE);
    }

    // Send message to server
    send(sock, message, strlen(message), 0);
    printf("Hello message sent to server\n");

    // Read message from server
    valread = read(sock, buffer, BUFFER_SIZE);
    printf("Message from server: %s\n", buffer);

    return 0;
}

server
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>

#define PORT 8080
#define BUFFER_SIZE 1024

int main() {
    int server_fd, new_socket, valread;
    struct sockaddr_in address;
    int addrlen = sizeof(address);
    char buffer[BUFFER_SIZE] = {0};
    char *message = "Hello from server";

    // Create socket file descriptor
    if ((server_fd = socket(AF_INET, SOCK_STREAM, 0)) == 0) {
        perror("Socket creation failed");
        exit(EXIT_FAILURE);
    }

    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons(PORT);

    // Bind the socket to the address and port
    if (bind(server_fd, (struct sockaddr *)&address, sizeof(address)) < 0) {
        perror("Bind failed");
        exit(EXIT_FAILURE);
    }

    // Listen for incoming connections
    if (listen(server_fd, 3) < 0) {
        perror("Listen failed");
        exit(EXIT_FAILURE);
    }

    // Accept the incoming connection
    if ((new_socket = accept(server_fd, (struct sockaddr *)&address, (socklen_t *)&addrlen)) < 0) {
        perror("Accept failed");
        exit(EXIT_FAILURE);
    }

    // Read message from client
    valread = read(new_socket, buffer, BUFFER_SIZE);
    printf("Message from client: %s\n", buffer);

    // Send message to client
    send(new_socket, message, strlen(message), 0);
    printf("Hello message sent to client\n");

    return 0;
}




Q Write a program for UDP to demonstrate the socket system calls in c/python

Client

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 12345
#define MAXLINE 1024

int main() {
    int sockfd;
    char buffer[MAXLINE];
    struct sockaddr_in servaddr;

    // Creating socket file descriptor
    if ((sockfd = socket(AF_INET, SOCK_DGRAM, 0)) < 0) {
        perror("socket creation failed");
        exit(EXIT_FAILURE);
    }

    memset(&servaddr, 0, sizeof(servaddr));

    // Filling server information
    servaddr.sin_family = AF_INET;
    servaddr.sin_port = htons(PORT);
    servaddr.sin_addr.s_addr = INADDR_ANY;

    while (1) {
        printf("Enter message: ");
        fgets(buffer, MAXLINE, stdin);

        sendto(sockfd, (const char *)buffer, strlen(buffer), MSG_CONFIRM, (const struct sockaddr *)&servaddr, sizeof(servaddr));
        printf("Message sent.\n");

        int n = recvfrom(sockfd, (char *)buffer, MAXLINE, MSG_WAITALL, NULL, NULL);
        buffer[n] = '\0';
        printf("Server : %s\n", buffer);
    }

    close(sockfd);
    return 0;
}

Server

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 12345
#define MAXLINE 1024

int main() {
    int sockfd;
    char buffer[MAXLINE];
    struct sockaddr_in servaddr, cliaddr;

    // Creating socket file descriptor
    if ((sockfd = socket(AF_INET, SOCK_DGRAM, 0)) < 0) {
        perror("socket creation failed");
        exit(EXIT_FAILURE);
    }

    memset(&servaddr, 0, sizeof(servaddr));
    memset(&cliaddr, 0, sizeof(cliaddr));

    // Filling server information
    servaddr.sin_family = AF_INET; // IPv4
    servaddr.sin_addr.s_addr = INADDR_ANY;
    servaddr.sin_port = htons(PORT);

    // Binding socket with server address
    if (bind(sockfd, (const struct sockaddr *)&servaddr, sizeof(servaddr)) < 0) {
        perror("bind failed");
        exit(EXIT_FAILURE);
    }

    printf("Server listening on port %d\n", PORT);

    while (1) {
        int len, n;

        len = sizeof(cliaddr);  //len is value/resuslt

        n = recvfrom(sockfd, (char *)buffer, MAXLINE, MSG_WAITALL, (struct sockaddr *)&cliaddr, &len);
        buffer[n] = '\0';
        printf("Client : %s\n", buffer);
        sendto(sockfd, (const char *)buffer, strlen(buffer), MSG_CONFIRM, (const struct sockaddr *)&cliaddr, len);
        printf("Message sent to client.\n");
    }

    return 0;
}


Implement echo server using TCP in iterative/concurrent logic.

Client

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 8080
#define BUFFER_SIZE 1024

int main() {
    int sock = 0;
    struct sockaddr_in serv_addr;
    char buffer[BUFFER_SIZE] = {0};
    const char *message = "Hello from client";

    // Create socket
    if ((sock = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
        perror("Socket creation error");
        exit(EXIT_FAILURE);
    }

    serv_addr.sin_family = AF_INET;
    serv_addr.sin_port = htons(PORT);

    // Convert IPv4 and IPv6 addresses from text to binary form
    if (inet_pton(AF_INET, "127.0.0.1", &serv_addr.sin_addr) <= 0) {
        perror("Invalid address/ Address not supported");
        exit(EXIT_FAILURE);
    }

    // Connect to server
    if (connect(sock, (struct sockaddr *)&serv_addr, sizeof(serv_addr)) < 0) {
        perror("Connection failed");
        exit(EXIT_FAILURE);
    }

    // Send message to server
    send(sock, message, strlen(message), 0);
    printf("Message sent to server: %s\n", message);

    // Read message from server
    read(sock, buffer, BUFFER_SIZE);
    printf("Message from server: %s\n", buffer);

    return 0;
}

Server

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 8080
#define MAX_CONNECTIONS 5
#define BUFFER_SIZE 1024

int main() {
    int server_fd, new_socket;
    struct sockaddr_in address;
    int opt = 1;
    int addrlen = sizeof(address);
    char buffer[BUFFER_SIZE] = {0};
    const char *message = "Echo from server: ";

    // Creating socket file descriptor
    if ((server_fd = socket(AF_INET, SOCK_STREAM, 0)) == 0) {
        perror("socket failed");
        exit(EXIT_FAILURE);
    }

    // Set socket options to reuse address and port
    if (setsockopt(server_fd, SOL_SOCKET, SO_REUSEADDR | SO_REUSEPORT, &opt, sizeof(opt))) {
        perror("setsockopt");
        exit(EXIT_FAILURE);
    }

    // Initialize address struct
    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons(PORT);

    // Bind socket to address
    if (bind(server_fd, (struct sockaddr *)&address, sizeof(address)) < 0) {
        perror("bind failed");
        exit(EXIT_FAILURE);
    }

    // Listen for incoming connections
    if (listen(server_fd, MAX_CONNECTIONS) < 0) {
        perror("listen");
        exit(EXIT_FAILURE);
    }

    // Accept incoming connections and handle them iteratively
    while (1) {
        if ((new_socket = accept(server_fd, (struct sockaddr *)&address, (socklen_t *)&addrlen)) < 0) {
            perror("accept");
            exit(EXIT_FAILURE);
        }

        // Read data from client
        read(new_socket, buffer, BUFFER_SIZE);

        // Send data back to client
        send(new_socket, message, strlen(message), 0);
        send(new_socket, buffer, strlen(buffer), 0);
        printf("Message sent to client: %s\n", buffer);

        // Clear the buffer
        memset(buffer, 0, sizeof(buffer));

        // Close the socket
        close(new_socket);
    }
    return 0;
}


Implement echo server using UDP in iterative/concurrent logic.

Client
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <arpa/inet.h>
#include <sys/socket.h>

#define PORT 9999
#define BUFFER_SIZE 4096

int main() {
    struct sockaddr_in server_addr;
    int sockfd;
    char buffer[BUFFER_SIZE];
    socklen_t server_len;

    // Create a UDP socket
    if ((sockfd = socket(AF_INET, SOCK_DGRAM, IPPROTO_UDP)) < 0) {
        perror("socket creation failed");
        exit(EXIT_FAILURE);
    }

    // Initialize server address structure
    memset(&server_addr, 0, sizeof(server_addr));
    server_addr.sin_family = AF_INET;
    server_addr.sin_addr.s_addr = INADDR_ANY;
    server_addr.sin_port = htons(PORT);

    while (1) {
        printf("Enter message to send (type 'exit' to quit): ");
        fgets(buffer, BUFFER_SIZE, stdin);

        // Remove newline character from the input
        buffer[strcspn(buffer, "\n")] = 0;

        if (strcmp(buffer, "exit") == 0) {
            break;
        }

        // Send message to the server
        server_len = sizeof(server_addr);
        if (sendto(sockfd, buffer, strlen(buffer), 0, (struct sockaddr*)&server_addr, server_len) < 0) {
            perror("sendto failed");
            exit(EXIT_FAILURE);
        }

        // Receive response from server
        if (recvfrom(sockfd, buffer, BUFFER_SIZE, 0, NULL, NULL) < 0) {
            perror("recvfrom failed");
            exit(EXIT_FAILURE);
        }

        printf("Received response: %s\n", buffer);
    }

    // Close the socket
    close(sockfd);

    return 0;
}

Server
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <arpa/inet.h>
#include <sys/socket.h>

#define PORT 9999
#define BUFFER_SIZE 4096

int main() {
    struct sockaddr_in server_addr, client_addr;
    int sockfd, client_len, recv_len;
    char buffer[BUFFER_SIZE];

    // Create a UDP socket
    if ((sockfd = socket(AF_INET, SOCK_DGRAM, IPPROTO_UDP)) < 0) {
        perror("socket creation failed");
        exit(EXIT_FAILURE);
    }

    // Initialize server address structure
    memset(&server_addr, 0, sizeof(server_addr));
    server_addr.sin_family = AF_INET;
    server_addr.sin_addr.s_addr = INADDR_ANY;
    server_addr.sin_port = htons(PORT);

    // Bind the socket
    if (bind(sockfd, (struct sockaddr*)&server_addr, sizeof(server_addr)) < 0) {
        perror("bind failed");
        exit(EXIT_FAILURE);
    }

    printf("Server is running on port %d\n", PORT);

    while (1) {
        printf("\nWaiting to receive message...\n");

        // Receive message from client
        client_len = sizeof(client_addr);
        if ((recv_len = recvfrom(sockfd, buffer, BUFFER_SIZE, 0, (struct sockaddr*)&client_addr, &client_len)) < 0) {
            perror("recvfrom failed");
            exit(EXIT_FAILURE);
        }

        printf("Received %d bytes from %s:%d\n", recv_len, inet_ntoa(client_addr.sin_addr), ntohs(client_addr.sin_port));
        printf("Data received: %s\n", buffer);

        // Echo back the received data
        if (sendto(sockfd, buffer, recv_len, 0, (struct sockaddr*)&client_addr, client_len) < 0) {
            perror("sendto failed");
            exit(EXIT_FAILURE);
        }
    }

    return 0;
}


41.Write a program to demonstrate IPC using shared memory (shmget, shmat,
shmdt). In this, one process will send A to Z/1 to 100 as input from user and another
process will receive it.

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/wait.h>

#define SHM_SIZE 1024

int main() {
    int shmid;
    key_t key;
    char *shm, *s;

    // Create a unique key
    key = ftok(".", 's');
    if (key == -1) {
        perror("ftok");
        exit(1);
    }

    // Create the shared memory segment
    shmid = shmget(key, SHM_SIZE, IPC_CREAT | 0666);
    if (shmid == -1) {
        perror("shmget");
        exit(1);
    }

    // Attach to the shared memory
    shm = shmat(shmid, NULL, 0);
    if (shm == (char *) -1) {
        perror("shmat");
        exit(1);
    }

    // Fork a child process
    pid_t pid = fork();

    if (pid == -1) {
        perror("fork");
        exit(1);
    }

    if (pid == 0) { // Child process (receiver)
        printf("Child process: Waiting for data...\n");

        // Wait for the parent process to write data
        while (*shm == 0)
            usleep(100);

        printf("Child process: Received data: %s\n", shm);

        // Detach from the shared memory
        if (shmdt(shm) == -1) {
            perror("shmdt");
            exit(1);
        }

        exit(0);
    } else { // Parent process (sender)
        printf("Parent process: Enter data to send (A to Z or 1 to 100): ");
        fgets(shm, SHM_SIZE, stdin);

        // Wait for the child process to complete
        wait(NULL);

        // Detach from the shared memory
        if (shmdt(shm) == -1) {
            perror("shmdt");
            exit(1);
        }

        // Remove the shared memory segment
        shmctl(shmid, IPC_RMID, NULL);
    }

    return 0;
}
/*
Commands
gcc -o filename filename.c
./filename

*/


42. Write a program to demonstrate IPC using shared memory (shmget, shmat,
shmdt). In this, one process will send from file A to Z/1 to 100 as input from user
and another process will receive it in file. (use same directory and different name
files)
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/wait.h>

#define SHM_SIZE 1024
#define DATA_FILE "data.txt"
#define RESULT_FILE "result.txt"

int main() {
    int shmid;
    key_t key;
    char *shm, *s;

    // Create a unique key
    key = ftok(".", 's');
    if (key == -1) {
        perror("ftok");
        exit(1);
    }

    // Create the shared memory segment
    shmid = shmget(key, SHM_SIZE, IPC_CREAT | 0666);
    if (shmid == -1) {
        perror("shmget");
        exit(1);
    }

    // Attach to the shared memory
    shm = shmat(shmid, NULL, 0);
    if (shm == (char *) -1) {
        perror("shmat");
        exit(1);
    }

    // Fork a child process
    pid_t pid = fork();

    if (pid == -1) {
        perror("fork");
        exit(1);
    }

    if (pid == 0) { // Child process (receiver)
        FILE *result_file = fopen(RESULT_FILE, "w");
        if (result_file == NULL) {
            perror("fopen");
            exit(1);
        }

        printf("Child process: Waiting for data...\n");

        // Wait for the parent process to write data
        while (*shm == 0)
            usleep(100);

        // Write the received data to a file
        fprintf(result_file, "%s", shm);
        printf("Child process: Received data and written to %s\n", RESULT_FILE);

        // Close the result file
        fclose(result_file);

        // Detach from the shared memory
        if (shmdt(shm) == -1) {
            perror("shmdt");
            exit(1);
        }

        exit(0);
    } else { // Parent process (sender)
        FILE *data_file = fopen(DATA_FILE, "r");
        if (data_file == NULL) {
            perror("fopen");
            exit(1);
        }

        printf("Parent process: Reading data from %s...\n", DATA_FILE);

        // Read data from the file
        fgets(shm, SHM_SIZE, data_file);

        // Close the data file
        fclose(data_file);

        printf("Parent process: Sending data to child process...\n");

        // Wait for the child process to complete
        wait(NULL);

        // Detach from the shared memory
        if (shmdt(shm) == -1) {
            perror("shmdt");
            exit(1);
        }

        // Remove the shared memory segment
        shmctl(shmid, IPC_RMID, NULL);
    }

    return 0;
}

/*
Commands
gcc -o filename filename.c
./filename

*/
43. Write a program to demonstrate IPC using shared memory (shmget, shmat, shmdt). In
this, one process will take numbers as input from user and second process will sort the
numbers and put back to shared memory. Third process will display the shared memory.
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/wait.h>

#define SHM_SIZE 1024

int main() {
    int shmid;
    key_t key;
    int *shm, *s;

    // Create a unique key
    key = ftok(".", 's');
    if (key == -1) {
        perror("ftok");
        exit(1);
    }

    // Create the shared memory segment
    shmid = shmget(key, SHM_SIZE, IPC_CREAT | 0666);
    if (shmid == -1) {
        perror("shmget");
        exit(1);
    }

    // Attach to the shared memory
    shm = shmat(shmid, NULL, 0);
    if (shm == (int *) -1) {
        perror("shmat");
        exit(1);
    }

    // Fork a child process to take input from the user
    pid_t pid_input = fork();

    if (pid_input == -1) {
        perror("fork");
        exit(1);
    }

    if (pid_input == 0) { // Child process (input)
        printf("Enter the number of elements: ");
        int num_elements;
        scanf("%d", &num_elements);

        printf("Enter %d numbers:\n", num_elements);
        for (int i = 0; i < num_elements; i++) {
            scanf("%d", &shm[i]);
        }

        // Detach from the shared memory
        if (shmdt(shm) == -1) {
            perror("shmdt");
            exit(1);
        }

        exit(0);
    } else { // Parent process (sort)
        wait(NULL); // Wait for the input process to complete

        // Fork another child process to sort the numbers
        pid_t pid_sort = fork();

        if (pid_sort == -1) {
            perror("fork");
            exit(1);
        }

        if (pid_sort == 0) { // Child process (sort)
            // Sort the numbers using bubble sort
            int temp;
            for (int i = 0; i < SHM_SIZE / sizeof(int); i++) {
                for (int j = 0; j < SHM_SIZE / sizeof(int) - i - 1; j++) {
                    if (shm[j] > shm[j + 1]) {
                        temp = shm[j];
                        shm[j] = shm[j + 1];
                        shm[j + 1] = temp;
                    }
                }
            }

            // Detach from the shared memory
            if (shmdt(shm) == -1) {
                perror("shmdt");
                exit(1);
            }

            exit(0);
        } else { // Parent process (display)
            wait(NULL); // Wait for the sort process to complete

            // Fork another child process to display the sorted numbers
            pid_t pid_display = fork();

            if (pid_display == -1) {
                perror("fork");
                exit(1);
            }

            if (pid_display == 0) { // Child process (display)
                printf("Sorted numbers:\n");
                for (int i = 0; i < SHM_SIZE / sizeof(int); i++) {
                    printf("%d ", shm[i]);
                }
                printf("\n");

                // Detach from the shared memory
                if (shmdt(shm) == -1) {
                    perror("shmdt");
                    exit(1);
                }

                exit(0);
            }
        }
    }

    // Wait for all child processes to complete
    wait(NULL);
    wait(NULL);
    wait(NULL);

    // Remove the shared memory segment
    shmctl(shmid, IPC_RMID, NULL);

    return 0;
}
/*
Commands
gcc -o shared_memory_sort shared_memory_sort.c
./shared_memory_sort

*/



44. Write a program in which different processes will perform different operation on shared
memory. Operation: create memory, delete, attach/ detach(using shmget, shmat, shmdt).
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/wait.h>

#define SHM_SIZE 1024

int main() {
    int shmid;
    key_t key;
    void *shm;

    // Create a unique key
    key = ftok(".", 's');
    if (key == -1) {
        perror("ftok");
        exit(1);
    }

    // Fork a child process to create shared memory
    pid_t pid_create = fork();

    if (pid_create == -1) {
        perror("fork");
        exit(1);
    }

    if (pid_create == 0) { // Child process (create)
        printf("Child process (create): Creating shared memory...\n");

        // Create the shared memory segment
        shmid = shmget(key, SHM_SIZE, IPC_CREAT | 0666);
        if (shmid == -1) {
            perror("shmget");
            exit(1);
        }

        printf("Child process (create): Shared memory created with ID: %d\n", shmid);

        exit(0);
    } else { // Parent process (delete)
        wait(NULL); // Wait for the create process to complete

        // Fork another child process to delete shared memory
        pid_t pid_delete = fork();

        if (pid_delete == -1) {
            perror("fork");
            exit(1);
        }

        if (pid_delete == 0) { // Child process (delete)
            printf("Child process (delete): Deleting shared memory...\n");

            // Delete the shared memory segment
            if (shmctl(shmid, IPC_RMID, NULL) == -1) {
                perror("shmctl");
                exit(1);
            }

            printf("Child process (delete): Shared memory deleted\n");

            exit(0);
        } else { // Parent process (attach/detach)
            wait(NULL); // Wait for the delete process to complete

            // Fork another child process to attach/detach shared memory
            pid_t pid_attach_detach = fork();

            if (pid_attach_detach == -1) {
                perror("fork");
                exit(1);
            }

            if (pid_attach_detach == 0) { // Child process (attach/detach)
                printf("Child process (attach/detach): Attaching to shared memory...\n");

                // Attach to the shared memory
                shmid = shmget(key, SHM_SIZE, 0666);
                if (shmid == -1) {
                    perror("shmget");
                    exit(1);
                }

                shm = shmat(shmid, NULL, 0);
                if (shm == (void *) -1) {
                    perror("shmat");
                    exit(1);
                }

                printf("Child process (attach/detach): Attached to shared memory\n");

                // Wait for a while
                sleep(2);

                printf("Child process (attach/detach): Detaching from shared memory...\n");

                // Detach from the shared memory
                if (shmdt(shm) == -1) {
                    perror("shmdt");
                    exit(1);
                }

                printf("Child process (attach/detach): Detached from shared memory\n");

                exit(0);
            }
        }
    }

    // Wait for all child processes to complete
    wait(NULL);
    wait(NULL);
    wait(NULL);

    return 0;
}
/*
Commands to run
gcc -o shared_memory shared_memory.c
./shared_memory
*/

45. Write programs to simulate linux commands cat, ls, cp, mv, head etc.

/*
Commands to run
gcc -o cp cp.c
gcc -o head head.c
gcc -o ls ls.c
gcc -o mv mv.c


./cp source_file destination_file
./head [number_of_lines] [file_name]
./ls [directory_path]
./mv source_file destination_file


*/
//cat
#include <stdio.h>

int main(int argc, char *argv[]) {
    if (argc < 2) {
        printf("Usage: %s <file1> [<file2> ...]\n", argv[0]);
        return 1;
    }

    for (int i = 1; i < argc; i++) {
        FILE *file = fopen(argv[i], "r");
        if (file == NULL) {
            printf("Error: Cannot open file %s\n", argv[i]);
            continue;
        }

        char c;
        while ((c = fgetc(file)) != EOF) {
            putchar(c);
        }

        fclose(file);
    }

    return 0;
}

// commands to run
/*
gcc -o cat cat.c
./cat file1.txt file2.txt

*/

//cp
#include <stdio.h>

int main(int argc, char *argv[]) {
    if (argc != 3) {
        printf("Usage: %s <source> <destination>\n", argv[0]);
        return 1;
    }

    FILE *source_file = fopen(argv[1], "r");
    if (source_file == NULL) {
        perror("fopen");
        return 1;
    }

    FILE *destination_file = fopen(argv[2], "w");
    if (destination_file == NULL) {
        perror("fopen");
        fclose(source_file);
        return 1;
    }

    char c;
    while ((c = fgetc(source_file)) != EOF) {
        fputc(c, destination_file);
    }

    fclose(source_file);
    fclose(destination_file);

    return 0;
}

//head
#include <stdio.h>

#define DEFAULT_NUM_LINES 10

int main(int argc, char *argv[]) {
    int num_lines = DEFAULT_NUM_LINES;
    if (argc > 1) {
        num_lines = atoi(argv[1]);
    }

    FILE *file = stdin;
    if (argc > 2) {
        file = fopen(argv[2], "r");
        if (file == NULL) {
            perror("fopen");
            return 1;
        }
    }

    int lines_printed = 0;
    char buffer[1024];
    while (fgets(buffer, sizeof(buffer), file) != NULL && lines_printed < num_lines) {
        fputs(buffer, stdout);
        lines_printed++;
    }

    if (file != stdin) {
        fclose(file);
    }

    return 0;
}


//ls
#include <stdio.h>
#include <dirent.h>

int main(int argc, char *argv[]) {
    const char *dir_path = argc > 1 ? argv[1] : ".";

    DIR *dir = opendir(dir_path);
    if (dir == NULL) {
        perror("opendir");
        return 1;
    }

    struct dirent *entry;
    while ((entry = readdir(dir)) != NULL) {
        printf("%s\n", entry->d_name);
    }

    closedir(dir);
    return 0;
}

//mv

#include <stdio.h>

int main(int argc, char *argv[]) {
    if (argc != 3) {
        printf("Usage: %s <source> <destination>\n", argv[0]);
        return 1;
    }

    if (rename(argv[1], argv[2]) == -1) {
        perror("rename");
        return 1;
    }

    return 0;
}


46. Write a program to ensure that function f1 should executed before executing function f2
using semaphore. (Ex. Program should ask for username before entering password)
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <semaphore.h>

// Define semaphores
sem_t sem_f1;
sem_t sem_f2;

void *f1(void *arg) {
    // Ask for username
    printf("Enter username: ");
    char username[100];
    scanf("%s", username);

    // Signal that f1 is done
    sem_post(&sem_f1);

    pthread_exit(NULL);
}

void *f2(void *arg) {
    // Wait for f1 to finish
    sem_wait(&sem_f1);

    // Now execute f2
    printf("Enter password: ");
    char password[100];
    scanf("%s", password);

    pthread_exit(NULL);
}

int main() {
    // Initialize semaphores
    sem_init(&sem_f1, 0, 0);
    sem_init(&sem_f2, 0, 0);

    // Create threads for f1 and f2
    pthread_t thread_f1, thread_f2;

    pthread_create(&thread_f1, NULL, f1, NULL);
    pthread_create(&thread_f2, NULL, f2, NULL);

    // Wait for threads to finish
    pthread_join(thread_f1, NULL);
    pthread_join(thread_f2, NULL);

    // Destroy semaphores
    sem_destroy(&sem_f1);
    sem_destroy(&sem_f2);

    return 0;
}

/*
gcc -o threads threads.c -pthread
./threads


*/


47. Write a program using OpenMP library to parallelize the for loop in sequential program
of finding prime numbers in given range.

#include <stdio.h>
#include <omp.h>

int is_prime(int n) {
    if (n <= 1) return 0;
    if (n <= 3) return 1;
    if (n % 2 == 0 || n % 3 == 0) return 0;

    for (int i = 5; i * i <= n; i += 6) {
        if (n % i == 0 || n % (i + 2) == 0) return 0;
    }

    return 1;
}

int main() {
    int lower = 1, upper = 100000;
    int num_primes = 0;

    #pragma omp parallel for reduction(+:num_primes)
    for (int i = lower; i <= upper; i++) {
        if (is_prime(i)) {
            num_primes++;
        }
    }

    printf("Number of prime numbers between %d and %d: %d\n", lower, upper, num_primes);

    return 0;
}

/*
gcc -o prime_numbers -fopenmp prime_numbers.c
./prime_numbers

*/


48. Using OpemnMP library write a program in which master thread count the total no. of
threads created, and others will print their thread numbers.
#include <stdio.h>
#include <omp.h>

int main() {
    int total_threads = 0;

    #pragma omp parallel
    {
        #pragma omp master
        {
            total_threads = omp_get_num_threads();
            printf("Total number of threads created: %d\n", total_threads);
        }

        int thread_num = omp_get_thread_num();
        printf("Thread %d reporting.\n", thread_num);
    }

    return 0;
}

/*
gcc -o thread_info -fopenmp thread_info.c
./thread_info

*/



49. Implement the program for IPC using MPI library (“Hello world” program).

#include <stdio.h>
#include <mpi.h>

int main(int argc, char *argv[]) {
    int rank, size;

    // Initialize MPI
    MPI_Init(&argc, &argv);

    // Get the rank of the current process
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);

    // Get the total number of processes
    MPI_Comm_size(MPI_COMM_WORLD, &size);

    // Print "Hello world" from each process
    printf("Hello world from process %d out of %d\n", rank, size);

    // Finalize MPI
    MPI_Finalize();

    return 0;
}
/*
commands to run
mpicc -o mpi_hello mpi_hello.c
mpiexec -n 4 ./mpi_hello

*/
50. Write a 2 programs that will both send and messages and construct the following
dialog between them
(Process 1) Sends the message "Are you hearing me?"
(Process 2) Receives the message and replies "Loud and Clear".
(Process 1) Receives the reply and then says "I can hear you too".
IPC:Message Queues:msgget, msgsnd, msgrcv.


#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <string.h>

#define MSGSZ 128

typedef struct msgbuf {
    long mtype;
    char mtext[MSGSZ];
} message_buf;

int main() {
    int msqid;
    key_t key;
    message_buf sbuf, rbuf;
    size_t buf_length;

    // Generate a key for the message queue
    if ((key = ftok("msgq.txt", 'B')) == -1) {
        perror("ftok");
        exit(1);
    }

    // Create a message queue
    if ((msqid = msgget(key, 0644 | IPC_CREAT)) == -1) {
        perror("msgget");
        exit(1);
    }

    // Send message
    sbuf.mtype = 1;
    strcpy(sbuf.mtext, "Are you hearing me?");
    buf_length = strlen(sbuf.mtext) + 1;

    if (msgsnd(msqid, &sbuf, buf_length, 0) == -1) {
        perror("msgsnd");
        exit(1);
    }

    // Receive reply
    if (msgrcv(msqid, &rbuf, MSGSZ, 2, 0) == -1) {
        perror("msgrcv");
        exit(1);
    }

    printf("Process 2: %s\n", rbuf.mtext);

    // Cleanup
    if (msgctl(msqid, IPC_RMID, NULL) == -1) {
        perror("msgctl");
        exit(1);
    }

    return 0;
}


#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <string.h>

#define MSGSZ 128

typedef struct msgbuf {
    long mtype;
    char mtext[MSGSZ];
} message_buf;

int main() {
    int msqid;
    key_t key;
    message_buf rbuf, sbuf;
    size_t buf_length;

    // Generate a key for the message queue
    if ((key = ftok("msgq.txt", 'B')) == -1) {
        perror("ftok");
        exit(1);
    }

    // Get the message queue
    if ((msqid = msgget(key, 0644)) == -1) {
        perror("msgget");
        exit(1);
    }

    // Receive message
    if (msgrcv(msqid, &rbuf, MSGSZ, 1, 0) == -1) {
        perror("msgrcv");
        exit(1);
    }

    printf("Process 1: %s\n", rbuf.mtext);

    // Send reply
    sbuf.mtype = 2;
    strcpy(sbuf.mtext, "Loud and Clear");
    buf_length = strlen(sbuf.mtext) + 1;

    if (msgsnd(msqid, &sbuf, buf_length, 0) == -1) {
        perror("msgsnd");
        exit(1);
    }

    return 0;
}



/*
commands to run
// open 2 terminals for 2 processes

gcc -o process1 process1.c
./process1

gcc -o process2 process2.c
./process2

*/

modified:
1st
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <string.h>

#define MSGSZ 128

typedef struct msgbuf {
    long mtype;
    char mtext[MSGSZ];
} message_buf;

int main() {
    int msqid;
    key_t key;
    message_buf sbuf, rbuf;
    size_t buf_length;

    // Generate a key for the message queue
    if ((key = ftok("msgq.txt", 'B')) == -1) {
        perror("ftok");
        exit(1);
    }

    // Create a message queue
    if ((msqid = msgget(key, 0644 | IPC_CREAT)) == -1) {
        perror("msgget");
        exit(1);
    }

    // Send message
    sbuf.mtype = 1;
    strcpy(sbuf.mtext, "Are you hearing me?");
    buf_length = strlen(sbuf.mtext) + 1;

    if (msgsnd(msqid, &sbuf, buf_length, 0) == -1) {
        perror("msgsnd");
        exit(1);
    }

    // Receive reply
    if (msgrcv(msqid, &rbuf, MSGSZ, 2, 0) == -1) {
        perror("msgrcv");
        exit(1);
    }

    printf("Process 2: %s\n", rbuf.mtext);

    // Send "I can hear you too" message
    sbuf.mtype = 1;
    strcpy(sbuf.mtext, "I can hear you too");
    buf_length = strlen(sbuf.mtext) + 1;

    if (msgsnd(msqid, &sbuf, buf_length, 0) == -1) {
        perror("msgsnd");
        exit(1);
    }

    // Cleanup
    if (msgctl(msqid, IPC_RMID, NULL) == -1) {
        perror("msgctl");
        exit(1);
    }

    return 0;
}

2nd program:
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <string.h>

#define MSGSZ 128

typedef struct msgbuf {
    long mtype;
    char mtext[MSGSZ];
} message_buf;

int main() {
    int msqid;
    key_t key;
    message_buf rbuf, sbuf;
    size_t buf_length;

    // Generate a key for the message queue
    if ((key = ftok("msgq.txt", 'B')) == -1) {
        perror("ftok");
        exit(1);
    }

    // Get the message queue
    if ((msqid = msgget(key, 0644)) == -1) {
        perror("msgget");
        exit(1);
    }

    // Receive message
    if (msgrcv(msqid, &rbuf, MSGSZ, 1, 0) == -1) {
        perror("msgrcv");
        exit(1);
    }

    printf("Process 1: %s\n", rbuf.mtext);

    // Send reply "Loud and Clear"
    sbuf.mtype = 2;
    strcpy(sbuf.mtext, "Loud and Clear");
    buf_length = strlen(sbuf.mtext) + 1;

    if (msgsnd(msqid, &sbuf, buf_length, 0) == -1) {
        perror("msgsnd");
        exit(1);
    }

    // Receive "I can hear you too" message
    if (msgrcv(msqid, &rbuf, MSGSZ, 1, 0) == -1) {
        perror("msgrcv");
        exit(1);
    }

    printf("Process 1: %s\n", rbuf.mtext);

    return 0;
}


Q Write a multithreaded program in JAVA for chatting.

Server
import java.io.*;
import java.net.*;
import java.util.concurrent.CopyOnWriteArrayList;

public class ChatServer {
    private static final int PORT = 1234;
    private static CopyOnWriteArrayList<ClientHandler> clients = new CopyOnWriteArrayList<>();

    public static void main(String[] args) {
        try (ServerSocket serverSocket = new ServerSocket(PORT)) {
            System.out.println("Server is listening on port " + PORT);
            
            while (true) {
                Socket socket = serverSocket.accept();
                ClientHandler clientThread = new ClientHandler(socket);
                clients.add(clientThread);
                clientThread.start();
            }
        } catch (IOException ex) {
            System.out.println("Server exception: " + ex.getMessage());
            ex.printStackTrace();
        }
    }

    static void broadcast(String message, ClientHandler excludeUser) {
        for (ClientHandler aClient : clients) {
            if (aClient != excludeUser) {
                aClient.sendMessage(message);
            }
        }
    }

    static void removeClient(ClientHandler client) {
        clients.remove(client);
        if (client.getUserName() != null) {
            System.out.println("The client [" + client.getUserName() + "] disconnected");
            broadcast("The client [" + client.getUserName() + "] has left the chat.", null);
        }
    }

    static class ClientHandler extends Thread {
        private Socket socket;
        private PrintWriter writer;
        private String userName;

        public ClientHandler(Socket socket) {
            this.socket = socket;
        }

        public void run() {
            try {
                InputStream input = socket.getInputStream();
                BufferedReader reader = new BufferedReader(new InputStreamReader(input));
                OutputStream output = socket.getOutputStream();
                writer = new PrintWriter(output, true);

                String userName = reader.readLine();
                this.userName = userName;
                String serverMessage = "New user connected: " + userName;
                System.out.println(serverMessage);
                ChatServer.broadcast(serverMessage, this);

                String clientMessage;

                do {
                    clientMessage = reader.readLine();
                    serverMessage = "[" + userName + "]: " + clientMessage;
                    ChatServer.broadcast(serverMessage, this);

                } while (!clientMessage.equals("bye"));

                ChatServer.removeClient(this);
                socket.close();

            } catch (IOException ex) {
                System.out.println("Error in UserThread: " + ex.getMessage());
                ex.printStackTrace();
            }
        }

        void sendMessage(String message) {
            writer.println(message);
        }

        String getUserName() {
            return this.userName;
        }
    }
}



Client
import java.io.*;
import java.net.*;

public class ChatClient {
    private String userName;
    private String hostname = "localhost";  
    private int port = 1234;   

    public ChatClient() {
        
    }

    public void execute() {
        try {
            Socket socket = new Socket(hostname, port);
            System.out.println("Connected to the chat server");

            new ReadThread(socket, this).start();
            new WriteThread(socket, this).start();

        } catch (UnknownHostException ex) {
            System.out.println("Server not found: " + ex.getMessage());
        } catch (IOException ex) {
            System.out.println("I/O Error: " + ex.getMessage());
        }
    }

    void setUserName(String userName) {
        this.userName = userName;
    }

    String getUserName() {
        return this.userName;
    }

    public static void main(String[] args) {
       
        ChatClient client = new ChatClient();
        client.execute();
    }

    static class ReadThread extends Thread {
        private BufferedReader reader;
        private Socket socket;
        private ChatClient client;

        public ReadThread(Socket socket, ChatClient client) {
            this.socket = socket;
            this.client = client;

            try {
                InputStream input = socket.getInputStream();
                reader = new BufferedReader(new InputStreamReader(input));
            } catch (IOException ex) {
                System.out.println("Error getting input stream: " + ex.getMessage());
                ex.printStackTrace();
            }
        }

        public void run() {
            while (true) {
                try {
                    String response = reader.readLine();
                    System.out.println("\n" + response);

                    // Prompt current user to enter their message right after displaying new messages
                    if (client.getUserName() != null) {
                        System.out.print("[" + client.getUserName() + "]: ");
                    }
                } catch (IOException ex) {
                    System.out.println("Error reading from server: " + ex.getMessage());
                    ex.printStackTrace();
                    break;
                }
            }
        }
    }

    static class WriteThread extends Thread {
        private PrintWriter writer;
        private Socket socket;
        private ChatClient client;

        public WriteThread(Socket socket, ChatClient client) {
            this.socket = socket;
            this.client = client;

            try {
                OutputStream output = socket.getOutputStream();
                writer = new PrintWriter(output, true);
            } catch (IOException ex) {
                System.out.println("Error getting output stream: " + ex.getMessage());
                ex.printStackTrace();
            }
        }

        public void run() {
            Console console = System.console();
            String userName = console.readLine("\nEnter your name: ");
            client.setUserName(userName);
            writer.println(userName);

            String text;

            do {
                text = console.readLine("[" + userName + "]: ");
                writer.println(text);

            } while (!text.equals("bye"));

            try {
                socket.close();
            } catch (IOException ex) {
                System.out.println("Error writing to server: " + ex.getMessage());
            }
        }
    }
}

modified in one code: java chatting
server:
// Java implementation of Server side
// It contains two classes : Server and ClientHandler
// Save file as Server.java

import java.io.*;
import java.util.*;
import java.net.*;

// Server class
public class Server 
{

	// Vector to store active clients
	static Vector<ClientHandler> ar = new Vector<>();
	
	// counter for clients
	static int i = 0;

	public static void main(String[] args) throws IOException 
	{
		// server is listening on port 1234
		ServerSocket ss = new ServerSocket(1234);
		
		Socket s;
		
		// running infinite loop for getting
		// client request
		while (true) 
		{
			// Accept the incoming request
			s = ss.accept();

			System.out.println("New client request received : " + s);
			
			// obtain input and output streams
			DataInputStream dis = new DataInputStream(s.getInputStream());
			DataOutputStream dos = new DataOutputStream(s.getOutputStream());
			
			System.out.println("Creating a new handler for this client...");

			// Create a new handler object for handling this request.
			ClientHandler mtch = new ClientHandler(s,"client " + i, dis, dos);

			// Create a new Thread with this object.
			Thread t = new Thread(mtch);
			
			System.out.println("Adding this client to active client list");

			// add this client to active clients list
			ar.add(mtch);

			// start the thread.
			t.start();

			// increment i for new client.
			// i is used for naming only, and can be replaced
			// by any naming scheme
			i++;

		}
	}
}

// ClientHandler class
class ClientHandler implements Runnable 
{
	Scanner scn = new Scanner(System.in);
	private String name;
	final DataInputStream dis;
	final DataOutputStream dos;
	Socket s;
	boolean isloggedin;
	
	// constructor
	public ClientHandler(Socket s, String name,
							DataInputStream dis, DataOutputStream dos) {
		this.dis = dis;
		this.dos = dos;
		this.name = name;
		this.s = s;
		this.isloggedin=true;
	}

	@Override
	public void run() {

		String received;
		while (true) 
		{
			try
			{
				// receive the string
				received = dis.readUTF();
				
				System.out.println(received);
				
				if(received.equals("logout")){
					this.isloggedin=false;
					this.s.close();
					break;
				}
				
				// break the string into message and recipient part
				StringTokenizer st = new StringTokenizer(received, "#");
				String MsgToSend = st.nextToken();
				String recipient = st.nextToken();

				// search for the recipient in the connected devices list.
				// ar is the vector storing client of active users
				for (ClientHandler mc : Server.ar) 
				{
					// if the recipient is found, write on its
					// output stream
					if (mc.name.equals(recipient) && mc.isloggedin==true) 
					{
						mc.dos.writeUTF(this.name+" : "+MsgToSend);
						break;
					}
				}
			} catch (IOException e) {
				
				e.printStackTrace();
			}
			
		}
		try
		{
			// closing resources
			this.dis.close();
			this.dos.close();
			
		}catch(IOException e){
			e.printStackTrace();
		}
	}
}

client:
// Java implementation for multithreaded chat client 
// Save file as Client.java 

import java.io.*; 
import java.net.*; 
import java.util.Scanner; 

public class Client 
{ 
	final static int ServerPort = 1234; 

	public static void main(String args[]) throws UnknownHostException, IOException 
	{ 
		Scanner scn = new Scanner(System.in); 
		
		// getting localhost ip 
		InetAddress ip = InetAddress.getByName("localhost"); 
		
		// establish the connection 
		Socket s = new Socket(ip, ServerPort); 
		
		// obtaining input and out streams 
		DataInputStream dis = new DataInputStream(s.getInputStream()); 
		DataOutputStream dos = new DataOutputStream(s.getOutputStream()); 

		// sendMessage thread 
		Thread sendMessage = new Thread(new Runnable() 
		{ 
			@Override
			public void run() { 
				while (true) { 

					// read the message to deliver. 
					String msg = scn.nextLine(); 
					
					try { 
						// write on the output stream 
						dos.writeUTF(msg); 
					} catch (IOException e) { 
						e.printStackTrace(); 
					} 
				} 
			} 
		}); 
		
		// readMessage thread 
		Thread readMessage = new Thread(new Runnable() 
		{ 
			@Override
			public void run() { 

				while (true) { 
					try { 
						// read the message sent to this client 
						String msg = dis.readUTF(); 
						System.out.println(msg); 
					} catch (IOException e) { 

						e.printStackTrace(); 
					} 
				} 
			} 
		}); 

		sendMessage.start(); 
		readMessage.start(); 

	} 
} 



write shell script with FIFO/mknod (named pipe) us for communication (IPC)

sender
#!/bin/bash

# Define the named pipe
PIPE=/tmp/my_fifo

# Create the named pipe if it doesn't exist
if [ ! -p $PIPE ]; then
    mkfifo $PIPE
fi

# Check if the receiver script is running
if ! pgrep -x "receiver.sh" > /dev/null; then
    echo "Receiver script is not running. Please start the receiver script before sending messages."
    exit 1
fi

# Prompt user to enter message
echo "Enter message to send (Press Ctrl+D to exit):"
while IFS= read -r line; do
    # Send message through the named pipe
    echo "$line" > $PIPE
done

reciever
#!/bin/bash

# Define the named pipe
PIPE=/tmp/my_fifo

# Create the named pipe if it doesn't exist
if [ ! -p $PIPE ]; then
    mkfifo $PIPE
fi

# Infinite loop to continuously listen for messages
while true; do
    # Read message from the named pipe
    if read line < $PIPE; then
        echo "Received message: $line"
    fi
done

Both scripts first define a named pipe (FIFO) path (/tmp/my_fifo).
They check if the named pipe already exists; if not, they create it using mkfifo.
The sender script (sender.sh) checks if the receiver script (receiver.sh) is running. If not, it prompts the user to start the receiver script first.
The sender script continuously reads input from the user and sends it to the named pipe.
The receiver script (receiver.sh) continuously listens for messages from the named pipe and displays them.
To use these scripts:

Save the sender script as sender.sh and the receiver script as receiver.sh.
Make both scripts executable: chmod +x sender.sh receiver.sh.
Open two terminal windows or tabs.
In one terminal, run the receiver script: ./receiver.sh.
In the other terminal, run the sender script: ./sender.sh.
Enter messages in the sender terminal, and they should be received and displayed by the receiver.



54. Implement echo server using UDP in iterative/concurrent logic.

Client
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 8080
#define MAXLINE 1024

int main() {
    int sockfd;
    char buffer[MAXLINE];
    struct sockaddr_in servaddr;

    // Creating socket file descriptor
    if ((sockfd = socket(AF_INET, SOCK_DGRAM, 0)) < 0) {
        perror("socket creation failed");
        exit(EXIT_FAILURE);
    }

    memset(&servaddr, 0, sizeof(servaddr));

    // Filling server information
    servaddr.sin_family = AF_INET;
    servaddr.sin_port = htons(PORT);
    servaddr.sin_addr.s_addr = INADDR_ANY;

    int n, len;

    while (1) {
        printf("Enter message: ");
        fgets(buffer, MAXLINE, stdin);
        sendto(sockfd, (const char *)buffer, strlen(buffer), MSG_CONFIRM, (const struct sockaddr *)&servaddr, sizeof(servaddr));
        n = recvfrom(sockfd, (char *)buffer, MAXLINE, MSG_WAITALL, (struct sockaddr *)&servaddr, &len);
        buffer[n] = '\0';
        printf("Server : %s\n", buffer);
    }

    close(sockfd);
    return 0;
}



Server
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 8080
#define MAXLINE 1024

int main() {
    int sockfd;
    char buffer[MAXLINE];
    struct sockaddr_in servaddr, cliaddr;

    // Creating socket file descriptor
    if ((sockfd = socket(AF_INET, SOCK_DGRAM, 0)) < 0) {
        perror("socket creation failed");
        exit(EXIT_FAILURE);
    }

    memset(&servaddr, 0, sizeof(servaddr));
    memset(&cliaddr, 0, sizeof(cliaddr));

    // Filling server information
    servaddr.sin_family = AF_INET; // IPv4
    servaddr.sin_addr.s_addr = INADDR_ANY;
    servaddr.sin_port = htons(PORT);

    // Bind the socket with the server address
    if (bind(sockfd, (const struct sockaddr *)&servaddr, sizeof(servaddr)) < 0) {
        perror("bind failed");
        exit(EXIT_FAILURE);
    }

    printf("Server is listening on port %d\n", PORT);

    int len, n;
    len = sizeof(cliaddr);  //len is value/resuslt

    while (1) {
        n = recvfrom(sockfd, (char *)buffer, MAXLINE, MSG_WAITALL, (struct sockaddr *)&cliaddr, &len);
        buffer[n] = '\0';
        printf("Client : %s\n", buffer);
        sendto(sockfd, (const char *)buffer, strlen(buffer), MSG_CONFIRM, (const struct sockaddr *)&cliaddr, len);
    }

    return 0;
}


write prog using FIFO/mknod (named pipe)/unmanned pipe for uppercase to lowercase to
conversion

#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <ctype.h>

int main() {
    int pipefd[2]; // File descriptors for the pipe
    int nbytes; // Number of bytes read from the pipe
    pid_t pid;
    char readbuffer[80]; // Buffer to read data from the pipe

    // Create the pipe
    if (pipe(pipefd) == -1) {
        perror("pipe");
        exit(EXIT_FAILURE);
    }

    // Fork a child process
    pid = fork();

    if (pid < 0) { // Error occurred
        perror("fork");
        exit(EXIT_FAILURE);
    }

    if (pid > 0) { // Parent process
        close(pipefd[0]); // Close the read end of the pipe

        // Write data to the pipe
        printf("Enter text: ");
        fgets(readbuffer, sizeof(readbuffer), stdin);
        write(pipefd[1], readbuffer, sizeof(readbuffer));
        close(pipefd[1]); // Close the write end of the pipe
    } 
    else { // Child process
        close(pipefd[1]); // Close the write end of the pipe
        nbytes = read(pipefd[0], readbuffer, sizeof(readbuffer)); // Read data from the pipe

        for (int i = 0; i < nbytes; i++) {
            readbuffer[i] = tolower(readbuffer[i]); // Convert to lowercase
        }

        printf("Lowercase text: %s", readbuffer);
        close(pipefd[0]); // Close the read end of the pipe
    }

    return 0;
}



Using FIFO as named pipe use read and write system calls to establish communication
(IPC) between two ends.
// using fifo as named pipe use read and write system calls to establish communication (IPC) between two ends

64a.c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>

#define FIFO_NAME "/tmp/my_fifo"

int main() {
    int fifo_fd;

    // Create FIFO
    if (mkfifo(FIFO_NAME, 0666) == -1) {
        perror("mkfifo");
        exit(EXIT_FAILURE);
    }

    printf("FIFO created successfully\n");

    // Open FIFO for writing
    fifo_fd = open(FIFO_NAME, O_WRONLY);
    if (fifo_fd == -1) {
        perror("open");
        exit(EXIT_FAILURE);
    }

    printf("FIFO opened for writing\n");

    // Write data to FIFO
    const char *message = "Hello from Writer";
    if (write(fifo_fd, message, sizeof(message)) == -1) {
        perror("write");
        exit(EXIT_FAILURE);
    }

    printf("Data written to FIFO\n");

    // Close FIFO
    close(fifo_fd);

    return 0;
}

64.b
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>

#define FIFO_NAME "/tmp/my_fifo"

int main() {
    int fifo_fd;
    char buf[256];

    // Open FIFO for reading
    fifo_fd = open(FIFO_NAME, O_RDONLY);
    if (fifo_fd == -1) {
        perror("open");
        exit(EXIT_FAILURE);
    }

    printf("FIFO opened for reading\n");

    // Read data from FIFO
    ssize_t num_bytes = read(fifo_fd, buf, sizeof(buf));
    if (num_bytes == -1) {
        perror("read");
        exit(EXIT_FAILURE);
    }

    // Null-terminate the received data
    buf[num_bytes] = '\0';

    printf("Received message: %s\n", buf);

    // Close FIFO
    close(fifo_fd);

    return 0;
}

modified:
reader:
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/stat.h>
#include <sys/types.h>

#define FIFO_NAME "/tmp/myfifo"
#define BUFFER_SIZE 256

int main() {
    int fd;
    char buffer[BUFFER_SIZE];
    
    // Open FIFO for reading
    fd = open(FIFO_NAME, O_RDONLY);
    
    while (1) {
        // Read from FIFO
        read(fd, buffer, BUFFER_SIZE);
        printf("Received message: %s\n", buffer);
    }

    // Close FIFO
    close(fd);
    
    // Remove FIFO
    unlink(FIFO_NAME);
    
    return 0;
}

writer:
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <string.h>

#define FIFO_NAME "/tmp/myfifo"
#define BUFFER_SIZE 256

int main() {
    int fd;
    char message[BUFFER_SIZE];
    
    // Create FIFO (named pipe)
    mkfifo(FIFO_NAME, 0666);

    // Open FIFO for writing
    fd = open(FIFO_NAME, O_WRONLY);
    
    while (1) {
        // Get message from user
        printf("Enter message: ");
        fgets(message, BUFFER_SIZE, stdin);
        
        // Write message to FIFO
        write(fd, message, strlen(message) + 1);
    }

    // Close FIFO
    close(fd);
    
    return 0;
}


ftp:
shell script to auto create ftp server
#!/bin/bash

# Update package index
sudo apt update

# Install vsftpd
sudo apt install -y vsftpd

# Prompt user for server ID
read -p "Enter server ID (default: myftpserver): " server_id

# Set default server ID if not provided
if [ -z "$server_id" ]; then
    server_id="myftpserver"
fi

# Configure vsftpd
sudo sed -i "s/#listen_ipv6=YES/listen_ipv6=NO/" /etc/vsftpd.conf
sudo sed -i "s/anonymous_enable=NO/anonymous_enable=YES/" /etc/vsftpd.conf
sudo sed -i "s/#local_enable=YES/local_enable=YES/" /etc/vsftpd.conf
sudo sed -i "s/#write_enable=YES/write_enable=YES/" /etc/vsftpd.conf
sudo sed -i "s/#anon_upload_enable=YES/anon_upload_enable=YES/" /etc/vsftpd.conf
sudo sed -i "s/#chroot_local_user=YES/chroot_local_user=YES/" /etc/vsftpd.conf
sudo sed -i "s/#chroot_list_enable=YES/chroot_list_enable=YES/" /etc/vsftpd.conf
sudo sed -i "s/#chroot_list_file=\/etc\/vsftpd.chroot_list/chroot_list_file=\/etc\/vsftpd.chroot_list/" /etc/vsftpd.conf
sudo sed -i "s/#local_umask=022/local_umask=022/" /etc/vsftpd.conf
sudo sed -i "s/#idle_session_timeout=600/idle_session_timeout=600/" /etc/vsftpd.conf
sudo sed -i "s/#data_connection_timeout=300/data_connection_timeout=300/" /etc/vsftpd.conf
sudo sed -i "s/#ftpd_banner=Welcome to blah FTP service./ftpd_banner=Welcome to $server_id FTP service./" /etc/vsftpd.conf

# Restart vsftpd service
sudo systemctl restart vsftpd

echo "FTP server setup complete."
















