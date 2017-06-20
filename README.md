# jQuery Tic-Tac-Toe with a Rails API — Part 2

Congratulations on setting up your Rails API back-end! Hopefully you took a short break to celebrate because the real fun starts now.

In this second installment, you're tasked with building out a JavaScript front-end to place on top of the Rails API we created in the previous exercise. For reference, [here's the video](http://flatiron-videos.s3.amazonaws.com/Learn%20Curriculum%20Helpers/ttt.mov) showing how the final product should function. (Right-click and `Save Link As...` to download.)

## Objectives
- Create a fully-functional tic-tac-toe game using jQuery and/or vanilla JavaScript.
- Make AJAX requests to a Rails API in order to save, update, and reload games.

## Getting started
Code your solution in `app/assets/javascripts/tictactoe.js`, which we're loading via the Rails asset pipeline. As a refresher, we added that file to the asset pipeline by specifying `//= require tictactoe` in our JavaScript manifest file (`app/assets/javascripts/application.js`).

You are welcome to use jQuery, pure JavaScript, or a combination of the two, but you should not have to create any new files or modify anything outside of `tictactoe.js`.

### Exploring the DOM
The only view our application requires lives in `app/views/home/index.html`. Before you dive into writing JavaScript, start the Rails server and familiarize yourself with the DOM that you'll be working with. Take special note of the way in which the squares of the game board are identified with `data-x` and `data-y` attributes.

## Conjunction junction, what's your function?
For the actual TTT functionality, the test suite is pretty opinionated. We've given you a lot of the structure, and the tests force you down a pretty specific path as far as which functions you need to define and what they should do:
- `player()`
  + Returns the token of the player whose turn it is, `'X'` when the `turn` variable is even and `'O'` when it is odd.
- `updateState()`
  + Invokes `player()` and adds the returned string (`'X'` or `'O'`) to the clicked square on the game board.
- `message()`
  + Accepts a string and adds it to the `div#message` element in the DOM.
- `checkWinner()`
  + Returns `true` if the current board contains any winning combinations (three `X` or `O` tokens in a row, vertically, horizontally, or diagonally). Otherwise, returns `false`.
  + If there is a winning combination on the board, `checkWinner()` should invoke `message()`, passing in the appropriate string based on who won: `'Player X Won!'` or `'Player O Won!'`
- `doTurn()`
  + Increments the `turn` variable by `1`.
  + Invokes the `updateState()` function, passing it the element that was clicked.
  + Invokes `checkWinner()` to determine whether the move results in a winning play.
- `attachListeners()`
  + Attaches the appropriate event listeners to the squares of the game board as well as for the `button#save`, `button#previous`, and `button#clear` elements.
  + When a user clicks on a square on the game board, the event listener should invoke `doTurn()` and pass it the element that was clicked.
  + ***NOTE***: `attachListeners()` _must_ be invoked inside either a `$(document).ready()` (jQuery) or a `window.onload = () => {}` (vanilla JavaScript). Otherwise, a number of the tests will fail (not to mention that your game probably won't function in the browser).

## Bonus(es)
1. Once all of the tests are passing and you have a functionally awesome / awesomely functional tic-tac-toe game with persistence, try refactoring your front-end to use ES6 `class`es and other OO design patterns. Think about the domain you're trying to model — how many classes do you need? What are the relationships between classes?
2. Implement a [memoization](https://www.sitepoint.com/implementing-memoization-in-javascript/) scheme for minimizing the amount of database calls your application makes.
3. Modify the `GameSerializer` to include the `updated_at` attribute, and display the last-updated time next to each saved game in the DOM.

## Resources
* [jQuery data()](https://api.jquery.com/jquery.data/)

<p class='util--hide'>View <a href='https://learn.co/lessons/js-tictactoe-rails-api'>jQuery Tic Tac Toe</a> on Learn.co and start learning to code for free.</p>
