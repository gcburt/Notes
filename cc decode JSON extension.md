```swift
extension Bundle {
    func decode(_ file: String) -> [String: Astronaut] {
        guard let URL = self.url(forResource: file, withExtension: nil) else { fatalError("Failed to find \(file)")
        }
        
        guard let data = try? Data(contentsOf: URL) else {
            fatalError("Failed to load \(file)")
        }
        
        let decoder = JSONDecoder()
        
        do {
            return try decoder.decode([String: Astronaut].self, from: data)
        } catch DecodingError.keyNotFound(let key, let context) {
            fatalError("Failed to decode \(file) from bundle due to missing key '\(key.stringValue)' – \(context.debugDescription)")
        } catch DecodingError.typeMismatch(_, let context) {
            fatalError("Failed to decode \(file) from bundle due to type mismatch – \(context.debugDescription)")
        } catch DecodingError.valueNotFound(let type, let context) {
            fatalError("Failed to decode \(file) from bundle due to missing \(type) value – \(context.debugDescription)")
        } catch DecodingError.dataCorrupted(_) {
            fatalError("Failed to decode \(file) from bundle because it appears to be invalid JSON.")
        } catch {
            fatalError("Failed to decode \(file) from bundle: \(error.localizedDescription)")
        }
    }
}
```

to call it

``` swift
let astronauts = Bundle.main.decode("astronauts.json")
```

i can make it generic

```swift
extension Bundle {
    func decode<T: Codable>(_ file: String) -> T {
        guard let URL = self.url(forResource: file, withExtension: nil) else { fatalError("Failed to find \(file)")
        }
        
        guard let data = try? Data(contentsOf: URL) else {
            fatalError("Failed to load \(file)")
        }
        
        let decoder = JSONDecoder()
        
        do {
            return try decoder.decode(T.self, from: data)
        } catch DecodingError.keyNotFound(let key, let context) {
            fatalError("Failed to decode \(file) from bundle due to missing key '\(key.stringValue)' – \(context.debugDescription)")
        } catch DecodingError.typeMismatch(_, let context) {
            fatalError("Failed to decode \(file) from bundle due to type mismatch – \(context.debugDescription)")
        } catch DecodingError.valueNotFound(let type, let context) {
            fatalError("Failed to decode \(file) from bundle due to missing \(type) value – \(context.debugDescription)")
        } catch DecodingError.dataCorrupted(_) {
            fatalError("Failed to decode \(file) from bundle because it appears to be invalid JSON.")
        } catch {
            fatalError("Failed to decode \(file) from bundle: \(error.localizedDescription)")
        }
    }
}
```

and call it too

```swift
let missions: [Mission] = Bundle.main.decode("missions.json")
```
