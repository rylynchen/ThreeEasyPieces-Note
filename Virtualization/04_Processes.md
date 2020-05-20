# Process
* Process API
    * Create
        * load **code** / **static data** to memory
        * allocate **stack** (local variables, function parameters)
        * allocate **heap** (dynamically-allocated)
        * open three **file descriptors** (std input, output and error)
    * Destroy
    * Wait
    * Miscellaneous Control
    * Status
    
* Process States
    * Running
    * Ready
    * Blocked
    
* Data Structures
```
struct context {
  int eip;
  int esp;
  int ebx;
  int ecx;
  int edx;
  int esi;
  int edi;
  int ebp;
};

// the different states a process can be in
enum proc_state { 
    UNUSED, 
    EMBRYO, 
    SLEEPING, 
    RUNNABLE, 
    RUNNING, 
    ZOMBIE
};

struct proc {
    char *mem;  // Start of process memory
    uint sz;    // Size of process memory
    char *kstack;   // Bottom of kernel stack
    enum proc_state state;  // Process state
    int pid;    // Process ID
    struct proc *parent; // Parent process
    void *chan; // If !zero, sleeping on chan
    int killed; // If !zero, has been killed
    struct file *ofile[NOFILE]; // Open files
    struct inode *cwd; // Current directory
    struct context context; // Switch here to run process
    struct trapframe *tf;
}
```