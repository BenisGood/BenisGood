const board = document.getElementById('board');
const restartButton = document.getElementById('restartButton');

const candyColors = ['red', 'orange', 'yellow', 'green', 'blue', 'purple'];

function createBoard() {
  for (let i = 0; i < 6; i++) {
    for (let j = 0; j < 6; j++) {
      const candy = document.createElement('div');
      candy.classList.add('candy');
      candy.style.backgroundColor = candyColors[Math.floor(Math.random() * candyColors.length)];
      board.appendChild(candy);
    }
  }
}

function matchCandies() {
  const candies = board.getElementsByClassName('candy');
  const matches = [];

  for (let i = 0; i < candies.length; i++) {
    const candy = candies[i];
    const top = i - 6;
    const bottom = i + 6;
    const left = i - 1;
    const right = i + 1;

    if (top >= 0 && candy.style.backgroundColor === board.children[top].style.backgroundColor) {
      matches.push([candy, board.children[top]]);
    }
    if (bottom < candies.length && candy.style.backgroundColor === board.children[bottom].style.backgroundColor) {
      matches.push([candy, board.children[bottom]]);
    }
    if (left >= 0 && candy.style.backgroundColor === board.children[left].style.backgroundColor) {
      matches.push([candy, board.children[left]]);
    }
    if (right < candies.length && candy.style.backgroundColor === board.children[right].style.backgroundColor) {
      matches.push([candy, board.children[right]]);
    }
  }

  for (let i = 0; i < matches.length; i++) {
    const match = matches[i];
    match[0].parentNode.removeChild(match[0]);
    match[1].parentNode.removeChild(match[1]);
  }

  setTimeout(createBoard, 500);
}

createBoard();
restartButton.addEventListener('click', () => {
  board.innerHTML = '';
  createBoard();
});

setInterval(matchCandies, 1000);
