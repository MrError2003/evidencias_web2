<!-- No borrar o modificar -->
[Inicio](./index.md)

## Sesión 7 


<!-- Su documentación aquí -->

## Hooks en REACT

 **Componente 1 - Ocultar y mostrar contenido**

- Este componente muestra dos contadores (count1 y count2) que pueden incrementarse o decrementarse mediante botones, y un botón que permite mostrar u ocultar estos contadores en función del estado de mostrarContenido. Es un ejemplo de cómo usar el Hook useState en React para administrar el estado local en componentes funcionales.

```jsx
import React, { useState } from "react";

export default function Componente1() {

    const [count1, setCount1] = useState(1)
    const [count2, setCount2] = useState(100)
    const [mostrarContenido, setMostrarContenido] = useState(false)

    function cambiarC1() {
        setCount1(count1 + 2)
    }

    function cambiarC2() {
        setCount2(count2 - 1)
    }

    function cambiarC3() {
        setCount1(count1 + 1)
        setCount2(count2 - 1)
    }

    function toogleMostrarContenido() {
        setMostrarContenido(!mostrarContenido)
    }

    return (

        <>

            {mostrarContenido && (

                <div>

                    <h1>Contador 1</h1>
                    <h1>{count1}</h1>

                    <h1>Contador 2</h1>
                    <h1>{count2}</h1>

                    <button onClick={cambiarC1}>Cambiar 1</button>
                    <button onClick={cambiarC2}>Cambiar 2</button>
                    <button onClick={cambiarC3}>Cambiar 3</button>

                </div>

            )}

            <button onClick={toogleMostrarContenido}>{mostrarContenido ? 'OCULTAR' : 'MOSTRAR'}</button>

        </>
    );
}
```

**Componente 2 - Lista de tareas**

- Este componente React permite al usuario agregar y marcar tareas como completadas. Las tareas se almacenan en el estado local tareas y se actualizan dinámicamente en la interfaz de usuario en función de las acciones del usuario.


```jsx
import React, { useState } from 'react'

function Componente2() {
    const [tareas, setTareas] = useState([]);
    const [nuevaTarea, setNuevaTarea] = useState('');

    function agregarTarea() {
        setTareas([...tareas, { texto: nuevaTarea, completada: false }]);
        setNuevaTarea('');
    }

    function marcarCompletada(index) {
        const nuevasTareas = [...tareas];
        nuevasTareas[index].completada = true;
        setTareas(nuevasTareas);
    }

    return (
        <div>
            <ul>
                {tareas.map((tarea, index) => (
                    <li key={index} className={tarea.completada ? 'completada' : ''} onClick={() => marcarCompletada(index)}>
                        {tarea.texto}
                    </li>
                ))}
            </ul>
            <input type="text" value={nuevaTarea} onChange={(e) => setNuevaTarea(e.target.value)} />
            <button onClick={agregarTarea}>Agregar Tarea</button>
        </div>
    );
}

export default Componente2;
```



**Componente 3 - Aumentar y disminuir**


- Este componente muestra cómo usar useEffect para realizar efectos secundarios cuando ciertas variables de estado (dato2 y dato3) cambian. Los valores de dato1, dato2 y dato3 se actualizan y se muestran en la interfaz de usuario en función de las acciones del usuario.

```jsx

import React, {useEffect, useState} from 'react'

export default function Componente3() {

    const[dato1, setDato] = useState(0)
    const[dato2, setDato2] = useState(0)
    const[dato3, setDato3] = useState(0)
    
    useEffect(() => {
        setDato(dato1 + 1)
    }, [dato2]);

    useEffect(() => {
        setDato(dato1 + 2)
    }, [dato3]);

  return (
    <div>
        <h1>{dato1}</h1>
        <h1>{dato2}</h1>
        <h1>{dato3}</h1>

        <button onClick={() => {setDato2(dato2 + 1)}}>Incrementar</button>
        <button onClick={() => {setDato3(dato3 + 1)}}>Incrementar</button>
    </div>
  )
}
```

**Componente 4 - Tabla de usuarios**

- Este componente React crea una tabla de usuarios que se puede filtrar por nombre y ordenar por edad. Los usuarios se filtran y ordenan dinámicamente según las acciones del usuario en la interfaz.

```jsx

import React, { useState } from 'react';

function TablaUsuarios() {
  const [usuarios, setUsuarios] = useState([
    { nombre: 'Juan', edad: 30 },
    { nombre: 'María', edad: 25 },
    { nombre: 'Pedro', edad: 35 },
    { nombre: 'Ana', edad: 28 },
    { nombre: 'Pancho', edad: 56 },
    { nombre: 'Regina', edad: 18 },
    { nombre: 'Pepe', edad: 42 },
  ]);
  const [filtro, setFiltro] = useState('');
  const [orden, setOrden] = useState('asc');

  function filtrarUsuarios(usuario) {
    return usuario.nombre.toLowerCase().includes(filtro.toLowerCase());
  }

  function ordenarUsuarios(a, b) {
    if (orden === 'asc') {
      return a.edad - b.edad;
    } else {
      return b.edad - a.edad;
    }
  }

  return (
    <div>
      <input type="text" value={filtro} onChange={(e) => setFiltro(e.target.value)} />
      <button onClick={() => setOrden(orden === 'asc' ? 'desc' : 'asc')}>{orden === 'asc' ? 'Ascendente' : 'Descendente'}</button>
      <table>
        <thead>
          <tr>
            <th>Nombre</th>
            <th>Edad</th>
          </tr>
        </thead>
        <tbody>
          {usuarios.filter(filtrarUsuarios).sort(ordenarUsuarios).map((usuario, index) => (
            <tr key={index}>
              <td>{usuario.nombre}</td>
              <td>{usuario.edad}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
}

export default TablaUsuarios;

```

**Componente 5 - Formulario Email**


- Este componente React proporciona un formulario de contacto básico que permite al usuario ingresar su nombre, correo electrónico y un mensaje. Cuando se envía el formulario, los valores ingresados se muestran en la consola, pero normalmente se utilizarían para realizar otras acciones, como enviar los datos a un servidor o realizar una lógica específica en una aplicación web.

```jsx
import React, { useState } from 'react';

function FormularioContacto() {
  const [nombre, setNombre] = useState('');
  const [email, setEmail] = useState('');
  const [mensaje, setMensaje] = useState('');

  function enviarFormulario(e) {
    e.preventDefault();
    console.log('Nombre:', nombre);
    console.log('Email:', email);
    console.log('Mensaje:', mensaje);
  }

  return (
    <form onSubmit={enviarFormulario}>
      <label>
        Nombre:
        <input type="text" value={nombre} onChange={(e) => setNombre(e.target.value)} />
      </label>
      <label>
        Correo electrónico:
        <input type="email" value={email} onChange={(e) => setEmail(e.target.value)} />
      </label>
      <label>
        Mensaje:
        <textarea value={mensaje} onChange={(e) => setMensaje(e.target.value)} />
      </label>
      <button type="submit">Enviar</button>
    </form>
  );
}

export default FormularioContacto;

```




