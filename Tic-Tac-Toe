"""
Monte Carlo Tic-Tac-Toe Player
"""

import random
import poc_ttt_gui
import poc_ttt_provided as provided

EMPTY = provided.EMPTY
PLAYERX = provided.PLAYERX
PLAYERO = provided.PLAYERO
DRAW = provided.DRAW
            
NTRIALS = 1         # Number of trials to run
SCORE_CURRENT = 1.0 # Score for squares played by the current player
SCORE_OTHER = 1.0   # Score for squares played by the other player

# Add your functions here.
def mc_trial(board, player):
    """
    play a game
    """
    while board.check_win() == None:
        empty_squares = board.get_empty_squares()
        #get a list of all empty squares
        
        random_move = random.choice(empty_squares)
        # choose a empty squares randomly
        board.move(random_move[0], random_move[1], player)
        # make a random move
        
        provided.switch_player(player)
        # switch player

def mc_update_scores(scores, board, player):
    """
    score the completed board and update the scores grid
    """
    if board.check_win() == DRAW:
        for dummy_square in scores:
            dummy_square = 0
    else:
        dim = board.get_dim()
        for dummy_row in range(dim):
            for dummy_col in range(dim):
                check_square = board.square(dummy_row, dummy_col)
            # check every square in the borad
            
                if check_square == EMPTY:
                    scores[dummy_row][dummy_col] += 0
            
                else:
                    if board.check_win() == player:
                        if check_square == player:
                            scores[dummy_row][dummy_col] += SCORE_CURRENT
                        else:
                            scores[dummy_row][dummy_col] += -SCORE_OTHER
                    else:
                        if check_square == player:
                            scores[dummy_row][dummy_col] += -SCORE_CURRENT
                        else:
                            scores[dummy_row][dummy_col] += SCORE_OTHER
                   
    
def get_best_move(board, scores):
    """
    find empty squares with maxmum score to move
    """
    empty_squares = board.get_empty_squares() 
    # return a list of (row, col)
    
    if empty_squares == None:
        print "No space to move."
    else:
        empty_score = {}
        max_empty_square = []
        for dummy_empty in empty_squares:
            row = dummy_empty[0]
            col = dummy_empty[1]
            empty_score[dummy_empty] = scores[row][col]
    
        max_score = max(empty_score.values())
    
        for dummy_empty, dummy_score in empty_score.items():
            if dummy_score == max_score:
                max_empty_square.append(dummy_empty)
    
        return random.choice(max_empty_square)
                
def mc_move(board, player, trials):
    """
    machine learn several times to find the max score empty square
    """
    
    dim = board.get_dim()      
    scores = [[0 for dummy_col in range(dim)] for dummy_row in range(dim)]
    for dummy_trial in range(1,trials+1):
        
        current_board = board.clone()
        mc_trial(current_board,player)
        mc_update_scores(scores, current_board, player)
        
    return get_best_move(board, scores)

# Test game with the console or the GUI.  Uncomment whichever 
# you prefer.  Both should be commented out when you submit 
# for testing to save time.

provided.play_game(mc_move,NTRIALS, False)        
poc_ttt_gui.run_gui(3, provided.PLAYERX, mc_move, NTRIALS, False)
