# snake

```
import random
import os
import time
import msvcrt  # działa na Windows

# Rozmiar planszy
WIDTH = 20
HEIGHT = 10

# Początkowa pozycja węża
snake = [(5, 5)]
direction = (1, 0)  # start w prawo

# Jedzenie
food = (random.randint(1, WIDTH-2), random.randint(1, HEIGHT-2))

def clear():
    os.system("cls")

def draw():
    clear()
    for y in range(HEIGHT):
        for x in range(WIDTH):
            if (x, y) in snake:
                print("O", end="")
            elif (x, y) == food:
                print("*", end="")
            elif x == 0 or x == WIDTH-1 or y == 0 or y == HEIGHT-1:
                print("#", end="")
            else:
                print(" ", end="")
        print()
    print("Sterowanie: W A S D")

def move():
    global food
    head_x, head_y = snake[0]
    dx, dy = direction
    new_head = (head_x + dx, head_y + dy)

    # Kolizja ze ścianą lub sobą
    if (new_head in snake or
        new_head[0] == 0 or new_head[0] == WIDTH-1 or
        new_head[1] == 0 or new_head[1] == HEIGHT-1):
        print("💀 GAME OVER!")
        exit()

    snake.insert(0, new_head)

    if new_head == food:
        food = (random.randint(1, WIDTH-2), random.randint(1, HEIGHT-2))
    else:
        snake.pop()

while True:
    draw()

    if msvcrt.kbhit():
        key = msvcrt.getch().decode("utf-8").lower()
        if key == "w":
            direction = (0, -1)
        elif key == "s":
            direction = (0, 1)
        elif key == "a":
            direction = (-1, 0)
        elif key == "d":
            direction = (1, 0)

    move()
    time.sleep(0.15)

```


Krzyżyk kółko

```
import random

def print_board(board):
    print()
    print(f" {board[0]} | {board[1]} | {board[2]}")
    print("---+---+---")
    print(f" {board[3]} | {board[4]} | {board[5]}")
    print("---+---+---")
    print(f" {board[6]} | {board[7]} | {board[8]}")
    print()

def check_winner(board, player):
    win_positions = [
        [0,1,2], [3,4,5], [6,7,8],  # wiersze
        [0,3,6], [1,4,7], [2,5,8],  # kolumny
        [0,4,8], [2,4,6]            # przekątne
    ]
    for pos in win_positions:
        if board[pos[0]] == board[pos[1]] == board[pos[2]] == player:
            return True
    return False

def is_draw(board):
    return " " not in board

def player_move(board):
    while True:
        try:
            move = int(input("Wybierz pole (1-9): ")) - 1
            if move in range(9) and board[move] == " ":
                board[move] = "X"
                break
            else:
                print("Nieprawidłowy ruch, spróbuj ponownie.")
        except ValueError:
            print("Wpisz liczbę od 1 do 9.")

def computer_move(board):
    available = [i for i in range(9) if board[i] == " "]
    move = random.choice(available)
    board[move] = "O"
    print(f"Komputer wybrał pole {move + 1}")

def main():
    board = [" "] * 9
    print("Gra w kółko i krzyżyk!")
    print_board(board)

    while True:
        player_move(board)
        print_board(board)
        if check_winner(board, "X"):
            print("Wygrałeś! 🎉")
            break
        if is_draw(board):
            print("Remis!")
            break

        computer_move(board)
        print_board(board)
        if check_winner(board, "O"):
            print("Komputer wygrał!")
            break
        if is_draw(board):
            print("Remis!")
            break

if __name__ == "__main__":
    main()

```

Rzut kością

```
import random

print("🎲 Gra: Rzut kością")

while True:
    input("Naciśnij Enter, aby rzucić kością (lub wpisz q aby wyjść): ")
    
    wynik = random.randint(1, 6)
    print(f"Wynik rzutu: {wynik}")
    
    wyjscie = input("Czy chcesz rzucić ponownie? (t/n): ")
    if wyjscie.lower() != "t":
        print("Koniec gry!")
        break

```

