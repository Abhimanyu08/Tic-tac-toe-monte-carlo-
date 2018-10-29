"""
Monte Carlo Tic-Tac-Toe Player
"""

import random
import poc_ttt_gui
import poc_ttt_provided as provided

# Constants for Monte Carlo simulator
# You may change the values of these constants as desired, but
#  do not change their names.
NTRIALS = 15         # Number of trials to run
SCORE_CURRENT = 1.0 # Score for squares played by the current player
SCORE_OTHER = 1.0   # Score for squares played by the other player
    
# Add your functions here.

def mc_trial(board,player):
    in_progress = True
    current_board = board
    curr_player = player
    while in_progress:
        em_squares = current_board.get_empty_squares()
        if len(em_squares) != 0:
            sqr = random.choice(em_squares)
            current_board.move(sqr[0],sqr[1],curr_player)
            curr_player = provided.switch_player(curr_player)
            if current_board.check_win() == provided.PLAYERX or current_board.check_win() == provided.PLAYERO or current_board.check_win() == provided.DRAW:
                in_progress = False
        else:
            in_progress = False

def mc_update_scores(scores,board,player):
    curr_player = player
    curr_board = board
    lst = []
    w_lst = []
    l_lst = []
    em_lst = []
    winner = curr_board.check_win()
    loser = provided.switch_player(winner)
    for idx in range(curr_board.get_dim()):
        for jdx in range(curr_board.get_dim()):
            lst.append((idx,jdx))
    if winner == provided.DRAW:
        for jdx in lst:
            scores[jdx[0]][jdx[1]] += 0
    else:
        for idx in lst:
            if curr_board.square(idx[0],idx[1]) == winner:
                w_lst.append(idx)
            elif curr_board.square(idx[0],idx[1]) == loser:
                l_lst.append(idx)
            else:
                em_lst.append(idx)
    for idx in em_lst:
        scores[idx[0]][idx[1]] += 0
    if winner == curr_player:
        for idx in w_lst:
            scores[idx[0]][idx[1]] += SCORE_CURRENT
        for jdx in l_lst:
            scores[jdx[0]][jdx[1]] -= SCORE_OTHER
    elif loser == curr_player:
        for idx in w_lst:
            scores[idx[0]][idx[1]] += SCORE_OTHER
        for jdx in l_lst:
            scores[jdx[0]][jdx[1]] -= SCORE_CURRENT
        
def get_best_move(board,scores):
    curr_board = board
    em_squares = curr_board.get_empty_squares()
    if len(em_squares) > 0 :
        sc_of_ems = []
        max_sq = []
        for jdx in em_squares:
            sc_of_ems.append(scores[jdx[0]][jdx[1]])
        max_sc = max(sc_of_ems)
        for idx in em_squares:
            if scores[idx[0]][idx[1]] == max_sc:
                max_sq.append(idx)
    return random.choice(max_sq)

def mc_move(board,player,trials):
    trials = NTRIALS
    scores = [[0 for dummy_idx in range(board.get_dim())] for dummy_jdx in range(board.get_dim())]
    for _ in range(trials):
        curr_board = board.clone()
        curr_pl = player
        mc_trial(curr_board,curr_pl)
        mc_update_scores(scores,curr_board,curr_pl)
    return get_best_move(board,scores)
        
        

# Test game with the console or the GUI.  Uncomment whichever 
# you prefer.
#change the number in poc_ttt_gui.run_gui(x...) to open a higher matrix tic-tac-toe game.
#provided.play_game(mc_move, NTRIALS, False)        
#poc_ttt_gui.run_gui(3, provided.PLAYERX, mc_move, NTRIALS, False)
