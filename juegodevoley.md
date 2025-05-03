# Partido de voley!

This is your README. READMEs are where you can communicate what your project is and how to use it.

Write your name on line 6, save it, and then head back to GitHub Desktop.
import random

class Equipo:
    def __init__(self, nombre):
        self.nombre = nombre
        self.partidosGanados = 0
        self.partidosPerdidos = 0
        self.setGanados = 0

    def reset_set(self):
        self.setGanados = 0


# Crear dos equipos
equipo1 = Equipo("Tiburones")
equipo2 = Equipo("Águilas")


def RegistraSet(ganador):
    global equipo1, equipo2
    if ganador == 1:
        equipo1.setGanados += 1
        if equipo1.setGanados == 3:
            equipo1.partidosGanados += 1
            equipo2.partidosPerdidos += 1
            equipo1.reset_set()
            equipo2.reset_set()
    elif ganador == 2:
        equipo2.setGanados += 1
        if equipo2.setGanados == 3:
            equipo2.partidosGanados += 1
            equipo1.partidosPerdidos += 1
            equipo1.reset_set()
            equipo2.reset_set()


def Puntos():
    return random.randint(10, 28)


def PuntosExtras():
    return random.randint(0, 6)


def JugarPartido():
    global equipo1, equipo2

    while equipo1.setGanados < 3 and equipo2.setGanados < 3:
        puntos1 = Puntos()
        puntos2 = Puntos()

        while True:
            if puntos1 >= 25 and puntos1 > puntos2:
                RegistraSet(1)
                break
            elif puntos2 >= 25 and puntos2 > puntos1:
                RegistraSet(2)
                break
            else:
                puntos1 += PuntosExtras()
                puntos2 += PuntosExtras()


def ResultadoTorneo():
    print("\nResultados del Torneo:")
    print(f"{equipo1.nombre} - Ganados: {equipo1.partidosGanados}, Perdidos: {equipo1.partidosPerdidos}")
    print(f"{equipo2.nombre} - Ganados: {equipo2.partidosGanados}, Perdidos: {equipo2.partidosPerdidos}")


# Programa principal
if __name__ == "__main__":
    try:
        cantidad_partidos = int(input("¿Cuántos partidos deben jugar los equipos?: "))
        for _ in range(cantidad_partidos):
            JugarPartido()
        ResultadoTorneo()
    except ValueError:
        print("Por favor, ingrese un número entero válido.")
