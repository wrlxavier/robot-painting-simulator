# Robot Painting Simulator 🤖🎨

Simulation of a KUKA LBR iiwa robotic manipulator painting images on a whiteboard pixel by pixel. Developed as a practical project for the Robotic Manipulators course at UFMG.

## 📋 Overview

This project simulates a 7-DOF robotic manipulator drawing images on a flat whiteboard. The robot converts any input image into a pixel matrix, paints each pixel with the appropriate color, and automatically changes brushes when needed.

## 🚀 Quick Start

Open the Jupyter notebook in Google Colab and run all cells:

```
pip install uaibot numpy pillow scikit-learn matplotlib tqdm
```

Upload your image when prompted, and watch the robot paint it!

## 🧠 How It Works

### 1. Image Processing
- **Color Quantization**: K-Means clustering reduces the image to 6 colors maximum
- **Resizing**: Image is resized to 16×16 pixels using nearest neighbor interpolation
- **Conversion**: RGB values are converted to hexadecimal color codes

### 2. Robot Control
- **Kinematic Control**: Uses geometric Jacobian and task-space control
- **Task Function**: Computes position error (3D) and partial orientation error (z-axis alignment)
- **Redundancy Resolution**: Pseudo-inverse of Jacobian handles 7-DOF to 4-DOF task mapping
- **Collision Avoidance**: Each configuration is checked for collisions before execution

```
# Control loop
qdot_d = pinv(Jacobian) @ (-K * error)
q_next = q + qdot_d * dt
```

### 3. Painting Logic
```
For each pixel:
    If color changed:
        → Return to safe position
        → Go to paint box
        → Change brush
        → Return to safe position
    
    → Position above pixel
    → Move down perpendicular to paint
    → Move up and continue
```

The end-effector is always kept normal to the board surface during painting movements.

## 📐 Main Components

**`ImageProcessor`**: Handles image loading, color reduction, resizing, and conversion to color matrix

**`PainterBoard`**: Creates the virtual whiteboard with 16×16 pixels and support structures

**`RobotController`**: Implements kinematic control with Jacobian-based task-space navigation

## 🎥 Demo

[Simulação de Pintura Robótica com KUKA LBR iiwa | Trabalho Prático - Manipuladores Robóticos | UFMG](https://youtu.be/Tk786zbliZo?si=Shiz0o4R63XhgrDt)

## 🛠️ Technologies

- **UAIBot**: Robotic simulation framework
- **Python**: NumPy, PIL, scikit-learn, Matplotlib
- **Robot**: KUKA LBR iiwa (7-DOF collaborative manipulator)

## 📚 Course

Robotic Manipulators | UFMG | Prof. Vinicius Mariano Gonçalves | Dec 2025

## 📝 License

MIT License - See [LICENSE](https://github.com/wrlxavier/robot-painting-simulator/blob/main/LICENSE) for details

---

⭐ Star this repo if you found it interesting!
