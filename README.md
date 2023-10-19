# demon
A Dice Game Called Pig
import random

def roll_dice():
    die1 = random.randint(1, 6)
    die2 = random.randint(1, 6)
    return die1, die2

def computer_turn(game_score, goal):
    turn_score = 0
    while turn_score < goal:
        die1, die2 = roll_dice()
        print(f"Computer rolled {die1}, {die2}")

        if die1 == 1 and die2 == 1:
            game_score = 0
            turn_score = 0
            print("Double 1s! Game score reset to 0.")
            break
        elif die1 == 1 or die2 == 1:
            turn_score = 0
            print("Rolled a 1. Turn score reset to 0.")
            break
        else:
            turn_score += die1 + die2
            print(f"Turn total: {turn_score}")

    game_score += turn_score
    return game_score

def human_turn(game_score):
    turn_score = 0
    while True:
        die1, die2 = roll_dice()
        print(f"You rolled {die1}, {die2}")

        if die1 == 1 and die2 == 1:
            game_score = 0
            turn_score = 0
            print("Double 1s! Game score reset to 0.")
            break
        elif die1 == 1 or die2 == 1:
            turn_score = 0
            print("Rolled a 1. Turn score reset to 0.")
            break
        elif die1 == 4 and die2 == 5:
            turn_score += 9
            print("You rolled 4 and 5. Add 9 to this turn.")
        elif die1 == 4 and die2 == 1:
            turn_score = 0
            print("You rolled 4 and 1. Player loses turn and points for this turn.")
            break
        elif die1 == 1 and die2 == 1:
            game_score = 0
            turn_score = 0
            print("Double 1s! Game score reset to 0.")
            break
        else:
            turn_score += die1 + die2
            print(f"Turn total: {turn_score}")

        roll_again = input("Roll again (y/n)? ").strip().lower()
        if roll_again != 'y':
            game_score += turn_score
            break

    return game_score

def human_vs_computer():
    human_score = 0
    computer_score = 0
    goal = 20

    while human_score < 100 and computer_score < 100:
        print(f"You: {human_score} Computer: {computer_score}")
        human_score = human_turn(human_score)

        if human_score >= 100:
            print(f"You: {human_score} Computer: {computer_score}")
            print("Congratulations! You win!")
            break

        print(f"You: {human_score} Computer: {computer_score}")
        computer_score = computer_turn(computer_score, goal)

        if computer_score >= 100:
            print(f"You: {human_score} Computer: {computer_score}")
            print("Computer wins!")
            break

def computer_solo(goal):
    computer_score = 0
    turns = 0
    while computer_score < 100:
        print(f"Turn: {turns + 1} Score: {computer_score}")
        computer_score = computer_turn(computer_score, goal)
        turns += 1
    print(f"Turns: {turns}")
    return turns
    
def world_championship(games, goal_1, goal_2):
    wins_1, wins_2 = 0, 0

    for _ in range(games):
        score_1, score_2 = 0,0
        while score_1 < 100 and score_2 < 100:
            score_1 = computer_turn(score_1, goal_1)
            score_2 = computer_turn(score_2, goal_2)

        if score_1 > score_2:
            wins_1 += 1
        elif score_2 > score_1:
            wins_2 += 1

    print(f"Computer 1: {wins_1} wins Computer 2: {wins_2}")
    return wins_1, wins_2
    
def validate_response(prompt, response_1, response_2):
    while True:
        user_response = input(prompt).strip().lower()
        if user_response == response_1 or user_response == response_2:
            return user_response

if __name__ == '__main__':
    print(roll_dice())
    computer_turn(0, 20)
    human_turn(57)
    computer_solo(20)
    world_championship(9, 20, 20)
    validate_response("Does this work (t/f)?", 't', 'f')
