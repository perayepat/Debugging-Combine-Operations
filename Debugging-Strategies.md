# Basic debugging tactics 

Using the basic print on sink and the print operator to see what's happening when we recieve our values from the publisher 

``` swift
let publisher = (1...20).publisher

//MARK: - Debuggin using print
publisher.sink { print($0)}

//MARK: - Print Operator
/// see the operations going on in the background
/// and events happening
publisher
    .print("Debuggin")
    .sink{print($0)}
```

## Using Handle Events operator 
this gives you of how the operations are handled step by step and allows you to set print statements or more UI indicators to show what happens every step of the way

``` swift

//MARK: - Debuggin failed network operations

guard let url = URL(string: "https://jsonplaceholder.typicode.com/posts") else {
    fatalError("Invalid URL")
}

let request = URLSession.shared.dataTaskPublisher(for: url)

let subscription = request
    .handleEvents(
        receiveSubscription: {_ in print("subscription recieved")},
        receiveOutput: {_  in print("recieved Output")},
        receiveCompletion: {_ in print("Recieved Completion")},
        receiveCancel: { print("Recieved Cancel")},
        receiveRequest: {_ in print("Recieved Request")}
    )
    .sink(receiveCompletion: {print($0)}, receiveValue: {data, response in
        print(data)
    })

```
