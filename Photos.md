## PhotosPicker

```swift
struct ContentView: View {
    @State private var pickerItem: PhotosPickerItem?
    @State private var selectedImage: Image?
    
    var body: some View {
        VStack {
            PhotosPicker("Select a picture", selection: $pickerItem, matching: .images) // leave out matching to accept eveything
            selectedImage?
                .resizable()
                .scaledToFit()
        }
        .onChange(of: pickerItem) {
            Task {
                selectedImage = try await pickerItem?.loadTransferable(type: Image.self)
            }
        }
    }
}
```
<img height="300" alt="Screenshot 2025-10-02 at 5 54 39 PM" src="https://github.com/user-attachments/assets/1340750b-8eab-493b-83e1-66ade6a2f972" />

> This code makes a photo reference/ image pair of properties. When a photo is chosen, the task assigns the reference to the selectedImage.
