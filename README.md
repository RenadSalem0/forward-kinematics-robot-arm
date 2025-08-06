
# 🦾 Forward Kinematics Robotic Arm

## 📌 Overview
This document explains the forward kinematics of a 2-DOF planar robotic arm using **two standard methods**:
1. **Trigonometric method (sin/cos equations)**
2. **Transformation matrix method (Homogeneous matrices using DH parameters)**

Both approaches lead to the same goal: computing the position of the end-effector in Cartesian space based on joint angles and link lengths.

---

## 🧮 1. Trigonometric Method (Basic Forward Kinematics)

### 🔧 System Setup
- Two rotational joints
- Two links:  
  `L1`: Length of the first link  
  `L2`: Length of the second link
- Two joint angles:  
  `θ1`: Angle between the base and first link  
  `θ2`: Angle between the first and second link

### 🧠 Forward Kinematics Equations

Using basic trigonometry, the position of the end-effector `(x, y)` is given by:

```
x = L1 * cos(θ1) + L2 * cos(θ1 + θ2)
y = L1 * sin(θ1) + L2 * sin(θ1 + θ2)
```

> These equations work for a **planar 2D system** and are ideal for introductory robotics tasks or simulation.

---

## 🧠 2. Matrix Method using Homogeneous Transformations (DH Parameters)

### 🔄 Concept

In this method, we define a **transformation matrix** for each link, representing both rotation and translation relative to the previous frame.

Each transformation is a **4×4 homogeneous matrix**, and the position of the end-effector is found by multiplying the transformations:

```
T = T1 * T2
```

### 📐 Transformation Matrix for Each Joint

Let’s define the matrices for a planar 2-DOF arm using standard DH convention:

#### Frame 1 (base to link 1):
   ```math
  T1= \begin{bmatrix}
   \cos(\theta_1) & -\sin(\theta_1) & 0 & L1 \cos(\theta_1) \\
   \sin(\theta_1) & \cos(\theta_1) & 0 & L1 \sin(\theta_1) \\
   0 & 0 & 1 & 0 \\
   0 & 0 & 0 & 1 \\
   \end{bmatrix}
```

#### Frame 2 (link 1 to link 2):
   ```math
   T2= \begin{bmatrix}
   \cos(\theta_2) & -\sin(\theta_2) & 0 & L2 \cos(\theta_2) \\
   \sin(\theta_2) & \cos(\theta_2) & 0 & L2 \sin(\theta_2) \\
   0 & 0 & 1 & 0 \\
   0 & 0 & 0 & 1 \\
   \end{bmatrix}
```

### 🔄 Final Transformation

```
T = T1 * T2
```

The position of the end-effector will be in the last column of the result matrix `T`, specifically:

```
(x, y) = (T[0, 3], T[1, 3])
```

> This method is scalable and works for **any number of links or 3D robotic arms**.

---

## 🧭 When to Use Which?

| Scenario                          | Method                  |
|----------------------------------|--------------------------|
| Simple 2D robot (2-DOF)          | ✅ Trigonometric equations |
| Robotic simulation in ROS / MATLAB | ✅ Matrix method         |
| Systems with 3+ joints or 3D motion | ✅ Matrix method        |
| Academic assignments (limited scope) | ✅ Trigonometric method |

---
