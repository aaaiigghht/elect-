import numpy as np
import matplotlib.pyplot as plt

# Параметри сигналу
U0 = 3 + 0.5 * 4  # амплітуда [В]
τi = 1  # тривалість імпульсу [мс]
T = (4 + 1) * τi  # період [мс]

# Кількість відображених гармонік у спектрі
num_harmonics = 10

# Функція для обчислення спектру
def spectrum(U0, τi, T, num_harmonics):
    harmonics = []
    amplitudes = []
    frequencies = []
    for i in range(1, num_harmonics + 1):
        harmonic = i * (1 / T)  # частота гармоніки
        amplitude = U0 * (τi / T) * np.sin(np.pi * i * τi / T) / (np.pi * i * τi / T)
        harmonics.append(harmonic)
        amplitudes.append(amplitude)
        frequencies.append(harmonic * 1000)  # переведення у герц

    return harmonics, amplitudes, frequencies

harmonics, amplitudes, frequencies = spectrum(U0, τi, T, num_harmonics)

# Малювання спектру
plt.stem(frequencies, amplitudes, use_line_collection=True)
plt.title('Спектр амплітуд прямокутних імпульсів')
plt.xlabel('Частота [Гц]')
plt.ylabel('Амплітуда')
plt.grid(True)
plt.show()
