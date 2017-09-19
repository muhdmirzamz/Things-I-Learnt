## Networking

- Completion handlers are usually used in async API calls. They are closures and what closures are is, they are functions that take a function as an argument.
Example:
``` swift
func fetchData(completion: @escaping (_ json: [String: Any]) -> Void) {
	let dataTask = URLSession.shared.dataTask(with: self.url!) { (data, response, error) in
		let json = try? JSONSerialization.jsonObject(with: data!, options: .allowFragments) as? [String: Any]

		completion(json!!)
	}
		
	dataTask.resume()
}
```
Note: `@escaping` keyword [explanation](https://stackoverflow.com/a/38990967)

This completion handler takes in a dictionary as an argument, most often for use as a JSON. In async calls, once you have the data, you can pass the data through the completion handler arguments. That way, when you call the main function, you can make use of the data that was passed through the completion handler.

You can then use the json as follows
``` swift
let database = Database()
database.fetchData { (json) in
  print(json)
}
```
references: [Completion handlers in Swift](https://thatthinginswift.com/completion-handlers/)
