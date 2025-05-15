# howToSolve

## General Guide

### Useful Webpages
- [StackOverflow](https://stackoverflow.com/)
- [W3Schools](https://www.w3schools.com/)
- [Bootstrap](https://getbootstrap.com/)

### If XAMPP Won't Start
1. Navigate to: `C:\xampp\mysql\backup`
2. Press `Ctrl + X` to cut the contents
3. Navigate to: `C:\xampp\mysql\data`
4. Press `Ctrl + A` to select all, then `Ctrl + P` to paste

## Desktop

### Text manipulation
```csharp
Replace(',','-');  // 2019-2-12
Trim('-');  // 2019212 
Split(',');  // {apple, banana, orange}
Contains("YES") // returns true

char[] nameArray = {'A', 'l', 'i', 'c', 'e'};
string name = new string(nameArray);
```

### Classes and Constructors
```csharp
 class Person
 {
     public int id { get; set; }
     public double average { get; set; }
     public string name { get; set; }
     public DateTime date { get; set; }

     public Person(int id, double average, string name, DateTime date)
     {
         this.id = id;
         this.average = average;
         this.name = name;
         this.date = date;
     }
 }
```

### Reading a File
```csharp
List<Person> peopleList = new List<Person>();

using (StreamReader sr = new StreamReader("filename.txt"))
{
    while (!sr.EndOfStream)
    {
        string line = sr.ReadLine();
        string[] data = line.Split(';');
        int id = int.Parse(data[0]);
        data[1] = data[1].Replace(',', '.');
        double atlag = double.Parse(data[1]);
        string name = data[2];
        DateTime date = Convert.ToDateTime(data[3]);
        Person personList = new Person(id, average, name, date);
        peopleList.Add(person);
    }
}
```

### Creating a File
```csharp
using (StreamWriter sw = File.CreateText("filename.txt"))
{
    sw.WriteLine("...");
}
```
### LINQ Examples
```csharp
using System.Linq;
```

#### 1. Aggregation (Count, Sum, Average, Max, Min)
Calculate statistics.

```csharp
int count = people.Count(); // Total people
int over30Count = people.Count(p => p.Age > 30); // People over 30
double totalSalary = people.Sum(p => p.Salary); // Total salary
double avgSalary = people.Average(p => p.Salary); // Average salary
int maxAge = people.Max(p => p.Age); // Oldest age
```

#### 2. Filtering (Where)
Select people older than 25.

```csharp
var olderThan25 = people.Where(p => p.Age > 25);
```

#### 3. Sorting (OrderBy, ThenBy)
Sort people by age, then by name.


```csharp
var sortedPeople = people.OrderBy(p => p.Age).ThenBy(p => p.Name);
```

#### 4. Selecting Specific Fields (Select)
Get a list of names and salaries.

```csharp
var namesAndSalaries = people.Select(p => new { p.Name, p.Salary });
```

#### 5. Grouping (GroupBy)
Group people by age.


```csharp
var groupedByAge = people.GroupBy(p => p.Age).Select(g => new { Age = g.Key, People = g });
```


#### 6. First, Last, Single
Get specific elements.

```csharp
Person firstPerson = people.First(); // First person
Person lastPerson = people.Last(); // Last person
Person singlePerson = people.Single(p => p.Id == 1); // Person with Id 1
```

#### 7. Any and All
Check conditions.

```csharp
bool hasYoung = people.Any(p => p.Age < 25); // True if any person is under 25
bool allHighEarners = people.All(p => p.Salary > 40000); // True if all earn > 40k
```

#### Tips for Effective LINQ
- **Performance**: Avoid multiple enumerations; materialize results with `.ToList()` if needed.
- **Debugging**: Break complex queries into smaller steps.

## Backend

### Endpoints
```javascript
import express from "express";
import mysql from "mysql2";
import cors from "cors";

const app = express();
const port = 3000;

app.use(express.json());
app.use(cors());

const db = mysql.createConnection({
  host: "localhost",
  user: "root",
  password: "",
  database: "namedays",
});

// API endpoint to get nameday by date
app.get("/api/nameday/", (req, res) => {
  // Extract "date" from query parameter
  const date = req.query.date;

  // Check if date is specified
  if (!date) {
    return res.status(400).json({ error: "Date parameter is required" });
  }

  // get the month and day
  const month = date.split("-")[0];
  const monthName = convertMonthNumberToName(month);
  const day = date.split("-")[1];
  const sql = SELECT name1, name2 FROM nameday WHERE month = ${month} AND day = ${day};

db.query(sql, (err, result) => {
    if (err) {
      console.log("Server error");
    }
    if (result.length === 0) {
      console.log("No nameday found");
    }
    const nameday = result[0];

// Send response with formatted date and nameday data
    res.json({
      date: `${monthName} ${day}.`,
      name1: nameday.name1,
      name2: nameday.name2,
    });
  });
});

// Function to convert month number to month name
function convertMonthNumberToName(monthNumber) {
  switch (monthNumber) {
    case "1":
      return "January";
    case "2":
      return "February";
    ...
  }
}


app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});

```

## Frontend
*(Empty for now)*
