import pygame
import random

# Initialize Pygame
pygame.init()

# Constants
WIDTH, HEIGHT = 800, 600
CELL_SIZE = 20
FPS = 10

# Colors
BLACK = (0, 0, 0)
GREEN = (0, 255, 0)
RED = (255, 0, 0)
WHITE = (255, 255, 255)

# Set up display
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption('Snake Game')

# Clock for controlling the frame rate
clock = pygame.time.Clock()

# Snake starting position and speed
snake = [(WIDTH // 2, HEIGHT // 2)]
direction = 'RIGHT'
change_to = direction
snake_speed = CELL_SIZE

# Food position
food_pos = (random.randint(0, (WIDTH - CELL_SIZE) // CELL_SIZE) * CELL_SIZE,
            random.randint(0, (HEIGHT - CELL_SIZE) // CELL_SIZE) * CELL_SIZE)

# Functions
def draw_snake(snake):
    for pos in snake:
        pygame.draw.rect(screen, GREEN, (pos[0], pos[1], CELL_SIZE, CELL_SIZE))

def move_snake():
    global direction

    if direction == 'UP':
        snake[0] = (snake[0][0], snake[0][1] - snake_speed)
    if direction == 'DOWN':
        snake[0] = (snake[0][0], snake[0][1] + snake_speed)
    if direction == 'LEFT':
        snake[0] = (snake[0][0] - snake_speed, snake[0][1])
    if direction == 'RIGHT':
        snake[0] = (snake[0][0] + snake_speed, snake[0][1])

def check_collision():
    if (snake[0][0] >= WIDTH or snake[0][0] < 0 or
            snake[0][1] >= HEIGHT or snake[0][1] < 0):
        return True

    for block in snake[1:]:
        if snake[0] == block:
            return True

    return False

def generate_food():
    return random.randint(0, (WIDTH - CELL_SIZE) // CELL_SIZE) * CELL_SIZE, \
           random.randint(0, (HEIGHT - CELL_SIZE) // CELL_SIZE) * CELL_SIZE

# Main game loop
running = True
while running:
    screen.fill(BLACK)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_UP and direction != 'DOWN':
                change_to = 'UP'
            if event.key == pygame.K_DOWN and direction != 'UP':
                change_to = 'DOWN'
            if event.key == pygame.K_LEFT and direction != 'RIGHT':
                change_to = 'LEFT'
            if event.key == pygame.K_RIGHT and direction != 'LEFT':
                change_to = 'RIGHT'

    # Change direction if allowed
    if change_to == 'UP' and direction != 'DOWN':
        direction = 'UP'
    if change_to == 'DOWN' and direction != 'UP':
        direction = 'DOWN'
    if change_to == 'LEFT' and direction != 'RIGHT':
        direction = 'LEFT'
    if change_to == 'RIGHT' and direction != 'LEFT':
        direction = 'RIGHT'

    # Move the snake
    move_snake()

    # Check for collision with the wall or itself
    if check_collision():
        running = False

    # Check if the snake eats the food
    if snake[0] == food_pos:
        snake.append((0, 0))
        food_pos = generate_food()

    # Draw food and snake
    pygame.draw.rect(screen, RED, (*food_pos, CELL_SIZE, CELL_SIZE))
    draw_snake(snake)

    pygame.display.flip()
    clock.tick(FPS)

pygame.quit()
