## CT Image Reconstruction
This assignment focuses on reconstructing an image from a set of parallel projections, a technique commonly used in computed tomography (CT). 

The acquisition process involves transforming an image of size `l × l`, which we aim to recover, into a sinogram of size `n × l`. 

This measurement process is linear, so the process can be mathematically expressed as: `y= Ax`


Here, `y` is the vectorized sinogram image, `x` is the vectorized image we are reconstructing, and `A` is the image formation operator. 
However, in real-world scenarios, measurements are affected by noise, which is modeled as:
`y_η = Ax + η`
where `y_η` represents the noisy measurements and `η` is the measurement noise.

**INTRO:**

How are matrices related to CT sinograms?
- The sinogram is a 2D representation of projections obtained by scanning an object from multiple angles
- Each row in the sinogram corresponds to projections of the object at a specific angle
- The goal is to reconstruct the origin image from the sinogram (the image which we want) by solving the inverse problem
- Mathematically: this involves back-projection, or solving `Ax=y`, where x is the image we want and y is the measured data (sinogram)
- The more angles we have (denser sinograms), the better the reconstruction is (explored in problem 1a).

**IN SHORT**:
The sinogram captures projections at all angles, and the inverse problem reconstructs the image by combining these projection

**1. Difficulties of inverse problems**
- Reconstructing an image from data is challenging because `A` is not always invertible.
- To address this, we use `A=ATA`, where increasing the number of projection angles improves stability by enhancing the matrix's ability to capture image details.
- Instead of computing the inverse, which is inefficient for sparse or singular matrices, the pseudo-inverse provides a practical approximation.
- However, as noise increases, the reconstructed images become blurrier, highlighting the trade-off between noise and reconstruction quality.
  
**2. Variational reconstruction**
- In this problem, we reconstruct an image from noisy measurements by solving a minimization problem.
- This problem is now more scalable to solve because it avoids directly inverting large or ill-conditioned matrices 
- To improve stability and avoid overfitting, we introduce a regularization term into the minimization problem.
- The regularization term improves stability by controlling the solution's complexity and reducing sensitivity to noise or errors in the data

**3. Optimization**
- We now use iterative algorithms—Gradient Descent and Conjugate Gradient—to solve the problem efficiently.
- These methods are ideal for large matrices `A` because they avoid explicitly forming `ATA` or computing its inverse.
- Iterative methods progressively refine the solution `x` using only matrix-vector products `Ax` and `ATy` which are computationally efficient, especially for sparse `A`
- As a result, the reconstructed image is more stable and accurate compared to the methods in part 1.

**4. Model Refinement**
- We incorporate **l2-regularization** and **l1-regularization** to improve stability and avoid overfitting.  
- **l2-regularization** penalizes large values in the solution, promoting smoothness and stability.  
- **l1-regularization** encourages **sparsity**, making most elements of  `x` zero, which is useful when the solution is expected to be sparse (e.g., images with few nonzero pixels).  
- Combining these techniques helps refine the reconstruction and improves image quality, even in the presence of noise.


*This project is inspired by coursework in optimization and inverse problems for imaging systems*
