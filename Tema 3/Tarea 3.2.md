# Caso de Uso Real de un Autómata Finito: Sistema de Validación de Contraseñas

## Descripción
Un autómata finito puede ser utilizado para validar si una contraseña cumple con ciertos criterios específicos, tales como:
- Longitud mínima de 8 caracteres.
- Contener al menos una letra mayúscula.
- Contener al menos una letra minúscula.
- Contener al menos un dígito.
- Contener al menos un carácter especial (por ejemplo, !, @, #, $, etc.).

## Implementación

### 1. Definición del Autómata
Se define un autómata finito determinista (DFA) con los siguientes estados y transiciones:

- **Estados:**
  - `q0`: Estado inicial.
  - `q1`: Se ha encontrado al menos una letra minúscula.
  - `q2`: Se ha encontrado al menos una letra mayúscula.
  - `q3`: Se ha encontrado al menos un dígito.
  - `q4`: Se ha encontrado al menos un carácter especial.
  - `q5`: Se ha alcanzado la longitud mínima de 8 caracteres.
  - `qf`: Estado final que indica una contraseña válida.

- **Transiciones:**
  - Desde `q0` a `q1` si se encuentra una letra minúscula.
  - Desde `q0` a `q2` si se encuentra una letra mayúscula.
  - Desde `q0` a `q3` si se encuentra un dígito.
  - Desde `q0` a `q4` si se encuentra un carácter especial.
  - Desde `q0` a `q5` si se alcanza la longitud de 8 caracteres.

- **Transiciones combinadas**: Para cada estado, si se encuentra un tipo de carácter que cumple una de las condiciones y la longitud es al menos 8 caracteres, se transita a `qf`.

### 2. Pseudocódigo del Autómata

```python
def es_contrasena_valida(contrasena):
    estado = 'q0'
    longitud = 0
    tiene_minuscula = False
    tiene_mayuscula = False
    tiene_digito = False
    tiene_especial = False

    caracteres_especiales = set("!@#$%^&*()-_+=<>?")

    for caracter in contrasena:
        longitud += 1
        
        if caracter.islower():
            tiene_minuscula = True
        elif caracter.isupper():
            tiene_mayuscula = True
        elif caracter.isdigit():
            tiene_digito = True
        elif caracter in caracteres_especiales:
            tiene_especial = True
        
        if longitud >= 8:
            if tiene_minuscula and tiene_mayuscula and tiene_digito and tiene_especial:
                estado = 'qf'
                break

    return estado == 'qf'
