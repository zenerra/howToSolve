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

### Classes and Constructors
```csharp
 class Person
 {
     public int id { get; set; }
     public double average { get; set; }
     public string name { get; set; }
     public DateTime date { get; set; }

     public Sportolo(int id, double average, string name, DateTime date)
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


```

## 1. Filtering (Where)
Select people older than 25.



```csharp
var olderThan25 = people.Where(p => p.Age > 25);
```

#### 2. Sorting (OrderBy, ThenBy)
Sort people by age, then by name.


```csharp
var sortedPeople = people.OrderBy(p => p.Age).ThenBy(p => p.Name);
```

#### 3. Selecting Specific Fields (Select)
Get a list of names and salaries.

```csharp
var namesAndSalaries = people.Select(p => new { p.Name, p.Salary });
```

#### 4. Grouping (GroupBy)
Group people by age.


```csharp
var groupedByAge = people.GroupBy(p => p.Age)
                         .Select(g => new { Age = g.Key, People = g });
```


#### 5. Aggregation (Count, Sum, Average, Max, Min)
Calculate statistics.

```csharp
int count = people.Count(); // Total people
int over30Count = people.Count(p => p.Age > 30); // People over 30
double totalSalary = people.Sum(p => p.Salary); // Total salary
double avgSalary = people.Average(p => p.Salary); // Average salary
int maxAge = people.Max(p => p.Age); // Oldest age
```

#### 7. First, Last, Single
Get specific elements.

```csharp
Person firstPerson = people.First(); // First person
Person lastPerson = people.Last(); // Last person
Person singlePerson = people.Single(p => p.Id == 1); // Person with Id 1
// Use FirstOrDefault, LastOrDefault, SingleOrDefault to avoid exceptions
Person firstOrNull = people.FirstOrDefault(p => p.Age > 40); // Null if not found
```

#### 8. Any and All
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
const express = require('express');
const app = express();
const port = 3000;

app.get('/hello', (req, res) => {
    res.send(`Hello!`);
});

const result = await connection.execute(
    'SELECT nev1, nev2 FROM nevnap WHERE ho = ? AND nap = ?',
    [ho, napSzam]
);

app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
});

app.post('/adatok', (req, res) => {
    const ujAdat = req.body;
    adatok.push(ujAdat);
    res.status(201).json(ujAdat);
});
```

## Frontend
*(Empty for now)*
