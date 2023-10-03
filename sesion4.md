<!-- No borrar o modificar -->
[Inicio](./index.md)

## Sesión 4


<!-- Su documentación aquí -->


**List.jsx**

    import React from 'react'
    
    export default function List({ items }) {
        
        return (
            <>
                <ul>
                    {
                        items.map((item) => (
                            <li style={{ color: item.color }}>
                                <h3>{item.name}</h3>
                            </li>
                        ))
                    }
                </ul>
            </>
    
    
        )
    ;
    }


**App.jsx**


        import { useState } from 'react'
        import reactLogo from './assets/react.svg'
        import viteLogo from '/vite.svg'
        //import './App.css'
        import List from './components/list'
        
        
        function App() {
          const items = [
            { name: 'Fresa', color: 'red' },
            { name: 'Berry', color: 'blue' },
            { name: 'Platano', color: 'green' },
            { name: 'Naranaja', color: 'orange' },
        
          ]
        
          return (
            <>
                <List items={items} />
            </>
          )
        }
    
    export default App


- El componente `List` recibe una prop llamada `items`, que es un array de objetos que contiene información sobre elementos de una lista. Este componente tiene la responsabilidad de mostrar estos elementos en forma de una lista desordenada (`<ul>`) en la interfaz de usuario. Aquí está cómo funciona:

-   El componente `List` toma un array `items` como prop, que contiene objetos con propiedades `name` (nombre) y `color` (color).
    
-   Dentro del componente, se utiliza el método `map` para recorrer el array `items`. Para cada elemento del array, se genera un elemento de lista (`<li>`) que muestra el nombre del elemento (`item.name`) y aplica el color del elemento (`item.color`) como estilo en línea al texto.
    
-   El resultado es una lista desordenada (`<ul>`) donde cada elemento de lista muestra el nombre y se colorea según el color especificado en los objetos del array `items`.
    

- En resumen, el componente `List` es una parte de la interfaz de usuario que se utiliza para mostrar una lista de elementos, y cada elemento se representa como un elemento de lista (`<li>`) con un nombre y un color asociado. El contenido de la lista se genera dinámicamente a partir del array `items` que se pasa como prop.



