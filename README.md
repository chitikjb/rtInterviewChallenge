# High level approach
A quick read through the problem statement convinced me to use a well evolved object oriented language for coding the solution. I picked c# because of my comfort level with the language by working on it through the years. Used Microsoft visual studio code for Mac as an IDE. It's a good lightweight IDE for developing/debugging in a lot of different langauges and has a good open source community support that shows in the number of plugins being developed for the tool. Considering we are reading the input from the terminal and formatting the output back to the console, the application is designed as a console application that takes one parameter as described in the problem statement, the path to the input text file.

# Assumptions
* Input file contains only a single word with no spaces as the driver name
* For this test purposes, the name is the unique identifier. Meaning there can't be two drivers with the same name.
* The `Driver` command is issued before a `Trip` for a driver when parsing the input text file sequentially.
* The data is not persisted to any database. The program uses it's stack and heap memory and is lost when program terminates.

# Objects

## Driver

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

## Trip

**Constructors**

| Name  | Description |
| ------------- | ------------- |
| Trip(TimeSpan, TimeSpan, distance)  | Initializes a new Trip object with the given StartTime, EndTime and DistanceTravelled |

**Properties**

| Name | Description |
| --- | --- |
| StartTime | Gets or Sets the start time of the trip |
| EndTime | Gets or Sets the end time of the trip |
| Distance | Gets or Sets the distance travelled during the trip |
| AvgSpeed | Gets or Sets the average speed for the trip |

## Command

**Constructors**

No defined constructor. Class contains only static properties and methods.

**Properties**

| Name | Description |
| --- | --- |
| ValidCommands | static property that contains all the valid commands of the program |

**Methods**

| Name | Description |
| --- | --- |
| ExecuteAddDriverCommand(string[]) | Creates a driver object from the parsed command string that is passed in. |
| ExecuteAddTripCommand(ref Driver, string[]) | Creates a Trip object and attaches to the driver. |

# Implementation details
The program accepts the path to a text file and does some basic validations on the command args and the path validity. The format of the input text is assumed to be the following.

```
Driver Dan
Driver Alex
Driver Bob
Trip Dan 07:15 07:45 17.3
Trip Dan 06:12 06:32 21.8
Trip Alex 12:01 13:16 42.0
```

We open the file into a StreamReader (C# utility class for stream reading files) and read each line. Each line is assumed to have one of the following two commands.
* Driver
* Trip

There are two functions **ProcessLine** and **GenerateDriverReport** in the Main program.

```
static void ProcessLine(string commandLine, int lineNumber, ref List<Driver> drivers) { ... }
```
The above method is called for each line found on the input file. It splits the string the space delimiter along with removing extra spaces. It validates the command and the argument count. Calls the static methods on the **Command** class to execute the commands.

```
static void GenerateDriverReport(List<Driver> drivers) { ... }
```
After processing the input text file we would have created Driver(s) and added their trips to the **drivers** object in our Main program. This function takes that list of Driver objects which contains the trip data and outputs the formatted driver summary to the Console. Output takes the following form.

```
Alex: 42 miles @ 34 mph
Dan: 39 miles @ 47 mph
Bob: 0 miles
```
