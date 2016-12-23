---
layout: post
title: Solving Hydrogen atom numerically with 14 lines of Matlab code
tags: 
- quantum mechanics
---

Let's have a look the code first(They were wrote by Mikael Kuisma in [this vedio](https://www.youtube.com/watch?v=bW44gCulrvI)):

{% highlight matlab %}
g = 40; g3 = g^3;
p = linspace(-4, 4, g);         % one dimensiton space lattice
[X, Y, Z] = meshgrid(p, p, p);  % three dimension space lattice
h = p(2) - p(1);                % latice spacing
X = X(:); Y = Y(:); Z = Z(:);   % all elements of arraty as a single column
R = sqrt(X.^2 + Y.^2 + Z.^2);   % distance from the center
Vext = -1 ./ R;                 % potential energy
e = ones(g,1);               
L = spdiags([e -2*e e], -1:1, g, g) / h^2; % 1D finite difference Laplacian
I = speye(g);
L3 = kron(kron(L,I), I) + kron(kron(I, L), I) + kron(kron(I, I), L);  % extend Laplacian to 3 D
H = -0.5 * L3 + spdiags(Vext, 0, g3, g3);  % Hamiltonian of H atom
[PSI,E] = eigs(H, 1, 'sa');                      % Smallest eigenvalue of H
%disp(['Total energy for Hydrogen atom' num2str(E*27.21, 5) 'eV']); %display result
%PSI_3 = reshape(PSI, [g,g,g]);
scatter3(X,Y,Z,PSI.^2 *9000);
{% endhighlight %}

These code calculated the  ground state energy of Hydrogen atom(You can run the code online in [this website](http://www.tutorialspoint.com/matlab/try_matlab.php)).

Result: ![Electron density](/public/blogfigure/Hydrogen_lowest.png)

Energy: 13.321eV

## Theory

The Hamiltonian of electron in the Hydrogen is (in [Atomic units](http://en.wikipedia.org/wiki/Atomic_units)):

$$
H =  -\frac{1}{2} \nabla^2 - \frac{1}{r}
$$

In order to calculate the energy levels and wave functions of Hydrogen, we have to solve the t-independent Schrodinger equation of the electron in a Hydrogen atom is

$$
 H \psi_n = E_n \psi_n
$$

Generally speaking, $$H$$ is an Oprator, $$E_n$$ is its eigenvalues and $$\psi_n$$ is the corresponding eigenvactors.
In continus space, the Hamiltonian is complicated as it contains second derivatives(the Laplacian: $$\nabla^2$$). 

However, if we discretize the space, the wave function becomes a column vector, and the Hamiltonian can be expresse'd as
a matrix. As it is an opration on the vector. 
In this way, the problem is transformed to "find eigenvactors and eigenvalues of a matrix". And matlab is an expert about this kind of job.

In order to get this matrix form of $$H$$, the hard part is to the Laplacian. And [this link](http://en.wikipedia.org/wiki/Kronecker_sum_of_discrete_Laplacians) 
tells you how to get the "discrete Laplacians".

## Code explanation

Comment by the code owner:

    There is a special trick with the grids. We take a 3d grid with dimensions g times g times g. 
    We flatten the 3d-array to a vector of dimensions 1 x g^3. 
    The hamiltonian operator is a linear mapping in this vector space, 
    thus a g^3 x g^3 array. 
    After we have calculated the wave function, we can reshape it back from vector representation to 3
        --[Mikael Kuisma](https://www.youtube.com/channel/UCmRLy_j4kXTktxLPY9QtHbw)

List of Matlab functions used in the code.

- y = linspace(x1,x2,N) returns N linearly spaced points.
- [X,Y,Z] = meshgrid(xgv,ygv,zgv) produces three-dimensional coordinate arrays. The output coordinate arrays X, Y, and Z contain copies of the grid vectors xgv, ygv, and zgv respectively. The sizes of the output arrays are determined by the length of the grid vectors. For grid vectors xgv, ygv, and zgv of length M, N, and P respectively, X, Y, and Z will have N rows, M columns, and P pages.
- A = spdiags(B,d,m,n) creates an m-by-n sparse matrix by taking the columns of B and placing them along the diagonals specified by d.
- S = speye(m,n) and S = speye([m n]) form an m-by-n sparse matrix with 1s on the main diagonal.
- K = kron(A,B) returns the Kronecker tensor product of matrices A and B. If A is an m-by-n matrix and B is a p-by-q matrix, then kron(A,B) is an m*p-by-n*q matrix formed by taking all possible products between the elements of A and the matrix B.
- eigs(A,k,sigma) and eigs(A,B,k,sigma) return k eigenvalues based on sigma, which can take any of the following values... where 'sa' means smallest
- disp(X) displays the contents of X without printing the variable name. disp does not display empty variables.


<script type="text/javascript"
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>