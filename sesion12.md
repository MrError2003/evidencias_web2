<!-- No borrar o modificar -->
[Inicio](./index.md)

## Sesión 12 


<!-- Su documentación aquí -->


## PRUEBAS UNITARIAS - EJEMPLO

**Componente - Toggle.jsx**

- este componente React muestra un mensaje que indica si está "Activo" o "Inactivo" según el valor del estado "activo", y proporciona un botón que permite cambiar ese estado de "Activo" a "Inactivo" o viceversa al hacer clic en él. Esto es un ejemplo de cómo React permite gestionar el estado de los componentes y actualizar la interfaz de usuario en función de esos cambios.

```jsx

import React from 'react'

export default function Toggle() {
    const [activo, setActivo] = React.useState(false);

    const handleToggle = () => {
      setActivo(!activo);
    };
  return (
    <div>
      <p>Estado: {activo ? 'Activo' : 'Inactivo'}</p>
      <button onClick={handleToggle}>Cambiar Estado</button>
    </div>
  )
}

```

**Pruebas unitarias - Toggle.test.jsx**

- este caso de prueba verifica que el componente Toggle funciona correctamente al cambiar de estado cuando se hace clic en el botón "Cambiar Estado". Si el estado inicial es "Inactivo", después de hacer clic en el botón, el estado debe cambiar a "Activo". Esto demuestra cómo las pruebas automatizadas pueden validar el comportamiento de un componente React.

```jsx

import { render, screen, fireEvent } from '@testing-library/react';
import Toggle from './Toggle';

test('El componente Toggle debe cambiar de estado al hacer clic en el botón', () => {
    render(<Toggle />);

    const elementoEstado = screen.getByText('Estado: Inactivo');

    const elementoBoton = screen.getByText('Cambiar Estado');

    expect(elementoEstado).toBeInTheDocument();

    fireEvent.click(elementoBoton);

    expect(elementoEstado).toHaveTextContent('Estado: Activo');
    
});

```


