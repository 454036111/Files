<p align="center">
    <img src="logo.png" width="300" max-width="50%" alt=“Files” />
</p>

Welcome to **Files**, a compact library that provides a nicer way to handle *files* and *folders*  in Swift. It’s primarily aimed at Swift scripting and tooling, but can also be embedded in applications that need to access the file system. It's essentially a thin wrapper around the `FileManager` APIs that `Foundation` provides.

### Features

- [X] Modern, object-oriented API for accessing, reading and writing files & folders.
- [X] Unified, simple `do, try, catch` error handling.
- [X] Easily construct recursive and flat sequences of files and folders.

### Examples

Iterate over the files contained in a folder:
```swift
for file in try Folder(path: "MyFolder").files {
    print(file.name)
}
```

Rename all files contained in a folder:
```swift
try Folder(path: "MyFolder").files.enumerated().forEach { (index, file) in
    try file.rename(to: file.nameWithoutExtension + "\(index)")
}
```

Recursively iterate over all folders in a tree:
```swift
FileSystem().homeFolder.makeSubfolderSequence(recursive: true).forEach { file in
    print("Name : \(file.name), parent: \(file.parent)")
}
```

Create, write and delete files and folders:
```swift
let folder = try Folder(path: "/users/john/folder")
let file = try folder.createFile(named: "file.json")
try file.write(data: wrap(object))
try file.delete()
try folder.delete()
```

Move all files in a folder to another:
```swift
let originFolder = try Folder(path: "/users/john/folderA")
let targetFolder = try Folder(path: "/users/john/folderB")
try originFolder.files.move(to: targetFolder)
```
