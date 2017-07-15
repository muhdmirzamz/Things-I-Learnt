## Networking

- Completion handlers are usually used in async API calls. They are closures and what closures are is, they are functions that take a function as an argument.
Example:
``` swift
func fetchData(completion: @escaping () -> [String: Any]) {

}
```
This completion handler return a dictionary, most often for use as a JSON. In async calls, once you have the data, you can pass the data through the completion handler arguments. That way, when you call the main function, you can make use of the data that was passed through the completion handler.
