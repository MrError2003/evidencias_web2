<!-- No borrar o modificar -->
[Inicio](./index.md)

## Sesión 6


<!-- Su documentación aquí -->


**App.jsx**

- En este archivo se define el componente principal de la aplicación llamado App.

- Se importa el componente List desde el archivo List.jsx.

- Se define un objeto datosReceta que contiene información sobre una receta de pastel de chocolate, incluyendo el nombre, el tiempo de preparación, los ingredientes y los pasos.

- El componente App se define como una función que devuelve elementos JSX. Utiliza la información de datosReceta para mostrar el nombre de la receta, el tiempo de preparación, los ingredientes y los pasos en una estructura de HTML.

```jsx
import List from './components/List'

const datosReceta = {
  "nombre": "Pastel de chocolate",
  "tiempoPreparacion": 60,
  "ingredientes": [
    {
      "nombre": "chocolate negro",
      "cantidad": "200g"
    },
    {
      "nombre": "mantequilla",
      "cantidad": "200g"
    },
    {
      "nombre": "azúcar",
      "cantidad": "200g"
    },
    {
      "nombre": "huevos",
      "cantidad": "4"
    },
    {
      "nombre": "harina",
      "cantidad": "150g"
    }
  ],
  "pasos": [
    "Precalentar el horno a 180 grados.",
    "Derretir el chocolate y la mantequilla juntos en un recipiente.",
    "Agregar el azúcar y mezclar bien.",
    "Agregar los huevos uno por uno y mezclar bien después de cada adición.",
    "Agregar la harina y mezclar hasta que esté bien combinado.",
    "Engrasar un molde para pastel y verter la mezcla.",
    "Hornear durante 40 minutos.",
    "Dejar enfriar antes de servir."
  ]
};


function App() {
  return (
    <div>
      <h1>{datosReceta.nombre}</h1>
      <p>Tiempo de preparación: {datosReceta.tiempoPreparacion} minutos</p>

      <List title="Ingredientes" items={datosReceta.ingredientes.map(ingrediente => `${ingrediente.cantidad} de ${ingrediente.nombre}`)} />
      <List title="Pasos" items={datosReceta.pasos} />
    </div>
  );
}

export default App
```

**list.jsx**


- Este archivo define un componente llamado List.

- El componente List recibe dos propiedades (title y items) y muestra una lista desordenada HTML (ul) con los elementos de la matriz items. El título se muestra como un encabezado (h2) antes de la lista.

- Utiliza el método map para iterar a través de los elementos de items y mostrar cada elemento en un elemento de lista (li) dentro de la lista desordenada.

```jsx
import React from 'react';

const List = ({ title, items }) => {
  return (
    <div>
      <h2>{title}</h2>
      <ul>
        {items.map((item, index) => (
          <li key={index}>{item}</li>
        ))}
      </ul>
    </div>
  );
};

export default List;
```






