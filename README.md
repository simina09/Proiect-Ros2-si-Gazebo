# 🤖 TurtleBot3 Penalty Kicker - Proiect ROS 2 & Computer Vision

## 📋 Descrierea Proiectului
Acest proiect reprezintă o aplicație avansată de robotică mobilă dezvoltată în **ROS 2 (Robot Operating System)** și simulată în **Gazebo**. Obiectivul principal este programarea unui robot autonom **TurtleBot3 Waffle Pi** capabil să identifice vizual o minge de fotbal (bazat pe culoare), să o urmărească și să execute o lovitură de pedeapsă (penalty) într-o poartă de fotbal, respectând reguli stricte de fizică și logică de control.

Proiectul integrează concepte fundamentale de:
* **Computer Vision** (procesare de imagine cu OpenCV).
* **Sisteme de Control** (Mașină de Stări Finită).
* **Simulare Fizică** (Gazebo, dinamică, coliziuni).
* **Automatizare** (Scripting Bash pentru resetare și randomizare).

---

## ✨ Funcționalități Cheie

1.  **Viziune Artificială în Timp Real:**
    * Utilizează camera robotului pentru a detecta mingea pe baza spațiului de culoare **HSV** (detectarea culorii roșii).
    * Algoritm de filtrare pentru eliminarea zgomotului de imagine.

2.  **Mașină de Stări Avansată (State Machine):**
    * **WAIT:** Calibrare inițială și așteptare pentru stabilizarea senzorilor.
    * **SEARCH:** Rotire pe loc pentru localizarea țintei.
    * **APPROACH:** Navigare proporțională către minge (centrare și avansare).
    * **BLIND KICK:** Logică de "memorie" pentru a continua șutul chiar și când mingea iese din câmpul vizual (în "punctul mort" de sub cameră).
    * **STOP:** Oprire de urgență sau finalizare misiune.

3.  **Detecție Automată a Golului:**
    * Monitorizează coordonatele absolute ale mingii în simulare.
    * Validează golul doar dacă mingea trece linia porții (`X < 0`) și se află între stâlpi (`-1.0 < Y < 1.0`).
    * Afișează mesaje distincte în terminal: `GOAL!!!` sau `MISS...`.

4.  **Sistem de Resetare Automatizat & Randomizat:**
    * Include un script Bash (`run_penalty.sh`) care permite resetarea rapidă a scenei fără repornirea Gazebo.
    * **Randomizare:** Robotul este generat la poziții ușor diferite la fiecare rulare (variație pe axele X și Y) pentru a testa robustețea algoritmului de viziune.

---

## 🛠️ Cerințe de Sistem (Prerequisites)

* **Sistem de Operare:** Ubuntu 22.04 (Jammy Jellyfish) sau similar.
* **Middleware:** ROS 2 Humble Hawksbill (sau Iron Irwini).
* **Simulator:** Gazebo Classic (versiunea 11+).
* **Pachete Dependente:**
    * `ros-<distro>-turtlebot3-gazebo`
    * `ros-<distro>-gazebo-ros-pkgs`
    * `python3-opencv`
    * `python3-numpy`

---

## 🚀 Instalare și Configurare

1.  **Crearea Spațiului de Lucru (Dacă nu există):**
    ```bash
    mkdir -p ~/ros2_ws/src
    cd ~/ros2_ws/src
    ```

2.  **Clonarea Proiectului:**
    ```bash
    git clone [https://github.com/Alex-Sefu/Proiect-Ros2-si-Gazebo.git](https://github.com/Alex-Sefu/Proiect-Ros2-si-Gazebo.git) turtlebot_penalty
    ```

3.  **Compilarea Pachetului:**
    ```bash
    cd ~/ros2_ws
    colcon build --packages-select turtlebot_penalty
    source install/setup.bash
    ```

4.  **Setarea Variabilei de Mediu:**
    ```bash
    export TURTLEBOT3_MODEL=waffle_pi
    ```

---

