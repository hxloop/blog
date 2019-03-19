>An initializer in `String` class `String(5, radix: 2)` creates a string which is a binary representation of 5 as : `101` 
But it will not give a padded version (for obvious and good reasons) like `00000101` or `00000000 00000101` which may be desirable in some cases

#### Here are two approaches of achieving this :

## 1.

```swift 
extension String {
    static func binaryRepresentation<F: FixedWidthInteger>(of val: F) -> String {
        let binaryString = String(val, radix: 2)
        if val.leadingZeroBitCount > 0 {
            return String(repeating: "0", count: val.leadingZeroBitCount) + binaryString
        }
        return binaryString
    }
}

// Usage
let five = UInt8(5) // 101
print(String.binaryRepresentation(of: UInt8(5))) //prints 00000101
```
## 2 
> By: [Karwag @ SO][kw]
```swift
extension String {
  init<B: FixedWidthInteger>(fullBinary value: B) {
    self = value.words.reduce(into: "") {
      $0.append(contentsOf: repeatElement("0", count: $1.leadingZeroBitCount))
      $0.append(String($1, radix: 2))
    }
  }
}
```

[kw]: <https://stackoverflow.com/a/47874469/751026>
