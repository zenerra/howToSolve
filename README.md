# howToSolve

## General Guide

### Setup Project Directory

```bash
mkdir "Project name here"
cd "Project name here"

mkdir backend
mkdir "subdirectory2"
mkdir "subdirectory3"
```

#### Useful Webpages
- [StackOverflow](https://stackoverflow.com/)
- [W3Schools](https://www.w3schools.com/)
- [Bootstrap](https://getbootstrap.com/)

#### VSC Extensions:
- EasyZoom
- Live Server
- Thunder Client
- Auto Rename Tag 

#### If XAMPP Won't Start
1. Navigate to: `C:\xampp\mysql\backup`
2. Press `Ctrl + X` to cut the contents
3. Navigate to: `C:\xampp\mysql\data`
4. Press `Ctrl + A` to select all, then `Ctrl + P` to paste

## Desktop 
Target finish time: **~1h 25min**

### Text manipulation
```csharp
Replace(',','-');  // 2019-2-12
Trim('-');  // 2019212 
Split(',');  // {apple, banana, orange}
Contains("YES") // returns true

char[] nameArray = {'A', 'l', 'i', 'c', 'e'};
string name = new string(nameArray);

Math.Round(number, 2)); // 5.43529 -> 5.44 (Honorable mention: Floor(), Ceiling())
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
        Person person = new Person(id, average, name, date);
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

```csharp
foreach (var group in groupedByYear)
{
    Console.WriteLine($"Year: {group.Year}");
    foreach (var person in group.People)
    {
        Console.WriteLine($"- {person.Name}");
    }
}
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
Target finish time: **~1h**


### Setup Node.js Express
#### Installs necessary packages inside backend folder and creates app.js/index.js file with basic content 
```bash
cd backend
npm install express mysql2 cors
npm pkg set type=module
cd backend
echo "import express from 'express';" > app.js
echo "import cors from 'cors';" >> app.js
echo "import mysql from 'mysql2';" >> app.js
echo "" >> app.js
echo "const app = express();" >> app.js
echo "app.use(cors());" >> app.js
echo "app.use(express.json());" >> app.js
echo "" >> app.js
echo "const db = mysql.createConnection({" >> app.js
echo "    host: 'localhost'," >> app.js
echo "    user: 'root'," >> app.js
echo "    password: ''," >> app.js
echo "    database: '', // Database name goes here" >> app.js
echo "    port: 3306" >> app.js
echo "});" >> app.js
echo "" >> app.js
echo "// endpoints" >> app.js
echo "" >> app.js
echo "app.listen(3000, () => {" >> app.js
echo "    console.log('Server is running on http://localhost:3000');" >> app.js
echo "});" >> app.js
```

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
  const date = req.query.date; // KEY

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
    res.json({ // KEY
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

// Delete data by ID
app.delete("/api/nameday/:id", async (req, res)=>{
 const id = req.params.id; // Extracts the ID from the URL parameter, e.g., /api/nameday/123
  const sql = "DELETE FROM nameday WHERE id = ?";
  const [result] = await database.execute(sql, [id]);
  res.status(200).json(result);
})

app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});

```

## Frontend
Target finish time: **~1h 30min**

### Import Bootstrap
```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.6/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-4Q6Gf2aSP4eDXB8Miphtr37CMZZQ5oXLH2yaXMJ2w8e2ZtHTl7GptT4jmndRuHDT" crossorigin="anonymous">
```

### Display and submit cards dynamically using Bootstrap
```html
<div class="container">  <!-- To make the page responsive -->
   <form id="dateForm" class="mb-4">
      <div class="row g-3 align-items-end">
        <div class="col-auto">
          <label for="dateInput" class="form-label">Select Date:</label>
          <input type="date" id="dateInput" class="form-control" required>
        </div>
        <div class="col-auto">
          <button type="submit" class="btn btn-primary">Get Nameday</button>
        </div>
      </div>
    </form>
</div>


    <div id="namedayCards" class="row row-cols-1 row-cols-md-2 g-4"></div> // Place for the cards


    <script>
    // Handle form submission
    document.getElementById('dateForm').addEventListener('submit', async (e) => {
      e.preventDefault();
      const date = document.getElementById('dateInput').value;
      if (!date) return;

      // Clear previous cards
      const cardContainer = document.getElementById('namedayCards');
      cardContainer.innerHTML = '';

      // Fetch data from API
      try {
        const response = await fetch(`http://localhost:3000/api/nameday/?date=${date}`);
        if (!response.ok) {
          throw new Error('Failed to fetch nameday data');
        }
        const data = await response.json();

        // Check for error response
        if (data.error) {
          cardContainer.innerHTML = `<div class="alert alert-warning">${data.error}</div>`;
          return;
        }

        // Create Bootstrap cards for each name
        const names = [data.name1, data.name2];
        names.forEach(name => {
          const card = document.createElement('div');
          card.className = 'col';
          card.innerHTML = `
            <div class="card h-100">
              <div class="card-body">
                <h5 class="card-title">${name}</h5>
                <p class="card-text">Nameday on ${data.date}</p>
              </div>
            </div>
          `;
          cardContainer.appendChild(card);
        });
      } catch (error) {
        console.error('Error:', error);
        cardContainer.innerHTML = `<div class="alert alert-danger">Error fetching data</div>`;
      }
    });
  </script>
```
