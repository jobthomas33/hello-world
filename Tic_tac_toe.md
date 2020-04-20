from IPython.display import clear_output
from random import randint

def display_board(board):
    clear_output()
    print('   |   |')
    print(' ' + board[7]+' | '+ board[8]+' | '+ board[9])
    print('   |   |')
    print('-----------')
    print('   |   |')
    print(' ' + board[4]+' | '+ board[5]+' | '+ board[6])
    print('   |   |')
    print('----------')
    print('   |   |')
    print(' ' + board[1]+' | '+ board[2]+' | '+ board[3])
    print('   |   |')

def player_input():
    '''
    output will be in the form of a tuple
    '''
    marker = ''
    while marker !='X' and marker !='O':
        marker=input('Player1 please give your input: ').upper()
    if marker=='X':
            return ('X','O')
    else:
            return('O','X')
        
def choose_first():
    num=randint(1,2)
    if num==1:
        return "player 1"
    else:
        return "player 2"
        
def player_choice():
    
    position=0
    while position not in range(1,10) or not space_check(board,position):
        position=int(input('please enter a posion (1-9): '))
    return position
            
            
def space_check(board, position):
    
    return board[position]==' '


def full_board_check(board):
    
    for i in range(1,10):
        if space_check(board,i):
            return False
    #Board is full if we return True
    return True

def place_marker(board, marker, position):
    board[position]=marker
    
def win_check(board, marker):
    
    if board[1]==board[2]==board[3]==marker:
        return True
    elif board[4]==board[5]==board[6]==marker:
        return True
    elif board[7]==board[8]==board[9]==marker:
        return True
    elif board[1]==board[4]==board[7]==marker:
        return True
    elif board[2]==board[5]==board[8]==marker:
        return True
    elif board[3]==board[6]==board[9]==marker:
        return True
    elif board[7]==board[5]==board[3]==marker:
        return True
    elif board[1]==board[5]==board[9]==marker:
        return True
    else:
        return False
    
def replay():
    
    choice=input('play again? Enter Yes or No ')
    return choice=='Yes'
    
    #Execution
print('Welcome to Tic Tac Toe!')
while True:
    #Play game
    
    board=[' ']*10
    #display_board(board)
    
    player1_marker,player2_marker=player_input()
    
    turn=choose_first()
    print(turn,"go first!")
    
    play_game=input('Ready to play? y or n ')
    if play_game=='y':
        game_on=True
    else:
        game_on=False
    
    while game_on:
        if turn=="player 1":
            display_board(board)
            position=player_choice()
            place_marker(board, player1_marker, position)
            
            if win_check(board,player1_marker):
                display_board(board)
                print('Player 1 has won!!')
                game_on=False
            else:
                if full_board_check(board):
                    print("Game has Tied!")
                    game_on=False
                else:
                    turn="Player 2"
               

        else:
            display_board(board)
            position=player_choice()
            place_marker(board, player2_marker, position)
            if win_check(board,player2_marker):
                display_board(board)
                print('Player 2 has won!!')
                game_on=False
            else:
                if full_board_check(board):
                    print("Game has Tied!")
                    game_on=False
                else:
                    turn="player 1"
    
    if not replay():
        break
    else:
        pass
