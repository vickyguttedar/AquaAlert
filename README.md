<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="style.css" />
    <title>Drink Water</title>
  </head>
  <body>
    <h1>Drink Water</h1>
    <h2>Goal: 2 liters</h2>
    <div class="cup">
      <div class="remained" id="remained">
        <span id="liters"></span>
        <small>Remained</small>
      </div>
      <div class="percentage" id="percentage"></div>
    </div>
    <p class="text">Select how many glasses of water that you have drank</p>
    <div class="cups">
      <div class="cup cup-small">250 ml</div>
      <div class="cup cup-small">250 ml</div>
      <div class="cup cup-small">250 ml</div>
      <div class="cup cup-small">250 ml</div>
      <div class="cup cup-small">250 ml</div>
      <div class="cup cup-small">250 ml</div>
      <div class="cup cup-small">250 ml</div>
      <div class="cup cup-small">250 ml</div>
    </div>
    <script src="script.js"></script>
  </body>
</html>  

#css
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600&display=swap");

:root {
  --border-color: #144fc6;
  --fill-color: #6ab3f8;
}

* {
  box-sizing: border-box;
}

body {
  background-color: #3494e4;
  color: #fff;
  font-family: "Montserrat", sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 40px;
}

h1 {
  margin: 10px 0 0;
}

h2 {
  font-weight: 400;
  margin: 10px 0;
}

.text {
  text-align: center;
  margin: 0 0 5px;
}

.cup {
  background-color: #fff;
  border: 4px solid var(--border-color);
  color: var(--border-color);
  border-radius: 0 0 40px 40px;
  height: 330px;
  width: 150px;
  margin: 30px 0;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.cup.cup-small {
  height: 95px;
  width: 50px;
  border-radius: 0 0 15px 15px;
  background-color: rgba(255, 255, 255, 0.9);
  cursor: pointer;
  font-size: 14px;
  align-items: center;
  justify-content: center;
  text-align: center;
  margin: 5px;
  transition: 0.3s ease;
}

.cup.cup-small.full {
  background-color: var(--fill-color);
  color: #fff;
}

.cups {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  width: 280px;
}

.remained {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  flex: 1;
  transition: 0.3s ease;
}

.remained span {
  font-size: 20px;
  font-weight: bold;
}

.remained small {
  font-size: 12px;
}

.percentage {
  background-color: var(--fill-color);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 30px;
  font-weight: bold;
  height: 0;
  transition: 0.3s ease;
} 

#js 

const smallCups = document.querySelectorAll(".cup-small");
const liters = document.getElementById("liters");
const percentage = document.getElementById("percentage");
const remained = document.getElementById("remained");

const updateBigCup = () => {
  const fullCups = document.querySelectorAll(".cup-small.full").length;
  const totalCups = smallCups.length;
  if (fullCups === 0) {
    percentage.style.visibility = "hidden";
    percentage.style.height = 0;
  } else {
    percentage.style.visibility = "visible";
    percentage.style.height = `${(fullCups / totalCups) * 330}px`;
    percentage.innerText = `${(fullCups / totalCups) * 100}%`;
  }
  if (fullCups === totalCups) {
    remained.style.visibility = "hidden";
    remained.style.height = 0;
  } else {
    percentage.style.visibility = "visible";
    liters.innerText = `${2 - (250 * fullCups) / 1000}L`;
  }
};

const highlightCups = (index) => {
  if (index === 7 && smallCups[index].classList.contains("full")) index--;
  if (
    smallCups[index].classList.contains("full") &&
    !smallCups[index].nextElementSibling.classList.contains("full")
  ) {
    index--;
  }
  smallCups.forEach((cup, index2) => {
    if (index2 <= index) cup.classList.add("full");
    else cup.classList.remove("full");
  });
  updateBigCup();
};

smallCups.forEach((cup, index) =>
  cup.addEventListener("click", () => highlightCups(index))
);

updateBigCup();

