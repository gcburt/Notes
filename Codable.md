## Codable, Decodable and Encodable

```swift
struct Profile: Decodable {
  let username: String?
  let fullName: String?
  let website: String?

  enum CodingKeys: String, CodingKey {
    case username
    case fullName = "full_name"
    case website
  }
} 

struct UpdateProfileParams: Encodable {
  let username: String
  let fullName: String
  let website: String

  enum CodingKeys: String, CodingKey {
    case username
    case fullName = "full_name"
    case website
  }
}
```

> I have a JSON back end. These two structs conform to the encodable and decodable protocols. Profile reads the JSON data, and UpdateProfileParams writes JSON data. This could easily be handled by a single Codable structure.

#### Encodable

>  Really good for analitics. I'll use it for user behavior data. ie. last active session timestamp

#### Decodable

>  For when the app just needs to read something. ie. Welcome message

#### Coding Key

> Required. Literally just a key. Notice the snake_case = fullName 

```swift
struct User: Codable {
    let firstName: String
    let lastName: String
}

struct ContentView: View {
    @State private var user = User(firstName: "Taylor", lastName: "Burton")
    
    var body: some View {
        Button("Save user") {
            let encoder = JSONEncoder()
            
            if let data = try? encoder.encode(user) {
                UserDefaults.standard.set(data, forKey: "UserData")
            }
        }
    }
}
```

> This encodes our instance of user into a JavaScript Object Notation, JSON, file.
