# Digital_daino
import pygame

import random

# Set up the window

WINDOW_WIDTH = 800

WINDOW_HEIGHT = 400

window = pygame.display.set_mode((WINDOW_WIDTH, WINDOW_HEIGHT))

pygame.display.set_caption('Dinosaur Game')

# Load images

dinosaur_image = pygame.image.load('dinosaur.png')

cactus_image = pygame.image.load('cactus.png')

# Set up the dinosaur

dinosaur_x = 50

dinosaur_y = WINDOW_HEIGHT - 100

dinosaur_speed = 0

dinosaur_acceleration = 1

# Set up the cactus

cactus_x = WINDOW_WIDTH

cactus_y = WINDOW_HEIGHT - 100

# Set up the game loop

game_over = False

clock = pygame.time.Clock()

# Game loop

while not game_over:

    # Event handling

    for event in pygame.event.get():

        if event.type == pygame.QUIT:

            game_over = True

        elif event.type == pygame.KEYDOWN:

            if event.key == pygame.K_SPACE:

                dinosaur_speed = -10

    # Move the dinosaur

    dinosaur_y += dinosaur_speed

    dinosaur_speed += dinosaur_acceleration

    # Move the cactus

    cactus_x -= 5

    if cactus_x < -50:

        cactus_x = WINDOW_WIDTH

        cactus_y = random.randint(WINDOW_HEIGHT - 150, WINDOW_HEIGHT - 50)

    # Check for collisions

    dinosaur_rect = pygame.Rect(dinosaur_x, dinosaur_y, 50, 50)

    cactus_rect = pygame.Rect(cactus_x, cactus_y, 50, 50)

    if dinosaur_rect.colliderect(cactus_rect):

        game_over = True

    # Draw the game

    window.fill((255, 255, 255))

    window.blit(dinosaur_image, (dinosaur_x, dinosaur_y))

    window.blit(cactus_image, (cactus_x, cactus_y))

    pygame.display.update()

    # Set the game speed

    clock.tick(60)

# Clean up

pygame.quit()

