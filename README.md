
import pygame
import sys
import math

# Inicializando o Pygame
pygame.init()

# Definindo as dimensões da janela
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Bandeira do Brasil em Movimento")

# Definindo cores
GREEN = (0, 156, 59)
YELLOW = (255, 223, 0)
BLUE = (0, 39, 118)
WHITE = (255, 255, 255)

# Função para desenhar a bandeira do Brasil
def draw_flag(surface, x_offset, wave_amplitude):
    surface.fill(GREEN)  # Fundo verde

    # Calculando a oscilação
    wave = [
        (x, int(math.sin((x + x_offset) * 0.02) * wave_amplitude))
        for x in range(-WIDTH // 2, WIDTH // 2)
    ]

    # Desenhando o losango amarelo
    pygame.draw.polygon(
        surface, YELLOW,
        [(400, 200 + wave[200][1]), (600, 300 + wave[400][1]), 
         (400, 400 + wave[200][1]), (200, 300 + wave[0][1])]
    )

    # Desenhando o círculo azul
    pygame.draw.circle(surface, BLUE, (400, 300 + wave[200][1]), 80)

    # Desenhando a faixa branca
    pygame.draw.arc(surface, WHITE, (320, 220, 160, 160), math.radians(30), math.radians(150), 5)

    # Adicionando texto "Ordem e Progresso"
    font = pygame.font.SysFont("arial", 20, bold=True)
    text = font.render("ORDEM E PROGRESSO", True, WHITE)
    text_rect = text.get_rect(center=(400, 270))
    surface.blit(text, text_rect)

# Loop principal
clock = pygame.time.Clock()
wave_offset = 0
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    # Atualizando o deslocamento da onda
    wave_offset += 2

    # Desenhando a bandeira
    draw_flag(screen, wave_offset, wave_amplitude=15)

    # Atualizando a tela
    pygame.display.flip()
    clock.tick(30)
