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
