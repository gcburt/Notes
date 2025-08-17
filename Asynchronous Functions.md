- Concurrency: Running multiple tasks on a CPU
- Parallelism: Running multiple tasks on seperate CPU's
- Synchronous: Runs tasks in order on a single thread
- Asynchronous: Has the ability to suspend itself to run other tasks.


```swift
func randomD6() async -> Int {
    Int.random(in: 1...6)
}

let result = await randomD6()
print(result)
```

Similar to `throw` and `try`, async functions use the marking keyword: `async` when creating the function, and `await` when calling it.
