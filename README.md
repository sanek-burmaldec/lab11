<!DOCTYPE html>
<html lang="uk">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Лабораторна робота №11 — Об’єкт Airplane</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 720px; margin: 30px auto; padding: 0 16px; }
    h1 { font-size: 22px; }
    #title { color: #333; }
    .card { border: 1px solid #ccc; border-radius: 8px; padding: 12px 16px; margin: 12px 0; }
    button { padding: 8px 14px; margin-right: 8px; cursor: pointer; }
    #output p { margin: 6px 0; }
  </style>
</head>
<body>
  <h1 id="title">Лабораторна робота №11. Об’єкти у JavaScript</h1>

  <button id="btnFly">Викликати fly()</button>
  <button id="btnAll">Показати всі літаки</button>
  <button id="btnColor">Змінити колір заголовка</button>

  <div class="card" id="output"></div>

  <script>
    // 1. Власний об’єкт (об’єктний літерал) із властивостями та методом
    let airplane = {
      model: "Boeing 737",
      capacity: 189,
      company: "Ukraine International Airlines",
      fly: function () {
        return "Літак " + this.model + " компанії " + this.company +
               " летить із " + this.capacity + " пасажирами.";
      }
    };

    // Динамічне додавання властивості та методу
    airplane.speed = 840; // км/год
    airplane.info = function () {
      return `${this.model} | місць: ${this.capacity} | авіакомпанія: ${this.company} | швидкість: ${this.speed} км/год`;
    };

    // 2. Функція-конструктор для створення однотипних об’єктів
    function Airplane(model, capacity, company) {
      this.model = model;
      this.capacity = capacity;
      this.company = company;
      this.fly = function () {
        return "Літак " + this.model + " компанії " + this.company +
               " летить із " + this.capacity + " пасажирами.";
      };
    }

    let planes = [
      new Airplane("Airbus A320", 180, "Wizz Air"),
      new Airplane("Boeing 777", 396, "Emirates"),
      new Airplane("Embraer 190", 100, "LOT Polish Airlines")
    ];

    // 3. Клас (ES6) — той самий об’єкт у сучасному записі
    class AirplaneClass {
      constructor(model, capacity, company) {
        this.model = model;
        this.capacity = capacity;
        this.company = company;
      }
      fly() {
        return `Літак ${this.model} компанії ${this.company} летить із ${this.capacity} пасажирами.`;
      }
    }
    let classPlane = new AirplaneClass("ATR 72", 72, "Air Baltic");

    // 4. Робота з DOM
    const output = document.getElementById("output");
    const heading = document.getElementById("title");

    function print(text) {
      const p = document.createElement("p");
      p.textContent = text;
      output.appendChild(p);
    }

    document.getElementById("btnFly").onclick = function () {
      output.innerHTML = "";
      print(airplane.fly());
      print(airplane.info());
    };

    document.getElementById("btnAll").onclick = function () {
      output.innerHTML = "";
      planes.forEach(function (p) { print(p.fly()); });
      print(classPlane.fly());
    };

    document.getElementById("btnColor").onclick = function () {
      heading.style.color = heading.style.color === "blue" ? "#333" : "blue";
    };

    // Одразу показати результат при відкритті сторінки
    document.getElementById("btnFly").onclick();

    // Вивід у консоль (F12)
    console.log(airplane.fly());
    planes.forEach(p => console.log(p.fly()));
    console.log(classPlane.fly());
  </script>
</body>
</html>
