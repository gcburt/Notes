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

## PhotosPicker array

```swift
struct ContentView: View {
    @State private var pickerItems = [PhotosPickerItem]()
    @State private var selectedImages = [Image]()
    
    var body: some View {
        VStack {
            PhotosPicker("Select a picture", selection: $pickerItems, maxSelectionCount: 5, matching: .images) // leave out matching to accept eveything
            ScrollView {
                ForEach(0..<selectedImages.count, id: \.self) { i in
                        selectedImages[i]
                        .resizable()
                        .scaledToFit()
                }
            }
        }
        .onChange(of: pickerItems) {
            Task {
                selectedImages.removeAll()
                
                for item in pickerItems {
                    if let loadedImage = try await item.loadTransferable(type: Image.self) {
                        selectedImages.append(loadedImage)
                    }
                }
            }
        }
    }
}
```

<img height="300" alt="Screenshot 2025-10-02 at 6 07 30 PM" src="https://github.com/user-attachments/assets/eecbcc3d-c28c-4138-b0f2-615eb232ec46" />

> Incorporates a few things.
> - `maxSelectionCount` Memory heavy task.
> - Some type of loop for displaying
> - The task requires a clean slate and then just loads one by one.
