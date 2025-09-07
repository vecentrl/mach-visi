## 44a  3D Transformations & Camera Models (part 1) s. 188–189
<!--
### 3D transformations 188
### Rigid transformation 189
### Euler angle representation 189 190
### Camera model 190
-->

### Preview
In this section, we extend affine transformations into 3D space and learn about rigid transformations, Euler angles, and camera models. You will see how mathematical matrices describe translations, rotations, and how cameras project 3D points into 2D images.

---

### 3D transformations

- Using homogeneous coordinates, 2D affine transformations can be extended to 3D.
- Mapping from a 3D point $P=(x, y, z)$ to a new point $P'=(x', y', z')$:

$$
\begin{bmatrix}
x' \\ y' \\ z' \\ 1
\end{bmatrix}
=
\begin{bmatrix}
a_{11} & a_{12} & a_{13} & a_{14} \\
a_{21} & a_{22} & a_{23} & a_{24} \\
a_{31} & a_{32} & a_{33} & a_{34} \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
x \\ y \\ z \\ 1
\end{bmatrix}
$$

- Coefficients $a_{11}, \dots, a_{34}$ can vary.
  - At least **6 point correspondences** are needed to estimate them.
- Rigid transformation (rotation + translation) is the most common case.
  - 6 degrees of freedom → needs **3 point correspondences**.
  - Represents the 3D pose.

---

### Rigid transformation

A rigid transformation preserves distances and angles.

$$
\begin{bmatrix}
x' \\ y' \\ z' \\ 1
\end{bmatrix}
=
\begin{bmatrix}
R & t \\
0 & 1
\end{bmatrix}
\begin{bmatrix}
x \\ y \\ z \\ 1
\end{bmatrix}
$$

- $R$ is a $3 \times 3$ rotation matrix.  
- $t$ is a $3 \times 1$ translation vector ($x_0, y_0, z_0$).  
- $R$ is orthonormal: $R^{-1} = R^T$.  
- Minimum parameters: 3.  
- Often parameterized with **Euler angles**.

---

### Euler angle representation

Rotations are expressed as:

- Rotation about x-axis (roll $\psi$):

$$
R_x(\psi) =
\begin{bmatrix}
1 & 0 & 0 \\
0 & \cos \psi & -\sin \psi \\
0 & \sin \psi & \cos \psi
\end{bmatrix}
$$

- Rotation about y-axis (pitch $\theta$):

$$
R_y(\theta) =
\begin{bmatrix}
\cos \theta & 0 & \sin \theta \\
0 & 1 & 0 \\
-\sin \theta & 0 & \cos \theta
\end{bmatrix}
$$

- Rotation about z-axis (yaw $\phi$):

$$
R_z(\phi) =
\begin{bmatrix}
\cos \phi & -\sin \phi & 0 \\
\sin \phi & \cos \phi & 0 \\
0 & 0 & 1
\end{bmatrix}
$$

---

### Euler angle representation (general)

A general 3D rotation matrix:

$$
R = R_z(\phi) R_y(\theta) R_x(\psi)
$$

Expanded:

$$
R =
\begin{bmatrix}
\cos \theta \cos \phi & \sin \psi \sin \theta \cos \phi - \cos \psi \sin \phi & \cos \psi \sin \theta \cos \phi + \sin \psi \sin \phi \\
\cos \theta \sin \phi & \sin \psi \sin \theta \sin \phi + \cos \psi \cos \phi & \cos \psi \sin \theta \sin \phi - \sin \psi \cos \phi \\
-\sin \theta & \sin \psi \cos \theta & \cos \psi \cos \theta
\end{bmatrix}
$$

- Decomposition is not unique → more than one angle set can describe the same orientation.
- Axis-angle representation:  
  - A unit vector $e$ defines the axis of rotation.  
  - Angle $\theta$ defines the magnitude.

---

### Camera model

The perspective camera model projects 3D points into 2D image coordinates.

$$
\begin{bmatrix}
s c \\ s r \\ s
\end{bmatrix}
=
M
\begin{bmatrix}
x \\ y \\ z \\ 1
\end{bmatrix}
=
\begin{bmatrix}
a_{11} & a_{12} & a_{13} & a_{14} \\
a_{21} & a_{22} & a_{23} & a_{24} \\
a_{31} & a_{32} & a_{33} & a_{34}
\end{bmatrix}
\begin{bmatrix}
x \\ y \\ z \\ 1
\end{bmatrix}
$$

- $(c, r)$ are the 2D image coordinates.  
- $s$ is a scale factor.  
- $c, r$ are computed by dividing the first two elements by the third.  
- Coefficients $a_{11}, \dots, a_{34}$ are estimated via **camera calibration**.

---

### Recap

- 3D affine transformations extend from 2D using homogeneous coordinates.  
- Rigid transformations combine translation and rotation.  
- Euler angles provide a convenient but sometimes ambiguous representation of rotation.  
- Camera models use projection matrices to map 3D points to 2D.  

---

### Reflective Question
How does camera calibration ensure that real-world 3D coordinates map correctly to 2D image pixels?

