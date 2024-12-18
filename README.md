const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

function generateRandomNumber(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

function startGame() {
  console.log("\nWelcome to the Number Guessing Game!");
  console.log("I have randomly chosen a number between 1 and 100.");
  console.log("Your task is to guess the number. Good luck!\n");

  const randomNumber = generateRandomNumber(1, 100);
  let attempts = 0;

  function askGuess() {
    rl.question("Enter your guess: ", (input) => {
      const guess = parseInt(input, 10);
      attempts++;

      if (isNaN(guess)) {
        console.log("Invalid input. Please enter a valid number.\n");
        askGuess();
      } else if (guess < 1 || guess > 100) {
        console.log("Out of range. Please guess a number between 1 and 100.\n");
        askGuess();
      } else if (guess < randomNumber) {
        console.log("Too low! Try again.\n");
        askGuess();
      } else if (guess > randomNumber) {
        console.log("Too high! Try again.\n");
        askGuess();
      } else {
        console.log(Congratulations! You guessed the number ${randomNumber} correctly in ${attempts} attempts!\n);
        askReplay();
      }
    });
  }

  function askReplay() {
    rl.question("Would you like to play again? (yes/no): ", (answer) => {
      if (answer.toLowerCase() === "yes") {
        startGame();
      } else {
        console.log("Thanks for playing! Goodbye!");
        rl.close();
      }
    });
  }

  askGuess();
}

startGame();
