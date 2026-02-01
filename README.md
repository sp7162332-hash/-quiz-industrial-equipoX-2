# -quiz-industrial-equipoX-2
Descripcion

import tkinter as tk
import random

class QuizApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Quiz de Inventarios")
        self.root.geometry("500x350")

        # 🔹 PREGUNTAS INTEGRADAS EN EL CÓDIGO
        self.preguntas = [
            {
                "pregunta": "¿Qué es un inventario mínimo?",
                "opciones": [
                    "La mayor cantidad de productos que puede almacenar una empresa",
                    "La cantidad mínima de productos que debe haber para evitar faltantes",
                    "La cantidad total de productos vendidos"
                ],
                "correcta": 1
            },
            {
                "pregunta": "¿Qué representa el inventario máximo?",
                "opciones": [
                    "La cantidad mínima necesaria para operar",
                    "La cantidad total vendida en un periodo",
                    "El nivel más alto de existencias que se puede almacenar"
                ],
                "correcta": 2
            },
            {
                "pregunta": "¿Cuál es el objetivo principal de establecer inventarios mínimos y máximos?",
                "opciones": [
                    "Aumentar las ventas",
                    "Evitar sobrecostos y faltantes de productos",
                    "Eliminar la rotación de inventarios"
                ],
                "correcta": 1
            },
            {
                "pregunta": "¿Qué es la rotación de inventarios?",
                "opciones": [
                    "El movimiento físico de productos en el almacén",
                    "La frecuencia con la que se renueva el inventario en un periodo",
                    "La cantidad máxima de productos almacenados"
                ],
                "correcta": 1
            },
            {
                "pregunta": "Una rotación de inventarios alta indica que:",
                "opciones": [
                    "Los productos se venden lentamente",
                    "Hay exceso de inventario",
                    "Los productos se venden rápidamente"
                ],
                "correcta": 2
            },
            {
                "pregunta": "¿Qué problema puede causar una rotación de inventarios baja?",
                "opciones": [
                    "Falta de productos",
                    "Acumulación y obsolescencia de mercancía",
                    "Aumento en las ventas"
                ],
                "correcta": 1
            },
            {
                "pregunta": "¿Qué es la reposición de inventarios?",
                "opciones": [
                    "La venta de productos",
                    "El proceso de volver a surtir los productos faltantes",
                    "El conteo físico del almacén"
                ],
                "correcta": 1
            },
            {
                "pregunta": "¿Cuándo se debe realizar la reposición de existencias?",
                "opciones": [
                    "Cuando el inventario llega al nivel mínimo",
                    "Cuando el almacén está lleno",
                    "Al final del año únicamente"
                ],
                "correcta": 0
            },
            {
                "pregunta": "¿Qué es el control de existencias?",
                "opciones": [
                    "La supervisión y registro de entradas y salidas de productos",
                    "El traslado de mercancía",
                    "El aumento del inventario máximo"
                ],
                "correcta": 0
            },
            {
                "pregunta": "¿Cuál es una consecuencia financiera de mantener inventarios excesivos?",
                "opciones": [
                    "Aumento de la liquidez",
                    "Mayor capital inmovilizado y costos operativos",
                    "Incremento en la rotación de inventarios"
                ],
                "correcta": 1
            }
        ]

        self.indice = 0
        self.puntos = 0
        self.preguntas_juego = []

        self.label_pregunta = tk.Label(root, text="", wraplength=450, font=("Arial", 12))
        self.label_pregunta.pack(pady=20)

        self.botones = []
        for i in range(3):
            btn = tk.Button(root, width=50, command=lambda i=i: self.verificar(i))
            btn.pack(pady=5)
            self.botones.append(btn)

        self.label_resultado = tk.Label(root, text="", font=("Arial", 11))
        self.label_resultado.pack(pady=10)

        self.boton_reiniciar = tk.Button(root, text="Reiniciar", command=self.iniciar_juego)
        self.boton_reiniciar.pack(pady=10)

        self.iniciar_juego()

    def iniciar_juego(self):
        self.puntos = 0
        self.indice = 0
        self.label_resultado.config(text="")
        self.preguntas_juego = random.sample(self.preguntas, 4)
        self.mostrar_pregunta()

    def mostrar_pregunta(self):
        if self.indice >= len(self.preguntas_juego):
            calificacion = (self.puntos / 4) * 10
            self.label_pregunta.config(text="RESULTADO FINAL")
            for btn in self.botones:
                btn.pack_forget()
            self.label_resultado.config(
                text=f"Puntos: {self.puntos} / 4\nCalificación: {calificacion}"
            )
            return

        p = self.preguntas_juego[self.indice]
        self.label_pregunta.config(text=p["pregunta"])

        for i, opcion in enumerate(p["opciones"]):
            self.botones[i].config(text=opcion)
            self.botones[i].pack(pady=5)

    def verificar(self, respuesta):
        if respuesta == self.preguntas_juego[self.indice]["correcta"]:
            self.puntos += 1
        self.indice += 1
        self.mostrar_pregunta()


# ▶️ Ejecutar aplicación
root = tk.Tk()
app = QuizApp(root)
root.mainloop()
