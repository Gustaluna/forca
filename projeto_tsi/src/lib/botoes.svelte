<script>
    let word = 'hangman';
    let attempts = 6;
    let hiddenWord = Array(word.length).fill('_');
    let guessedLetters = new Set();
    let guess = '';
  
    function checkLetter() {
      if (guessedLetters.has(guess)) return;
      guessedLetters.add(guess);
  
      let found = false;
      for (let i = 0; i < word.length; i++) {
        if (word[i] === guess) {
          hiddenWord[i] = guess;
          found = true;
        }
      }
  
      if (!found) attempts--;
    }
  </script>
  
  <div>
    <h1>Svelte Hangman</h1>
    <p>Attempts left: {attempts}</p>
    <p>
      Word: {hiddenWord.join(' ')}
    </p>
  
    <div>
      <p>Guessed letters:</p>
      <p>
        {#each Array.from(guessedLetters) as letter}
          <span>{letter}</span>
        {/each}
      </p>
    </div>
    <div>
      <p>Guess a letter:</p>
      <input type="text" bind:value="{guess}" />
      <button on:click="{checkLetter}">Submit</button>
    </div>
  
    {#if attempts === 0}
      <p>Game Over! The word was "{word}".</p>
    {:else if !hiddenWord.includes('_')}
      <p>Congratulations! You won!</p>
    {/if}
  </div>