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


