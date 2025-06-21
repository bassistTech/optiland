# Derivation of vector grating equation

[bassistTech](https://github.com/bassisttech), 2025. 

I found a vector form of the grating equation in the OSLO reference manual:

https://lambdaresfiles.com/wp-content/uploads/support/oslo/oslo_releases/OSLOUserGuide.pdf

However, I will re-derive it from scratch here. The familiar textbook grating equation is:

$n' \sin \alpha' + n \sin \alpha = m\lambda/d$,

We will need to have this equation in vector form. Multiplying both sides of this equation by $\hat q$:

$(n' \sin \alpha') \hat q  + (n \sin \alpha) \hat q  = (m\lambda/d) \hat q$

While $\hat q$ can be an arbitrary vector, I'm going to anticipate the result that I need, and let it be the unit vector perpendicular to the grooves of the grating, and $\hat p$ the surface normal. This can be re-written as:

$n' \hat e' \times \hat p - n \hat e \times \hat p = (m \lambda /d) \hat q$

noting that the second term is negative due to the relative directions of the incident and diffracted rays. Finally, this solves to:

$n' \hat e' \times \hat p = n \hat e \times \hat p + \hat q(m \lambda /d)$

This is exactly the equation given in the OSLO manual. But while it's easy to write, it's hard to use, because there is no general "inverse" of a cross product. A vector form of Snell's Law, using cross products, has the same problem.

However, for a plane grating, normal to the local x-y axis, and with grooves parallel to the x axis (perpendicular to the y-axis), it can be simplified by letting 

$\hat p = \hat k$ and $\hat q = \hat j$,

This simplification is acceptable because other orientations can be implemented with coordinate rotations. Using the traditional formula for the cross product:

$\vec{a} \times \vec{b} = (a_yb_z-a_zb_y)\hat i + (a_zb_x-a_xb_z) \hat j+(a_xb_y-a_yb_x) \hat k$

The general grating equation reduces to:

$n'(e'_y \hat x + e'_x \hat y) = n (e_y \hat x + e_x \hat y) + \dfrac {m \lambda} d \hat x$

Collecting like terms,

$e'_y = \dfrac 1 {n'}(n e_y + \dfrac {m \lambda} {d})$

$e'_x = \dfrac n {n'} e_x$

These equations work for reflection gratings as well, by letting $n' = -n$. The simplification is acceptable because any other orientation of the grating can be handled with coordinate rotations. And a refractive index is needed in case the grating is a transmission grating, which is typically a diffractive surface in between glass plates.

The equations are kind of boring. The first one, for $e'_y$ is exactly the textbook grating equation. The second one, for $e'_x$ is Snell's Law, and tells us that nohing interesting happens in the $x$ direction. 

For now, my contribution to Optiland only includes a plane grating (surface type "plane_grating"). This was easier to implement, because there's exactly one surface normal, therefore exactly one value of $\hat q$. The same formula should work for a curved grating, but each ray will have unique values of $e'_x$ and $e'_y$. Also, the plane grating is easy to test. I drew a ray trace by hand on thin paper, with a ruler and protractor, 
and held it over the Optiland graph on my monitor!

To work with a curved grating, the value of $\hat q$ has to be computed for each ray. Also, for total generality, a vector representing the groove period and orientation could be a function of the position on the surface. I will think about a way to approximate the behavior of a concave grating, but with a caveat: Many commercial gratings can't be precisely modeled. The reason is that vendors don't disclose detailed prescription information for aberration corrected holographic gratings.