<!-- No borrar o modificar -->
[Inicio](./index.md)

## Sesión 3 


<!-- Su documentación aquí -->


**MovieCard.jsx:** 

- Este componente se encarga de mostrar una tarjeta (card) para una película individual. Toma tres propiedades (title, description, imageUrl) como entrada y muestra el título, la descripción y la imagen de la película utilizando componentes de tarjeta proporcionados por React Bootstrap.

    import React from 'react'
    import { Card } from "react-bootstrap";
    
    export default function MovieCard({ title, description, imageUrl }) {
        return (
            <Card>
                <Card.Img variant="top" src={imageUrl} />
                <Card.Body>
                    <Card.Title>{title}</Card.Title>
                    <Card.Text>{description}</Card.Text>
                </Card.Body>
            </Card>
        )
    }


**MovieList.jsx:** 

- Este componente es responsable de mostrar una lista de películas. Define un array llamado movies que contiene objetos de película con títulos, descripciones e URLs de imágenes. Luego, utiliza un bucle map para recorrer este array y generar un MovieCard para cada película. Los datos de la película se pasan como propiedades al componente MovieCard.

    import React from "react";
    import MovieCard from "./MovieCard";
    import { Container, Row, Col } from "react-bootstrap";
    
    const movies = [
      {
        title: "Pelicula 1",
        description: "Descripción de la película 1.",
        imageUrl: "https://m.media-amazon.com/images/I/61XXvCFNaRL._AC_SL1024_.jpg"
      },
      {
        title: "Pelicula 2",
        description: "Descripción de la película 2.",
        imageUrl: "https://www.joblo.com/wp-content/uploads/2019/03/avengers-endgame-poster-xl-1.jpg",
      },
      {
        title: "Pelicula 3",
        description: "Descripción de la película 2.",
        imageUrl: "https://www.aceprensa.com/wp-content/uploads/2018/03/333339-0.jpg",
      },
      
    ];
    
    const MovieList = () => {
      return (
        <Container>
          <Row>
            {movies.map((movie, index) => (
              <Col key={index} xs={12} md={4}>
                <MovieCard
                  title={movie.title}
                  description={movie.description}
                  imageUrl={movie.imageUrl}
                />
              </Col>
            ))}
          </Row>
        </Container>
      );
    };
    export default MovieList;


**App.jsx:** 

- Este es el componente principal de la aplicación. En él, se importa el componente MovieList y se utiliza en el elemento principal de la página. La aplicación renderiza un encabezado con el título "Películas" y luego muestra la lista de películas utilizando el componente MovieList.

    import './App.css'
    import MovieList from './components/MovieList'
    
    function App() {
    
      return (
        <>
        <div>
          <header>
            <h1>Películas</h1>
          </header>
          <main>
            <MovieList/>
          </main>
        </div>
          
        </>
      )
    }
    
    export default App



- En resumen, cuando ejecutas esta aplicación, obtendrás una página web que muestra una lista de tarjetas de películas, cada una con su título, descripción e imagen. Esta estructura facilita la adición de nuevas películas a la lista o la modificación de las existentes, ya que todo se gestiona de manera modular y componentizada.


