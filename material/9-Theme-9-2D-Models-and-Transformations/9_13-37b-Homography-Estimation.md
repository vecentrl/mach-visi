## 37b Homography Estimation
-->
![](162a-1.jpg)

### Preview

In this part, we learn how to **estimate a homography** from a set of point correspondences. This is essential for tasks like stitching images together, rectifying photos, or mapping one view of a plane to another.

---

### Homography estimation

To compute the homography, we need a set of **point correspondences** between two images:

* Each point \$(X\_i, Y\_i)\$ in the first image corresponds to \$(X'\_i, Y'\_i)\$ in the second image.
* These pairs form a system of linear equations that can be written in matrix form:

$$
M \cdot \mathbf{x} = \mathbf{b}
$$

where \$M\$ is a \$2n \times 8\$ matrix (constructed from the correspondences), \$\mathbf{x}\$ contains the unknown homography parameters, and \$\mathbf{b}\$ represents the transformed points.

![](162a-1.jpg)
*Figure: Matrix setup for homography estimation.*

The **least squares estimate** of the parameters is:

$$
\hat{\mathbf{x}} = (M^T M)^{-1} M^T \mathbf{b}
$$

Finally, the homography matrix has 9 elements, but since it is defined up to scale, one entry (usually \$a\_{33}\$) can be set to 1 for normalization.

---

### Recap

* Homography estimation requires at least **four point correspondences**.
* The problem can be expressed as a linear system solved with least squares.
* Homography is unique up to a scale factor, so one parameter is fixed (e.g., $a\_{33}=1$).

---

### Stop to think

Why do we normalize $a\_{33}$ to 1 when estimating the homography? What does this tell us about the scale of the transformation?

---




