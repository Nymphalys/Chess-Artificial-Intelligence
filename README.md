Chess Artificial Intelligence
Concepts :
-	Graphics: draw and Move generation
-	Algorithm: Board Evaluation
-	AI: Minimax
-	Optimization: Alpha Beta pruning

Chessboard Display
	chessboard() this function is used for the calculation of the end point of the cordinates of the box to make and is also responsible for calling the drawSquare()
The main function, which is in charge of providing graphics to the display window, also calls this display function.
As there are 8 columns on a single chess board, the formation of boxes is done by iterating first from the first row, making the first column, then the second, and so on until the eighth column. After every call to draw, the colour of our current box, which changes every time, is also sent.
The same method described above is repeated until all 8 rows have been iterated, resulting in a total of 64 boxes (8 rows and 8 column).
Move Generation
	Define a polymorphic chessPiece object which contains the chess piece's location and which has a virtual draw() and a move() method. Derived classes will override the draw method to create draw different shapes for the pieces using OpenGL, while the move() method will check whether a move for a particular piece is valid. The move() method can be enforced if the position values are private.

Then define a chessBoard object for the board, which contains the pieces. Define a draw() method, which draws the board and calls the draw() method on each of the pieces.

The move generation library basically implements all the rules of chess. Based on this, we can calculate all legal moves for a given board state.

How to detect legal moves?
Function legalMoves() returns a vector<int> of all possible moves. (If p is in vector that means x = p / 8, y = p % 8 is a legal move).
Input of legalMoves() is position of piece where we clicked, and a bool variable lastWhite, which stores if the last moves was white.
If lastWhile == true and we click on a white piece again, we return false.
Find the piece that is lying on the given square if not, and then return all potential movements.

The input is the initial position, and the output is every motion that may be made from that position.

The first thing we'll do is create a function that just returns a random move out of all the potential moves. We can now play against the computer, although it performs below average.
Position evaluation
	Now let’s try to understand which side is stronger in a certain position. The simplest way to achieve this is to count the relative strength of the pieces on the board using the following table:
Pawn = 10
Knight = 30
Bishop = 30
Rook = 50
Queen = 90
King = 900

With the evalBoardState() function, we’re able to create an algorithm that chooses the move that gives the highest evaluation. The improvement is that our algorithm will now capture a piece if it can.
We have to create an algorithm that finds the best move.

Minimax Algorithm

Let’s assume A & B are playing a game. We are given a full binary tree of height n and each leaf node has a value. Player A is trying to maximise the score and player B is trying to minimize final score. Given both play optimally, what’s the largest/smallest score we can get (depending on the parity of n)?

The trick here is to work backwords. At last level, B will choose the minimum of the 2 child nodes. In next move A will the max of 2 child nodes. And this process keeps repeating.

Now how is this related to chess? If we give values to pieces, ans set score = total value of white pieces – total value of black pieces, then white is trying to maximize the score whereas black is trying to minimize the score.

AlphaBeta Pruning
The minimax algorithm is too slow at depth greater than 3. So, we introduce alpha beta pruning. Alpha-beta pruning is an optimization method to the minimax algorithm that allows us to disregard some branches in the search tree. This helps us evaluate the minimax search tree much deeper, while using the same resources. 
The alpha-beta pruning is based on the situation where we can stop evaluating a part of the search tree if we find a move that leads to a worse situation than a previously discovered move.

Improved evaluation function
The initial evaluation function is quite naive as we only count the material that is found on the board. To improve this, we add to the evaluation a factor that takes in account the position of the pieces. For example, a knight on the center of the board is better (because it has more options and is thus more active) than a knight on the edge of the board.

