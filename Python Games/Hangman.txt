import time
import random

restart = 0
while restart != 1:
    # Store Images as Functions
            def hang0():
                print('')
                print('')
                print('')
                print('')
                print('')
                print('')
                print('')
                print('____________________\n')

            def hang1():
                print('')
                print('   |')
                print('   |')
                print('   |')
                print('   |')
                print('   |')
                print('   |')
                print('___|________________\n')

            def hang2():
                print('')
                print('   |  /')
                print('   | /')
                print('   |/')
                print('   |')
                print('   |')
                print('   |')
                print('___|________________\n')

            def hang3():
                print('____________________')
                print('   |  /')
                print('   | /')
                print('   |/')
                print('   |')
                print('   |')
                print('   |')
                print('___|________________\n')

            def hang4():
                print('____________________')
                print('   |  /     |')
                print('   | /     (_)')
                print('   |/')
                print('   |')
                print('   |')
                print('   |')
                print('___|________________\n')

            def hang5():
                print('____________________')
                print('   |  /     |')
                print('   | /     (_)')
                print('   |/       |')
                print('   |        |')
                print('   |')
                print('   |')
                print('___|________________\n')

            def hang6():
                print('____________________')
                print('   |  /     |')
                print('   | /     (_)')
                print('   |/      /|\ ')
                print('   |      / | \ ')
                print('   |')
                print('   |')
                print('___|________________\n')

            def hang7():
                print('____________________')
                print('   |  /     |')
                print('   | /     (_)')
                print('   |/      /|\ ')
                print('   |      / | \ ')
                print('   |       / \ ')
                print('   |      /   \ ')
                print('___|________________')

            # Puts Images in List to be Called Upon by their Index
            hang_list = [hang0, hang1, hang2, hang3, hang4, hang5, hang6, hang7]

            # Import and Store "States" Category List
            states1 = open('states.txt','r')
            line = 'Gallows Pole'
            states_pool = []
            while line != '':
                line = states1.readline()
                line = line.strip('\n').lower()
                states_pool.append(line)
            states1.close()

            # Import and Store "Countries" Category List
            countries1 = open('Countries.txt','r')
            line = 'Gallows Pole'
            countries_pool = []
            while line != '':
                line = countries1.readline()
                line = line.strip('\n').lower()
                countries_pool.append(line)    
            countries1.close()

            # Import and Store "Baby Animals" Category List
            babyanimals1 = open('babyanimals.txt','r')
            line = 'Gallows Pole'
            baby_animals_pool = []
            while line != '':
                line = babyanimals1.readline()
                line = line.strip('\n').lower()
                baby_animals_pool.append(line)    
            babyanimals1.close()

            # Removes Last Entry Because it's Blank. Couldn't Think of a Better Way
            states_pool.pop(len(states_pool) - 1)
            countries_pool.pop(len(countries_pool) - 1)
            baby_animals_pool.pop(len(baby_animals_pool) - 1)

            # Asks User to Choose Category
            while True:
                plyr_category = str(input('Select a Category: States (U.S.), Countries, Baby Animals, or Random\n')).lower()
                if plyr_category == 'states' or plyr_category == 'us states' or plyr_category == 'u.s. states':
                    playlist = states_pool
                    break
                elif plyr_category == 'countries':
                    playlist = countries_pool
                    break
                elif plyr_category == 'baby animals' or plyr_category == 'animals' or plyr_category == 'babyanimals':
                    playlist = baby_animals_pool
                    break
                elif plyr_category == 'random':
                    ran_pool = [states_pool, countries_pool, baby_animals_pool]
                    playlist = random.choice(ran_pool)
                    break
                else:
                    print('Invalid Entry')
                    time.sleep(1)

            # Shuffle Chosen list and Pop Random Index (Double-Random)
            x = random.randint(1,len(playlist)-1)
            random.shuffle(playlist)
            game_word = playlist.pop(x)

            # Non-essential Code
            time.sleep(0.25)
            print('Excellent!')
            time.sleep(1.5)
            print('Okay, I have Chosen a Word.')
            time.sleep(1)

            # Player Selects Difficulty and Given Corresponding Number of Lives
            plyr_lives = 1
            while True:
                plyr_difficulty = str(input('Select a Difficulty: Easy, Medium, or Hard\n')).lower()
                if plyr_difficulty == 'easy' or plyr_difficulty == 'ez':
                    plyr_lives += 6
                    hang_ind = 0
                    break
                elif plyr_difficulty == 'medium':
                    plyr_lives += 4
                    hang_ind = 2
                    break
                elif plyr_difficulty == 'hard':
                    plyr_lives += 2
                    hang_ind = 4
                    break
                # Hidden Extreme difficulty ;)
                elif plyr_difficulty == 'extreme':
                    time.sleep(0.5)
                    print('Looks like you found my hidden challenge! You get 1 strike, good luck!\n')
                    time.sleep(2)
                    hang_ind = 6
                    break
                else:
                    print('Invalid Entry')
                    time.sleep(1)

            # Creates Corresponding Spaces for Game Word        
            spaces = []
            for i in game_word:
                if i == ' ':
                    i = ' '
                else:
                    i = '_'
                spaces += i
                
            # Actual Game, Asks for Letter as Long as Player Has Lives
            lttr_pool = str('abcdefghijklmnopqrstuvwxyz0')
            guessed_lttrs = ''
            while plyr_lives != 0 and (''.join(spaces) == game_word) == False:
                print('Guessed Letters:', guessed_lttrs)
                hang_list[hang_ind]()
                print('Your Word: ',''.join(spaces),'\nLives:',plyr_lives)
                while True:
                    plyr_guess = str(input('Guess a Letter: ')).lower()
                    switch = 0
                    if plyr_guess.isalpha() == True and len(plyr_guess) < 2:
                        for i in lttr_pool:
                            # Runs if Guess is New
                            if i == plyr_guess:
                                lttr_pool = lttr_pool.replace(plyr_guess,' ')
                                guessed_lttrs += plyr_guess + ' '
                                wd_ind = 0
                                for i in game_word:
                                    if i == plyr_guess:
                                        for i in spaces:
                                            spaces[wd_ind] = plyr_guess
                                            switch = 1
                                            break
                                    wd_ind += 1
                                if switch == 1:
                                    time.sleep(0.5)
                                    print('Correct!')
                                    time.sleep(0.5)
                                else:
                                    time.sleep(0.5)
                                    print('"'+plyr_guess+'"','is not in The Word')
                                    plyr_lives -= 1
                                    hang_ind += 1
                                    time.sleep(0.5)
                                break
                            # Rejects if Letter Already Guessed
                            elif i == '0':
                                print('You Already Guessed','"'+plyr_guess+'"')
                                break
                        break
                    else:
                        print('Guess Single Letter Only')
                        time.sleep(1)
            if plyr_lives == 0:
                print('Guessed Letters:', guessed_lttrs)
                hang_list[hang_ind]()
                print('Your Word: ',''.join(spaces),'\nLives:',plyr_lives)
                print('Game Over, You Lose!')
            elif plyr_lives != 0:
                print('You Win!')
            time.sleep(1)
            print('The Word was:',game_word)

            while True:
                replay = str(input('Play Again? (y/n): ')).lower()
                if replay == 'y' or replay == 'yes':
                    restart = 0
                    time.sleep(0.25)
                    print("That's What I Like to Hear!")
                    time.sleep(1)
                    print('\n')
                    break
                elif replay == 'n' or replay == 'no':
                    restart = 1
                    if plyr_lives == 0:
                        time.sleep(0.25)
                        print('Way to Be a Sore Loser.')
                    else:
                        print('Thanks for Playing!')
                    break
                else:
                    print('Invalid Entry')
                    time.sleep(1)
