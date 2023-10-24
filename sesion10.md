<!-- No borrar o modificar -->
[Inicio](./index.md)

## Sesión 10 


**API - REST COUNTRIES**

**Country.jsx**

- este componente Country muestra información detallada sobre un país, incluyendo su nombre, bandera, capital, población y región. Se comunica con una API externa para obtener los datos del país en función del nombre proporcionado a través de la prop ```countryName```.

```jsx

import React, { useState, useEffect } from 'react';

export default function Country({ countryName }) {
  const [countryData, setCountryData] = useState(null);

  useEffect(() => {
    fetch(`https://restcountries.com/v3.1/name/${countryName}`)
      .then(response => response.json())
      .then(data => setCountryData(data[0]))
      .catch(error => console.error(error));
  }, [countryName]);

  if (!countryData) {
    return <div>Loading...</div>;
  }

  const flagStyle = {
    width: `100px`
  };

  return (
    <div>
      <h1>{countryData.name.common}</h1>
      <img
        src={countryData.flags.svg}
        alt={`Flag of ${countryData.name.common}`}
        style={flagStyle}
      />
      <p>Capital: {countryData.capital}</p>
      <p>Population: {countryData.population}</p>
      <p>Region: {countryData.region}</p>      
    </div>
  );
}

```

**Selector.jsx**

- el componente Selector muestra un selector de países que permite al usuario elegir un país y muestra información detallada sobre el país seleccionado utilizando el componente Country. La información de los países se obtiene de una API externa.

```jsx

import React, { useState, useEffect } from 'react';
import Country from './Country';


async function fetchCountries() {
    const response = await fetch('https://restcountries.com/v3.1/all');
    const data = await response.json();
    const countries = data.map(country => country.name.common);
    countries.sort();
    return countries;
}

export default function Selector() {
    const [countries, setCountries] = useState([]);
    const [selectedCountry, setSelectedCountry] = useState('');

    useEffect(() => {
        async function fetchCountriesData() {
            const data = await fetchCountries();
            setCountries(data);
        }
        fetchCountriesData();
    }, []);

    const handleChange = event => {
        setSelectedCountry(event.target.value);
    };

    return (
        <>
            <select value={selectedCountry} onChange={handleChange}>
                {countries.map(country => (
                    <option key={country} value={country}>
                        {country}
                    </option>
                ))}
            </select>
            <Country countryName={selectedCountry} />
        </>
    )
}

```








