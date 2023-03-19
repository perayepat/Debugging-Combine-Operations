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


