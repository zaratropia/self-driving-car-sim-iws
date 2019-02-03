# Übung zum autonomen Fahren im Informatik-Workshop (Master)
#### Wintersemester 18/19 - Hochschule Mannheim


## Simulator und Installation
[Simulator (Version 2)](https://github.com/udacity/self-driving-car-sim#term-1)

Installation der Umgebung geht nur einfach wenn `conda` installiert ist! Ansonten müssen alle benötigenten Pakete in der passenden Version manuell installiert werden..

Befehl: `conda create env -f environment[-gpu].yml`

## Training

[Forschungsarbeit von NVIDIA](https://images.nvidia.com/content/tegra/automotive/images/2016/solutions/pdf/end-to-end-dl-using-px.pdf)

Der relevante Quellcode befindet sich in der `model.py`. Hier müssen zu erst noch einige Zeilen ergänzt werden. Im folgenden findet ihr einige Hinweise dazu.

### Snippets Schichten im CNN

**Convolution Layer**
```python
model.add(Convolution2D(kernel_count, kernel_x, kernel_y, border_mode='same', subsample=(X, X))) 
model.add(Activation(activation_relu))
```
*Hinweis: Subsampling ist 2x2 in den ersten drei Ebenen, danach 1x1*

**Pooling Layer**
```python
model.add(MaxPooling2D(pool_size=(2, 2), strides=(1, 1)))
```

**Fully-Connected Layer**
```python
model.add(Dense(neron_count))
model.add(Activation(activation_relu))
```
*Wichtig: Pfad zu aufgezeichneten Trainingsbildern und Lenkdaten (CSV) in der `helper.py` anpassen!*

Training starten: `python model.py`


## Autonomes Fahren

Nun zur `drive.py`, diese steuert später das Fahrzeug. Wichtig ist hier vor allem die Funktion `telemetry`. In ihr werden die eingehnden Daten verarbeitet und die neuen Lenkdaten vorhergesagt. Zum besseren Verständnis empfiehlt es sich, sich einmal die Ausgaben des Funktionsparameters `data` ausgeben zu lassen.

Anschließend sollte es möglich sein die entsprechenden Variablen zu befüllen und die Funktion zu vervollständigen. Mit dem `throttle`-Paramter darf gerne experimentiert werden. 

Hinweis: 
```python 
print('Hallo, ich habe 5 Nachkomma-Stellen: {:.5f}'.format(0.167341324))`
```

Autonomes Fahren: `python drive.py model.json`

*Wichtig: Simulator muss im 'Autonomous Mode' sein*

