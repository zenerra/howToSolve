# howToSolve

## General Guide

### Useful Webpages
- [StackOverflow](https://stackoverflow.com/)
- [W3Schools](https://www.w3schools.com/)
- [Merlinvizsga](https://merlinvizsga.hu/) (For Node modules setup)
- [Bootstrap](https://getbootstrap.com/)

### If XAMPP Won't Start
1. Navigate to: `C:\xampp\mysql\backup`
2. Press `Ctrl + X` to cut the contents
3. Navigate to: `C:\xampp\mysql\data`
4. Press `Ctrl + A` to select all, then `Ctrl + P` to paste

## Desktop

### Classes and Constructors
```csharp
class Ember
{
    public int azonosito { get; set; }
    
    public Ember(int azonosito)
    {
        this.azonosito = azonosito;
    }
}
```

### Reading a File
```csharp
List<Ember> emberek = new List<Ember>();

using (StreamReader sr = new StreamReader("filename.txt"))
{
    while (!sr.EndOfStream)
    {
        string line = sr.ReadLine();
        string[] data = line.Split(';');
        int azonosito = int.Parse(data[0]);
        data[1] = data[1].Replace(',', '.');
        double atlag = double.Parse(data[1]);
        DateTime datum = Convert.ToDateTime(data[5]);
        Ember ember = new Ember(azonosito, atlag, datum);
        emberek.Add(ember);
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
