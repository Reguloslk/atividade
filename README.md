import pygame
import sys

# Inicialização
pygame.init()

# Configuração da tela
LARGURA = 800
ALTURA = 600
tela = pygame.display.set_mode((LARGURA, ALTURA))
pygame.display.set_caption("Ping Pong")

# Cores
PRETO = (0, 0, 0)
BRANCO = (255, 255, 255)

# Raquete
raquete = pygame.Rect(50, 250, 15, 100)
velocidade_raquete = 7

# Bola
bola = pygame.Rect(390, 290, 20, 20)
vel_x = 5
vel_y = 5

# Placar
placar = 0
fonte = pygame.font.Font(None, 50)

# Relógio
clock = pygame.time.Clock()

# Loop principal
while True:

    # Eventos
    for evento in pygame.event.get():
        if evento.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    # Movimento da raquete
    teclas = pygame.key.get_pressed()

    if teclas[pygame.K_UP]:
        raquete.y -= velocidade_raquete

    if teclas[pygame.K_DOWN]:
        raquete.y += velocidade_raquete

    # Limites da raquete
    if raquete.top < 0:
        raquete.top = 0

    if raquete.bottom > ALTURA:
        raquete.bottom = ALTURA

    # Movimento da bola
    bola.x += vel_x
    bola.y += vel_y

    # Colisão com bordas superior e inferior
    if bola.top <= 0 or bola.bottom >= ALTURA:
        vel_y *= -1

    # Colisão com a raquete
    if bola.colliderect(raquete):
        vel_x *= -1

    # Bola saiu da área de jogo
    if bola.left <= 0:
        bola.center = (LARGURA // 2, ALTURA // 2)
        vel_x = 5
        vel_y = 5

    # Ponto marcado
    if bola.right >= LARGURA:
        placar += 1
        bola.center = (LARGURA // 2, ALTURA // 2)
        vel_x = -5
        vel_y = 5

    # Desenho
    tela.fill(PRETO)

    pygame.draw.rect(tela, BRANCO, raquete)
    pygame.draw.ellipse(tela, BRANCO, bola)

    texto = fonte.render(f"Placar: {placar}", True, BRANCO)
    tela.blit(texto, (300, 20))

    pygame.display.update()
    clock.tick(60)
