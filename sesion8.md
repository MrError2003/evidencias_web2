<!-- No borrar o modificar -->
[Inicio](./index.md)

## Sesión 8 


<!-- Su documentación aquí -->

**useEffect 1 - Ultima tecla presionada**


- Este componente registra y muestra la última tecla presionada por el usuario en la interfaz utilizando el evento de teclado y el Hook useEffect.


```jsx
import React, { useState, useEffect } from 'react';

export default function Componente4() {
  const [keyPressed, setKeyPressed] = useState(null);

  useEffect(() => {
    function handleKeyPress(event) {
      setKeyPressed(event.key);
    }

    window.addEventListener('keydown', handleKeyPress);

    return () => {
      window.removeEventListener('keydown', handleKeyPress);
    };
  }, []);

  return (
    <div>
      <p>Última tecla presionada: {keyPressed}</p>
    </div>
  );
}
```



**useEffect 2 - Ubicacion por coordenadas**


- Este componente React obtiene la ubicación geográfica actual del usuario utilizando el servicio de geolocalización del navegador y muestra las coordenadas de latitud y longitud en la interfaz de usuario una vez que se obtiene la ubicación.

```jsx
import React, { useState, useEffect } from 'react';


export default function Componente5() {
  const [ubicacion, setUbicacion] = useState(null);

  useEffect(() => {
    function obtenerUbicacion() {
      navigator.geolocation.getCurrentPosition((posicion) => {
        const latitud = posicion.coords.latitude;
        const longitud = posicion.coords.longitude;
        setUbicacion({ latitud, longitud });
      });
    }
    obtenerUbicacion();
  }, []);

  return (
    <div>
      {ubicacion ? (
        <h1>Ubicación actual: ({ubicacion.latitud}, {ubicacion.longitud})</h1>
      ) : (
        <h1>Obteniendo ubicación...</h1>
      )}
    </div>
  );
}
```
**useEfect 3 - Cambio de ventana**

- Este componente React muestra dinámicamente el ancho de la ventana del navegador y se actualiza automáticamente cuando el usuario cambia el tamaño de la ventana. Es un ejemplo de cómo usar el Hook useEffect para realizar efectos secundarios basados en eventos del navegador.

```jsx
import React, { useState, useEffect } from 'react';

function TamañoVentana() {
    const [ancho, setAncho] = useState(window.innerWidth);

    useEffect(() => {
        function manejarCambioDeTamaño() {
            setAncho(window.innerWidth);
        }
        window.addEventListener('resize', manejarCambioDeTamaño);

        return () => {
            window.removeEventListener('resize', manejarCambioDeTamaño);
        };
    }, []);

    return (
        <div>
            <h1>Ancho de la ventana: {ancho}px</h1>
        </div>
    );
}

export default TamañoVentana;
```

**useEffect 4 - Formulario valido**

- Este componente React proporciona un formulario de registro que realiza validación en tiempo real y muestra mensajes de error según los criterios de validación definidos para los campos Nombre, Email y Contraseña. 

```jsx

import React, { useState, useEffect } from 'react';

function Formulario() {
  const [formulario, setFormulario] = useState({
    nombre: '',
    email: '',
    password: '',
  });
  const [errores, setErrores] = useState({});

  const validarFormulario = () => {
    const nuevosErrores = {};

    if (!formulario.nombre) {
      nuevosErrores.nombre = 'El nombre es requerido';
    }
    if (!formulario.email) {
      nuevosErrores.email = 'El email es requerido';
    } else if (!/S+@S+.S+/.test(formulario.email)) {
      nuevosErrores.email = 'El email es inválido';
    }
    if (!formulario.password) {
      nuevosErrores.password = 'La contraseña es requerida';
    } else if (formulario.password.length < 8) {
      nuevosErrores.password = 'La contraseña debe tener al menos 8 caracteres';
    }

    setErrores(nuevosErrores);
  };

  useEffect(() => {
    validarFormulario();
  }, [formulario]);

  const handleSubmit = (event) => {
    event.preventDefault();
    if (Object.keys(errores).length === 0) {
      alert('Formulario válido. Datos enviados al servidor');
    } else {
      alert('Formulario inválido. Verifique los campos marcados');
    }
  };

  const handleChange = (event) => {
    setFormulario({
      ...formulario,
      [event.target.name]: event.target.value,
    });
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label htmlFor="nombre">Nombre:</label>
        <input
          type="text"
          id="nombre"
          name="nombre"
          value={formulario.nombre}
          onChange={handleChange}
        />
        {errores.nombre && <span className="error">{errores.nombre}</span>}
      </div>
      <div>
        <label htmlFor="email">Email:</label>
        <input
          type="email"
          id="email"
          name="email"
          value={formulario.email}
          onChange={handleChange}
        />
        {errores.email && <span className="error">{errores.email}</span>}
      </div>
      <div>
        <label htmlFor="password">Contraseña:</label>
        <input
          type="password"
          id="password"
          name="password"
          value={formulario.password}
          onChange={handleChange}
        />
        {errores.password && <span className="error">{errores.password}</span>}
      </div>
      <button type="submit">Enviar</button>
    </form>
  );
}

export default Formulario;

``` 

**useEffect 5 - Contador de caracteres**

- Este componente React proporciona una lista de elementos paginada, donde se muestra un número específico de elementos por página. Los usuarios pueden navegar entre las páginas utilizando los botones de paginación. Esto es útil cuando se tiene una gran cantidad de elementos para mostrar y se quiere dividir en páginas más pequeñas para una mejor experiencia del usuario.

```jsx

import React, { useState, useEffect } from 'react';

function ListaElementos() {
  const [elementos, setElementos] = useState([
    'Manzana',
    'Banana',
    'Cereza',
    'Durazno',
    'Fresa',
    'Uva',
    'Kiwi',
    'Limón',
    'Naranja',
    'Pera',
    'Papaya',
    'Piña',
    'Sandía',
  ]);
  const [paginaActual, setPaginaActual] = useState(1);
  const [elementosPorPagina] = useState(4);
  const [elementosPagina, setElementosPagina] = useState([]);

  useEffect(() => {
    const indiceFinal = paginaActual * elementosPorPagina;
    const indiceInicial = indiceFinal - elementosPorPagina;
    const elementosPaginaActual = elementos.slice(indiceInicial, indiceFinal);
    setElementosPagina(elementosPaginaActual);
  }, [paginaActual, elementosPorPagina, elementos]);

  const handleClickPagina = (numeroPagina) => {
    setPaginaActual(numeroPagina);
  };

  const numeroPaginas = Math.ceil(elementos.length / elementosPorPagina);
  const paginas = [];
  for (let i = 1; i <= numeroPaginas; i++) {
    paginas.push(
      <button key={i} onClick={() => handleClickPagina(i)}>
        {i}
      </button>
    );
  }

  return (
    <>
      <ul>
        {elementosPagina.map((elemento, index) => (
          <li key={index}>{elemento}</li>
        ))}
      </ul>
      <div>
        {paginas}
      </div>
    </>
  );
}

export default ListaElementos;

```





