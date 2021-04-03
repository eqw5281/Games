import random
import time
print('The "?" Indicates a Face-Down Card\n')
while True:
    # Function checks score of hand when called upon
    def check_score(hand):
        ace_switch = 0
        score = 0
        for i in hand:
            # Assigns numeric values to face cards
            if i == 'J' or i == 'Q' or i == 'K' :
                i = 10
            elif i == 'A':
                ace_switch = 1
                i = 11
            score += i
        # Changes one ace from 11 to 1 if hand total is > 21
        # ace_count keeps track of number of aces that can still be changed
        if score > 21 and ace_switch == 1:
            for i in hand:
                if i == 'A':
                    score -= 10
                    print("(Ace Changed to 1)")
                    ace_switch -= 1
                    time.sleep(1)
                    break
        return score

    # Function draws card and adds to hand when called upon
    def draw_card(hand):
        card = list.pop(cards)
        hand.append(card)
        return hand

    # Generate and Shuffle Card Deck
    cardnum = list(range(2,11))
    cardletters = ['J','Q','K','A']
    cards = (cardnum + cardletters) * 4
    random.shuffle(cards)

    # Dealer Draws 2 Cards
    dlr_hnd = []
    draw_card(dlr_hnd)
    draw_card(dlr_hnd)
    print("Dealer's Hand: ",'?',dlr_hnd[1])
    # Dealer's score is checked here to look for double aces
    dlr_score = check_score(dlr_hnd)

    # Player Draws 2 Cards
    plyr_hnd = []
    draw_card(plyr_hnd)
    draw_card(plyr_hnd)
    print("Your Hand: ",plyr_hnd)
    # Player's score is checked here to look for double aces
    plyr_score = check_score(plyr_hnd)

    # Player can choose to draw cards or stay. Score and hand are updated
    if plyr_score < 21:
        while True:
            plyr_choice = str(input('\nHit or Stay?: ')).lower()
            if plyr_choice == 'hit':
                # Player chose to draw. Card is added and score is updated
                draw_card(plyr_hnd)
                plyr_score = check_score(plyr_hnd)
                print("\nDealer's Hand: ",'?',dlr_hnd[1])
                print("Your Hand: ",plyr_hnd)
                if plyr_score > 21:
                    # Player has busted. Loop breaks
                    print('You Bust, Dealer Wins.')
                    time.sleep(1)
                    print("Dealer's Hand",dlr_hnd)
                    break
            elif plyr_choice == 'stay':
                # Player chose to stay. Loop breaks
                break
            else:
                # Catch case repeats loop until a valid entry is entered
                print('Invalid Entry')

    # Check if Dealer Needs to Draw
    while True:
        if plyr_score >= 21:
            # Dealer does not need to draw because player already lost. Loop breaks
            break
            time.sleep(1)
        elif dlr_score <= 16:
            # Dealer draws as long as score is <= 16
            draw_card(dlr_hnd)
            print('Dealer drew a card: ',dlr_hnd)
            dlr_score = check_score(dlr_hnd)
            time.sleep(1)
        elif dlr_score > 21:
            print('Dealer Busts, You Win!')
            break
        else:
            time.sleep(1)
            print('Dealer Stays:',dlr_hnd)
            break

    # Determine Winner
    if plyr_score == 21 and dlr_score != plyr_score:
        print('Blackjack! (You Win)')
        time.sleep(1)
        print("Dealer's Hand: ",dlr_hnd)
    elif plyr_score < dlr_score and dlr_score <= 21:
        print('Dealer wins',dlr_score,'to',plyr_score)
    elif plyr_score > dlr_score and plyr_score < 21:
        print('You win',plyr_score,'to',dlr_score)
    elif plyr_score == dlr_score:
        print('Push (Draw)')

    time.sleep(1)
    plyr_restart = str(input("replay (y/n)?\n")).lower()
    if plyr_restart == "y":
        print("-----------------RESTARTING-----------------")
    elif plyr_restart == "n":
        break
    else:
        print('Invalid Entry')
