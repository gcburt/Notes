## Task


### Task
```swift
struct functionOrderExampleView: View {
    let functions = Functions()
    
    var body: some View {
        Button("start") {
            functions.one()
            Task {
                functions.two()
            }
            functions.three()
        }
    }
}

@MainActor
struct Functions {
    func one() {}
    func two() {}
    func three() {}
}
```
> Tasks schedule work. In this scenario, all of the functions run on the main actor. In order of occurance:
- 1
- Task is scheduled
- 3
- 2


### Race conditions
```swift
struct functionOrderExampleView: View {
    let functions = Functions()
    
    var body: some View {
        Button("start") {
            Task {
                functions.one()
            }
            Task {
                functions.two()
            }
            functions.three()
        }
    }
}

@MainActor
struct Functions {
    func one() {}
    func two() {}
    func three() {}
}
```
> This time there is a race condition created between 1 and 2. They race to _start_, not to complete. Only one can run on the main actor at a time.
- 3
- 1 or 2
- 1 or 2

### Await
```swift
struct functionOrderExampleView: View {
    let functions = Functions()
    
    var body: some View {
        Button("start") {
            functions.one()
            Task {
                functions.two()
            }
            await functions.three()
            functions.four()
        }
    }
}

@MainActor
struct Functions {
    func one() {}
    func two() {}
    func three() async {}
    func four() {}
}
```
> Now an await is included. Awaits allow the function to suspend at that point. It cannot skip it.
- 1
- Task is scheduled
- 3 provides option to suspend the Button. It is not required.
- At this point task has been scheduled and 3 is allowed to pause. The main actor has its choice
- 2 or 3
- 2 or 3
- 4

