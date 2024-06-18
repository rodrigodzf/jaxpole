# jaxpole


<!-- WARNING: THIS FILE WAS AUTOGENERATED! DO NOT EDIT! -->

This is an implementation of a differentiable time-varying all-pole
filter in JAX based on
[torchlpc](https://github.com/yoyololicon/torchlpc).

## Install

``` sh
pip install jaxpole
```

or locally from source

``` sh
pip install -e '.[dev]'
```

## How to use

``` python
import jax.numpy as jnp
import jax

pole = 0.99 * jnp.exp(1j * jnp.pi / 4)
coeffs = jnp.array([-2 * pole.real, pole.real**2 + pole.imag**2])

x = jax.random.normal(jax.random.PRNGKey(0), (1, 1000)) # (B, T)
A = jnp.tile(coeffs, (1, x.shape[-1], 1)) # (B, T, P)
zi = jnp.zeros((1, 2)) # (B, P)

# filter the signal
y = allpole(x, A, zi)
```
