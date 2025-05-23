<script>
  // Vytvoříme zamíchané pole čísel 1–8 a jedno prázdné políčko
  let grid = createShuffledGrid();

  // Velikost mřížky (3x3)
	  let size = 3;

  // Vytvoří náhodně zamíchané puzzle, které je možné vyřešit
  function createShuffledGrid() {
    let numbers = [1, 2, 3, 4, 5, 6, 7, 8, ''];
    let shuffled;

    do {
      shuffled = [...numbers];
      for (let i = shuffled.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * (i + 1));
        [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
      }
    } while (!isSolvable(shuffled));

    return shuffled;
  }

  // Funkce, která přesune dlaždici, pokud je vedle prázdné
  function moveTile(index) {
    let emptyIndex = grid.indexOf('');
    if (areNeighbors(index, emptyIndex)) {
      [grid[index], grid[emptyIndex]] = [grid[emptyIndex], grid[index]];
    }
  }

  // Zjistí, jestli jsou dva indexy vedle sebe (nahoře, dole, vlevo, vpravo)
  function areNeighbors(i1, i2) {
    let x1 = i1 % size;
    let y1 = Math.floor(i1 / size);
    let x2 = i2 % size;
    let y2 = Math.floor(i2 / size);
    return Math.abs(x1 - x2) + Math.abs(y1 - y2) === 1;
  }

  // Vrátí true, pokud je puzzle řešitelné (sudý počet inverzí)
  function isSolvable(arr) {
    let nums = arr.filter(n => n !== '');
    let inversions = 0;
    for (let i = 0; i < nums.length; i++) {
      for (let j = i + 1; j < nums.length; j++) {
        if (nums[i] > nums[j]) inversions++;
      }
    }
    return inversions % 2 === 0;
  }

  // Zkontroluje, jestli je puzzle správně složené
  function isSolved() {
    let correct = [1, 2, 3, 4, 5, 6, 7, 8, ''];
    return grid.every((val, idx) => val === correct[idx]);
  }
</script>

<h2>Jednoduché Puzzle 3×3</h2>

<!-- Mřížka puzzle -->
<div class="grid">
  {#each grid as tile, i}
    <div class="tile {tile === '' ? 'empty' : ''}" on:click={() => moveTile(i)}>
      {tile}
    </div>
  {/each}
</div>

<!-- Výhra -->
{#if isSolved()}
  <p><strong>Skvělé!</strong> Puzzle je složené správně! 🎉</p>
{/if}

<style>
  .grid {
    display: grid;
    grid-template-columns: repeat(3, 80px);
    gap: 5px;
    margin-bottom: 10px;
  }

  .tile {
    width: 80px;
    height: 80px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 24px;
    background-color: #f0f0f0;
    border: 2px solid #ccc;
    cursor: pointer;
    user-select: none;
  }

  .tile.empty {
    background-color: #fff;
    border: 2px dashed #aaa;
    cursor: default;
  }
</style>