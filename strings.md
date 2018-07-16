## Strings

Prefixes
``` swift
let index = str.index(str.startIndex, offsetBy: 5)
let mySubstring = str.prefix(upTo: index)
```

Suffixes
``` swift
let index = str.index(str.endIndex, offsetBy: -10)
let mySubstring = str.suffix(from: index)
```

OR you can do this
``` swift
let start = str.index(str.startIndex, offsetBy: 7)
let end = str.index(str.endIndex, offsetBy: -6)
let range = start..<end

let mySubstring = str[range]
```

This [link](https://stackoverflow.com/a/39677331) for more info

