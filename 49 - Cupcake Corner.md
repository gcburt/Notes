## Loading data with URLSession

```swift
truct Response: Codable {
    var response: [Result]
}

struct Result: Codable {
    var trackId: Int
    var trackName: String
    var collectionName: String
}

struct ContentView: View {
    
    @State private var results = [Result]()
    
    var body: some View {
        List(results, id: \.trackId) { item in
            VStack(alignment: .leading) {
                Text(item.trackName)
                    .font(.headline)
                
                Text(item.collectionName)
            }
        }
        .task {
            await loadData()
        }
    }
    
    func loadData() async {
        guard let url = URL(string: "https://itunes.apple.com/search?term=taylor+swift&entity=song") else { print("Invalid URL")
            return
        }
        
        do {
            let (data, _) = try await URLSession.shared.data(from: url)
            
            if let decodedResponse = try? JSONDecoder().decode(Response.self, from: data) { // .decode is a generic function that needs a type. .self references Response as the type and satisfies that.
                results = decodedResponse.results
            }
        } catch {
            print("Invalid data")
        }
    }
}
```

<img height="300" alt="Screenshot 2025-09-09 at 10 23 27 AM" src="https://github.com/user-attachments/assets/6d65804b-a818-4121-97e5-3ceab2fadb7f" />
