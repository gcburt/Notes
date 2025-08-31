# Navigation

## .navigationDestination and path

```swift
struct ContentView: View {
    @State private var path = [Int]()
    
    var body: some View {
        NavigationStack(path: $path) {
            VStack {
                Button("Show 32") {
                    path = [32]
                }
                Button("Show 64") {
                    path.append(64)
                }
                Button("Show 32 then 64") {
                    path = [32, 64]
                }
            }
            .navigationDestination(for: Int.self) { selection in
                Text("You selecteed \(selection)")
            }
        }
    }
}
```

> This shows a navigation path.
> 1. First, a path is made. Here it is an empty array of intigers. It can be bound to the `NavigationStack`.
> 2. Second, path is assigned a value. This is simple enough, that it just kinda works everywhere.
> 3. Finally, a `.navigationDestination` is created. 
<img height="300" alt="Screenshot 2025-08-26 at 1 32 37 PM" src="https://github.com/user-attachments/assets/7242c401-cc25-4d8f-ba1b-f53317b60ef3" />
<img height="300" alt="Screenshot 2025-08-26 at 1 32 57 PM" src="https://github.com/user-attachments/assets/2b34cd03-a56a-4518-b40a-fa16f6f2c5a6" />

## NavigationPath

```swift
struct ContentView: View {
    @State private var path = NavigationPath()
    
    var body: some View {
        NavigationStack(path: $path) {
            List {
                ForEach(1..<5) { i in
                    NavigationLink("Select number \(i)", value: i)
                }
                ForEach(1..<5) { i in
                    NavigationLink("Select string \(i)", value: String(i))
                }
            }
            .navigationDestination(for: Int.self) { selection in
                Text("You selected number \(selection)")
            }
            .navigationDestination(for: String.self) { selection in
                Text("You selected string \(selection)")
            }
            .toolbar {
                Button("Push 556") {
                    path.append(556)
                }
            }
        }
    }
}
```

> This is similar to the previous example, but it uses a `NavigationPath` instead. NavigationPath is kinda like an automatic array of multiple type destinations.

<img width="150" alt="Screenshot 2025-08-26 at 1 43 19 PM" src="https://github.com/user-attachments/assets/1b19b5aa-7720-403e-935a-ca5e9aaef964" />


## @Binding

```swift
struct DetailView: View {
    var number: Int
    @Binding var path: NavigationPath
    
    var body: some View {
        NavigationLink("Get new number", value: Int.random(in: 1...100))
            .navigationTitle("\(number)")
            .toolbar {
                Button("\(0)") {
                    path = NavigationPath()
                }
            }
    }
}

struct ContentView: View {
    @State private var path = NavigationPath()
    
    var body: some View {
        NavigationStack(path: $path) {
             DetailView(number: 0, path: $path)
                .navigationDestination(for: Int.self) { i in
                    DetailView(number: i, path: $path)
                }
        }
    }
}
```
> This example uses two structs. DetailView creates a new random number every time the button is pressed. The toolbar button returns us back to the root view of 0.

<img height="300" alt="Screenshot 2025-08-26 at 1 44 01 PM" src="https://github.com/user-attachments/assets/eb6c02ea-4b6b-45a1-ba9d-3864d7bd858c" />
<img height="300" alt="Screenshot 2025-08-26 at 1 44 18 PM" src="https://github.com/user-attachments/assets/a76506a8-b177-47c2-b51a-2a22afc905a4" />

## Save paths using Codable

```swift
@Observable
class PathStore {
    var path: [Int] {
        didSet {
            save()
        }
    }
    
    private let savePath = URL.documentsDirectory.appending(path: "SavedPath")
    
    init() {
        if let data = try? Data(contentsOf: savePath) {
            if let decoded = try? JSONDecoder().decode([Int].self, from: data) {
                path = decoded
                return
            }
        }
        
        path = []
    }
    
    func save() {
        do {
            let data = try JSONEncoder().encode(path)
            try data.write(to: savePath)
        } catch {
            print("Failed to save navigation data")
        }
    }
}

struct ContentView: View {
    @State private var pathStore = PathStore()
    
    var body: some View {
        NavigationStack(path: $path) {
            DetailView(number: 0)
                .navigationDestination(for: Int.self) { i in
                    DetailView(number: i)
                }
        }
    }
}

struct DetailView: View {
    var number: Int
    
    var body: some View {
        NavigationLink("Go to random number", value: Int.random(in: 1...100))
            .navigationTitle("Number: \(number)")
    }
}
```

> Uses an [Int] array to store a path. It's mostly cut and paste

### *or*

```swift
@Observable
class PathStore {
    var path: NavigationPath { // 1
        didSet {
            save()
        }
    }
    
    private let savePath = URL.documentsDirectory.appending(path: "SavedPath")
    
    init() {
        if let data = try? Data(contentsOf: savePath) {
            if let decoded = try? JSONDecoder().decode(NavigationPath.CodableRepresentation.self, from: data) { // 2
                path = NavigationPath(decoded) // 3
                return
            }
        }
        
        path = NavigationPath()
    }
    
    func save() {
        guard let representation = path.codable else { return } // 4
        
        do {
            let data = try JSONEncoder().encode(representation) // 5
            try data.write(to: savePath)
        } catch {
            print("Failed to save navigation data")
        }
    }
}

struct ContentView: View {
    @State private var pathStore = PathStore()
    
    var body: some View {
        NavigationStack(path: $pathStore.path) {
            DetailView(number: 0)
                .navigationDestination(for: Int.self) { i in
                    DetailView(number: i)
                }
        }
    }
}

struct DetailView: View {
    var number: Int
    
    var body: some View {
        NavigationLink("Go to random number", value: Int.random(in: 1...100))
            .navigationTitle("Number: \(number)")
    }
}
```

> If you use a NavigationPath instead, you need to make a few changes. They're labeled. Just cut and paste.

## Color or hide the toolbar

```swift
struct ContentView: View {
    var body: some View {
        NavigationStack {
            List(0..<100) { i in
                Text("\(i)")
            }
            .navigationTitle("Title")
            .navigationBarTitleDisplayMode(.inline)
            .toolbarBackground(.blue)
            .toolbarColorScheme(.dark)
        }
    }
}
```

> This looks like shit.

<img height="300" alt="Screenshot 2025-08-29 at 3 10 39 PM" src="https://github.com/user-attachments/assets/906419d5-a867-46fc-bccc-b0f0bb97856b" />
<img height="300" alt="Screenshot 2025-08-29 at 3 10 45 PM" src="https://github.com/user-attachments/assets/f60b6bcd-36ee-43c9-928e-f221e6617f94" />

```swift
struct ContentView: View {
    var body: some View {
        NavigationStack {
            List(0..<100) { i in
                Text("\(i)")
            }
            .navigationTitle("Title")
            .navigationBarTitleDisplayMode(.inline)
            .toolbar(.hidden, for: .navigationBar)
        }
    }
}
```
> Not much better. I've seen a fade out. That's probably where we'll go.

<img width="150" alt="Screenshot 2025-08-29 at 3 15 14 PM" src="https://github.com/user-attachments/assets/6eda89c7-d44f-4039-871e-8ce75d8ae277" />

## Moving toolbar buttons

```swift
struct ContentView: View {
    var body: some View {
        NavigationStack {
            Text("Hello")
                .toolbar {
                    ToolbarItem(placement: .topBarLeading) {
                        Button("Tap Me") {}
                    }
                }
                .navigationBarBackButtonHidden()
        }
    }
}
```

> I can move around the toolbar button. Some of the options are literal places, but others are contextual.
> .navigationBarBackButtonHidden() is a dead button right now, but can be used to hde the back button based on logic.

<img width="448" height="301" alt="Screenshot 2025-08-29 at 3 20 07 PM" src="https://github.com/user-attachments/assets/73c72571-6ae6-42d5-afbc-c53d9ee5cf72" />
<img height="300" alt="Screenshot 2025-08-29 at 3 19 42 PM" src="https://github.com/user-attachments/assets/8e223bf4-e825-4392-8051-870285e5b0ce" />


## Editing the navbar title

```swift
struct ContentView: View {
    @State private var title = "SwiftUI"

    var body: some View {
        NavigationStack {
            Text("Hello, world!")
                .navigationTitle($title)
                .navigationBarTitleDisplayMode(.inline)
        }
    }
}
```

> This may come in handy?

<img width="150" alt="Screenshot 2025-08-29 at 3 24 25 PM" src="https://github.com/user-attachments/assets/11fc32b9-f56b-40db-b2fa-4731b16d06d4" />

