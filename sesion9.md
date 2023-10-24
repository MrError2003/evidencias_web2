<!-- No borrar o modificar -->
[Inicio](./index.md)

## Sesión 9 


<!-- Su documentación aquí -->

**useContext - Cambio de tema de aplicacion**


- Este componente muestra cómo se puede usar el contexto en React para administrar y compartir el tema de una aplicación entre varios componentes sin necesidad de pasar propiedades manualmente a través de la jerarquía de componentes. El estado ```theme``` y la función ```toggleTheme``` se gestionan en el componente App, y otros componentes pueden acceder a estos valores utilizando el hook ```useContext``` en React.

```jsx

import React, { useState } from 'react';
import ThemeContext from './ThemeContext';
import ThemeSwitcher from './ThemeSwitcher';
import ThemeDisplay from './ThemeDisplay';
import ThemedButton from './ThemedButton';
import './App.css';

function App() {
  const [theme, setTheme] = useState('light');

  function toggleTheme() {
    setTheme(theme === 'light' ? 'dark' : 'light');
  }

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      <div className={`app app-${theme}`}>
        <h1>Contexto y useContext en React</h1>
        <ThemeSwitcher />
        <ThemeDisplay />
        <ThemedButton>
          Botón con tema
        </ThemedButton>
      </div>
    </ThemeContext.Provider>
  );
}

export default App;

```

**```ThemeContext.js```**

- Permite proporcionar el tema actual y la función para cambiarlo a otros componentes dentro de la aplicación, lo que facilita la administración del tema en toda la aplicación sin necesidad de pasar propiedades manualmente a través de la jerarquía de componentes.

```jsx

import React from 'react';

const ThemeContext = React.createContext({
  theme: 'light',
  toggleTheme: () => {}
});

export default ThemeContext;

```

**ThemeDisplay**

-  ThemeDisplay es un componente que se encarga de mostrar el tema actual de la aplicación, utilizando el contexto proporcionado por ThemeContext. El valor del tema se obtiene a través de useContext, y se utiliza para cambiar la apariencia del componente al tema actual. Este enfoque permite que el componente refleje automáticamente los cambios en el tema sin necesidad de pasar manualmente el tema como una propiedad.

```jsx

import React, { useContext } from 'react';
import ThemeContext from './ThemeContext';
import './ThemeDisplay.css';

function ThemeDisplay() {
  const { theme } = useContext(ThemeContext);

  return (
    <div className={`theme-display theme-display-${theme}`}>
      <p>El tema actual es: {theme}</p>
    </div>
  );
}

export default ThemeDisplay;

```



