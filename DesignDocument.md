This is the design document for pthread-lib. You will find the exact specification of what each piece of code was designed.

## 1 Core Design ##
### 1.1 Data Structures ###
**1.1.1** An expandable array of thread pool pointers (THREAD\_POOL). This allows the programmer to create multiple pools of threads

**1.1.2** An expandable array of function pointers. This will function as the queue that work will be submitted to. This should be able to be assigned to any pool or every pool. For example, pool A gets function pointers from queue 1 and queue 2 while pool B gets function pointers from queue 2 only. This and any configuration should be possible.

**1.1.3** A THREAD\_POOL struct that contains a core\_pool\_size, max\_pool\_size, keep\_alive\_time, curr\_pool\_size,

**1.1.4** A THREAD\_POOL\_STATE struct that consists of RUNNING=0, SHUTDOWN=1, STOP=2, TERMINATED=3

**1.1.5** A THREAD struct that contains various information about a thread.

**1.1.5.1** **TODO: what data should be in the THREAD struct?**


### 1.2 Methods ###
#### public methods ####
**1.2.1** submit(function\_pointer) - submits the function pointer to be executed

**1.2.2** submit(function\_pointer, queue)

**1.2.3** submit(function\_pointer, pool)

**1.2.4** awaitTermination(long timeOut) - wait for the pools to terminate

**1.2.5** purge() - remove all the data in the queue

**1.2.6** shutdown()

#### private methods ####
**1.2.?** addThread - adds a thread to the pool up to max\_pool\_size if demand is high

**1.2.?** poll - waits to get a task from the assigned queues (must have alg. for checking multiple queues

**1.2.?** take - takes the function pointer off the queue and executes it (must have mutex)


## 2 Thread Manager ##
**2.1** beginManaging()

**2.2** stopManaging()

**2.3** checkThreads()

**2.4** stopThreadPool()

## 3 Signal Handler ##
**3.1** int signal\_handler\_create(FUNCTION\_PTRS **function\_ptrs)**

**3.2** void stop\_signal\_manager()

**3.3** void destroy\_signal\_manager()

**3.4** void _**signal\_handler\_function(void**functions)_

**3.5** int block\_all\_signals()



## 4 Wrapper Functions ##







