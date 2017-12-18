Answers for Day 11

tictactoe-game-player.js

Assignment: Explain how this apparently sequential code can function to play *two* sides of the game.
Solution: Because the code is based on promises. When all expressions for given User evaluates to true, then it's his or her turn. After that user makes move, all expressions for the other user evaluate to true.

Assignment: Run load tests. See them succeed a couple of times.
Move expectMoveMade() and expectGameJoined() after joinGame() call, and expectGameCreated() after createGame() call like this:
	userB.joinGame(userA.getGame().gameId).expectMoveMade('X').expectGameJoined().then(function () {
Run load tests again. They should fail. Explain why they fail.
Solution: It didn't make any difference for me. The tests still succeded after changing the code.

-----

tictactoe.loadtest.js

Assignment: Find appropriate numbers to configure the load test so it passes on your buildserver under normal load.
Solution: My local machine was occasionally up to 18. I left it at
    let count = 12;

test-api.js
Assignment: Trace this call - back and forth - through the code.
Put in log statements that enable you to trace the messages going back and forth.
Result is a list of modules/functions in this source code which get invoked when cleanDatabase is called.

user-api.js
Assignment: Explain what the push/pop functions do for this API. What effect would it have on the fluent API if we did not have them?
Solution: They store the order of the events. If we didn't have them, the moves could be out of order.
