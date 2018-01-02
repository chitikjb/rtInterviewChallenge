## High level approach
A quick read through the problem statement convinced me to use a well evolved object oriented language for coding the solution. I picked c# because of my comfort level with the language by working on it through the years. Used Microsoft visual studio code for Mac as an IDE. It's a good lightweight IDE for developing/debugging in a lot of different langauges and has a good open source community support that shows in the number of plugins being developed for the tool. Considering we are reading the input from the terminal and formatting the output back to the console, the application is designed as a console application that takes one parameter as described in the problem statement, the path to the input text file.

## Objects

### Driver
---
**Constructors**

| Name  | Description |
| ------------- | ------------- |
| Driver(string)  | Initializes a new Driver object with the given string as the driver name  |

**Properties**

| Name | Description |
| --- | --- |
| DriverName | Gets or Sets the driver name string |
| TotalDistanceDriven | Gets or Sets the total distance driven by the driver |
| AvgSpeed | Gets or Sets the avg speed of the driver based on his trip history |
| Trips | Gets or Sets the trips associated with the driver |

**Methods**

| Name | Description |
| --- | --- |
| UpdateAverageSpeed() | Updates the average speed of the driver based on the property Trips |
| UpdateTotalDistance() | Updates the total distance driven based on the property Trips |
---
