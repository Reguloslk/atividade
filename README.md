# atividade
import turtle

# Configuração da janela
tela = turtle.Screen()
tela.title("Ping Pong Simples")
tela.bgcolor("black")
tela.setup(width=800, height=600)

# Raquete esquerda
raquete = turtle.Turtle()
raquete.speed(0)
raquete.shape("square")
raquete.color("white")
raquete.shapesize(stretch_wid=5, stretch_len=1)
raquete.penup()
raquete.goto(-350, 0)

# Bola
bola = turtle.Turtle()
bola.speed(0)
bola.shape("circle")
bola.color("white")
bola.penup()
bola.goto(0, 0)

# Movimento da bola
bola.dx = 0.2
bola.dy = 0.2

# Movimentos da raquete
def subir():
    y = raquete.ycor()
    raquete.sety(y + 20)

def descer():
    y = raquete.ycor()
    raquete.sety(y - 20)

# Teclas
tela.listen()
tela.onkeypress(subir, "w")
tela.onkeypress(descer, "s")

# Loop principal
while True:
    tela.update()

    bola.setx(bola.xcor() + bola.dx)
    bola.sety(bola.ycor() + bola.dy)

    # Bater nas bordas superior e inferior
    if bola.ycor() > 290 or bola.ycor() < -290:
        bola.dy *= -1

    # Bater na raquete
    if (bola.xcor() < -340 and
        bola.xcor() > -350 and
        raquete.ycor() - 50 < bola.ycor() < raquete.ycor() + 50):
        bola.dx *= -1

    # Reinicia a bola se passar da raquete
    if bola.xcor() < -390 or bola.xcor() > 390:
        bola.goto(0, 0)
        bola.dx *= -1
