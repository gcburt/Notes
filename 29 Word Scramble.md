## Lists
> Lists make, well... lists. 
```swift
struct ContentView: View {
    var body: some View {
        List {
            Text("One")
            Text("Two")
            Text("Three")
            
            ForEach(0...5, id: \.self) {
                Text("\($0)")
            }
        }
        .listStyle(.grouped)
    }
}
```
1. `.listStyle()` has a bunch of modifiers. They're subtle.
   
<img width="150" height="355" alt="Screenshot 2025-07-15 at 3 21 24 PM" src="https://github.com/user-attachments/assets/771e28c8-554d-4704-b618-e23b8d9a3dd7" />

```swift
struct ContentView: View {
    var body: some View {
        List(1...5, id: \.self) {
            Text("Test box")
            
            Text("\($0)")
        }
    }
}
```
> Unlike Form, Lists can create their own lines without ForEach. This also works on arrays.
<img width="150" height="355" alt="Screenshot 2025-07-15 at 3 27 47 PM" src="https://github.com/user-attachments/assets/144411f1-de1a-447d-bffd-b6beb1f86321" />

## Loading files from a bundle

```swift
struct ContentView: View {
    var body: some View {}
    
    func testBundle() {
        if let fileURL = Bundle.main.url(forResource: "somefile", withExtension: "txt") {
            if let fileContents = try? String(contentsOf: fileURL, encoding: .utf8) {
                // we loaded the file into a String
            }
        }
    }
}
```
> Comparable to loading images from the assets file.
> When I make an app, all the files are stored inside a folder called a bundle. I don't know why yet, but sometimes there will be multiple bundles for a single app. Here I am attempting to load a .txt file from my *main* bundle.

`if let fileURL = Bundle.main.url(forResource: "somefile", withExtension: "txt")`
> First, i'm using `if let` to assign fileURL to a URL. It's located in Bundle.main. It's a .url named `somefile.txt`.

`if let fileContents = try? String(contentsOf: fileURL, encoding: .utf8) {`
> If I find the document, I'll look inside with `if let` again to assign the new fileContents constant to a very very **very** long string. 

```swift
func testStrings() {
    let word = "example"
    let checker = UITextChecker()
    
    let range = NSRange(location: 0, length: word.utf16.count)
    let mispelledRange = checker.rangeOfMisspelledWord(in: word, range: range, startingAt: 0, wrap: false, language: "en")
    
    let correctSpelling = mispelledRange.location == NSNotFound
}
```

1. word is the test example.
2. checker imports a text checker from the UI and initializes it.
3. range converts the Swift string into an Objective-C string. .utf16 is the old format
4. mispelled range (in: "The checked word", range: "The objective-C word we made", startingAt: "the first word", wrap: "Do we want to go back to the beginning?", languege: "English"
5. correctSpelling checks if objective-C found a mispelled word.

```swift
func testStrings() {
    let input = "a b c"
    let letters = input.components(separatedBy: " ") // "\n" does new line
    let letter = letters.randomElement()
}
```

> the components(separatedBy: " ") command identifies the components in the string


```swift
struct ContentView: View {
    @State private var usedWords: [String] = []
    @State private var rootWord: String = ""
    @State private var newWord: String = ""
    
    var body: some View {
        NavigationStack {
            List {
                Section {
                    TextField("Enter your word", text: $newWord)
                        .textInputAutocapitalization(.never)
//                    Button("OK", action: addNewWord)
                }
                
                Section {
                    ForEach(usedWords, id: \.self) { word in
                        Text(word)
                    }
                }
            }
            .navigationTitle(rootWord)
            .onSubmit(addNewWord)
        }
    }
    
    func addNewWord() {
        let formattedWord = newWord.lowercased().trimmingCharacters(in: .whitespacesAndNewlines)
        guard formattedWord.count > 0 else { return }
        withAnimation {
            usedWords.insert(formattedWord, at: 0)
        }
        newWord = ""
    }
}
```
1. `.textInputAutocapitalization(.never)` disables auto capitiliazation
2. `.onSubmit(addNewWord)` makes enter run the code
3. `.insert(formattedWord, at: 0)` puts the word at the beginning of the array, compared to append, whick puts it at the back.
4. `.trimmingCharacters(in: .whitespacesAndNewlines)` removes whitespaces and lines

```
   import SwiftUI

struct ContentView: View {
    @State private var usedWords: [String] = []
    @State private var rootWord: String = ""
    @State private var newWord: String = ""
    
    var body: some View {
        NavigationStack {
            List {
                Section {
                    TextField("Enter your word", text: $newWord)
                        .textInputAutocapitalization(.never)
//                    Button("OK", action: addNewWord)
                }
                
                Section {
                    ForEach(usedWords, id: \.self) { word in
                        Text(word)
                    }
                }
            }
            .navigationTitle(rootWord)
            .onSubmit(addNewWord)
            .onAppear(perform: newGame)
        }
    }
    
    func addNewWord() {
        let formattedWord = newWord.lowercased().trimmingCharacters(in: .whitespacesAndNewlines)
        guard formattedWord.count > 0 else { return }
        withAnimation {
            usedWords.insert(formattedWord, at: 0)
        }
        newWord = ""
    }
    
    func newGame() {
        if let startWordsURL = Bundle.main.url(forResource: "start", withExtension: "txt") {
            if let startWords = try? String(contentsOf: startWordsURL, encoding: .utf8) {
                let allWords = startWords.components(separatedBy: "\n")
                rootWord = allWords.randomElement() ?? "silkworm"
                return
            }
        }
        
        fatalError("start.txt loading error")
    }
    
    func isOriginal(_ word: String) -> Bool {
        !usedWords.contains(word)
    }
    
    func containsSameLetters(_ word: String) -> Bool {
        var tempWord = rootWord
        var letterArray: [Character] = Array(word)
        var letterArrayRoot: [Character] = Array(tempWord)
        
        
        for letter in letterArray {
            if let index = letterArrayRoot.firstIndex(of: letter) {
                letterArrayRoot.remove(at: index)
            } else {
                return false
            }
        }
        
        return true
    }
}
```
half ass code
