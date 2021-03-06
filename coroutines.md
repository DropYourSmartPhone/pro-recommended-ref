--- understanding kotlin coroutines
key-conceptions: [builder, scope, context, dispatcher]
key-words: 
- CoroutineScope.launch(): Launches a new coroutine without blocking the current thread and returns a reference to the coroutine as a Job. 
- CoroutineScope.async(): Creates a coroutine and returns its future result as an implementation of Deferred. 
- await(): Awaits for completion of this value without blocking a thread and resumes when deferred computation is complete 
- Job: A background job. Conceptually, a job is a cancellable thing with a life-cycle that culminates in its completion.
- Deferred: Deferred value is a non-blocking cancellable future — it is a Job with a result.
- Job.join(): Suspends the coroutine until this job is complete. 
- coroutineScope(): suspend, Creates a CoroutineScope and calls the specified suspend block with this scope. 
- GlobleScope: Global scope is used to launch top-level coroutines which are operating on the whole application lifetime and are not cancelled prematurely.
- withContext(): Calls the specified suspending block with a given coroutine context, suspends until it completes, and returns the result.
- CoroutineContext: An indexed set is a mix between a set and a map. Every element in this set has a unique Key.

comments: 
- launch return a Job, and async return a Deffered. They are different when exceptions.
- withContext(Dispatchers.Main) { }, is suspend
- runBlocking: don't call in a coroutine, but in normal thread, espeically in Main.
- Dispather: how to use threads to execute coroutines
- it's important to know a function is a blocking or unblocking. A blocking is it cannot delay.

vs: 
- launch vs async
- Job vs Deferred
- GlobleScope vs coroutineScope()
- Blocking vs Non-blocking, launch/async are non-blocking, coroutineScope/withContext are blocking

UI_Thread:
- launch(Dispatchers.Main){}
- withContext(Dispatchers.Main) {}
- You can also call deley() inside block, because they are suspend, but they don't block UI thread, just block coroutine.

runBlocking:
- Runs a new coroutine and blocks the current thread interruptibly until its completion. 
- This function should not be used from a coroutine. 
- It is designed to bridge regular blocking code to libraries that are written in suspending style, to be used in main functions and in tests.
- If there is a launch inside, the runBlocking will not return until the launch finish.
