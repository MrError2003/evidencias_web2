<!-- No borrar o modificar -->
[Inicio](./index.md)

## Sesión 11 

## API con AXIOS

**API The Cocktail DB componente - cocktail.jsx**

- Este componente permite a los usuarios seleccionar una categoría de cócteles y luego obtener y mostrar los cócteles en la categoría elegida de la API de ```TheCocktailDB```.

```jsx

import React, { useState, useEffect } from "react";
import axios from "axios";

export default function TheCocktailDB() {
    const [categories, setCategories] = useState([]);
    const [selectedCategory, setSelectedCategory] = useState("");
    const [cocktails, setCocktails] = useState([]);

    useEffect(() => {
        axios
            .get("https://www.thecocktaildb.com/api/json/v1/1/list.php?c=list")
            .then((response) => {
                setCategories(response.data.drinks);
            });
    }, []);

    useEffect(() => {
        if (selectedCategory !== "") {
            axios
                .get(`https://www.thecocktaildb.com/api/json/v1/1/filter.php?c=${selectedCategory}`)
                .then((response) => {
                    setCocktails(response.data.drinks);
                });
        }
    }, [selectedCategory]);

    const handleCategoryChange = (event) => {
        setSelectedCategory(event.target.value);
    };

    const flagStyle = {
        width: `100px`
    };

    return (
        <div>
    <label htmlFor="category-select" class="cocktail">Selecciona una categoría:</label>
    <select
        name="category-select"
        id="category-select"
        value={selectedCategory}
        onChange={handleCategoryChange}
        class="cocktail"
    >
        <option value="">Selecciona una categoría</option>
        {categories.map((category) => (
            <option key={category.strCategory} value={category.strCategory}>
                {category.strCategory}
            </option>
        ))}
    </select>
    <h2 class="cocktail">Cócteles disponibles en la categoría {selectedCategory}:</h2>
    <ul class="cocktail-container"> 
        {cocktails.map((cocktail) => (
            <li key={cocktail.idDrink} class="cocktail">
                {cocktail.strDrink}
                <img
                    src={cocktail.strDrinkThumb}
                    class="cocktail-image" 
                />
            </li>
        ))}
    </ul>
</div>

    );
}

```

**API fakestore**

- Este componente de React muestra una lista de productos de FakeStore y permite al usuario filtrarlos por categoría. Las categorías y productos se obtienen de la API de FakeStore utilizando solicitudes HTTP, y la interfaz de usuario se organiza utilizando componentes de Bootstrap para lograr una presentación ordenada.

```jsx


import React, { useState, useEffect } from "react";
import axios from "axios";
import { Container, Row, Col, Nav, Card } from "react-bootstrap";


export default function FakeStore() {
    const [products, setProducts] = useState([]);
    const [categories, setCategories] = useState([]);
    const [selectedCategory, setSelectedCategory] = useState("");

    useEffect(() => {
        axios
            .get("https://fakestoreapi.com/products")
            .then((response) => setProducts(response.data));

        axios
            .get("https://fakestoreapi.com/products/categories")
            .then((response) => setCategories(response.data));
    }, []);

    const handleCategoryChange = (eventKey) => {
        setSelectedCategory(eventKey);
    };

    const filteredProducts =
        selectedCategory === ""
            ? products
            : products.filter((product) => product.category === selectedCategory);

    return (
        <Container fluid>
            <Row>
                <Col>
                    <h1>Lista de productos</h1>
                </Col>
            </Row>
            <Row>
                <Col md={2}>
                    <Nav
                        variant="pills"
                        className="flex-column"
                        activeKey={selectedCategory}
                        onSelect={handleCategoryChange}
                    >
                        <Nav.Item>
                            <Nav.Link eventKey="">Todas las categorías</Nav.Link>
                        </Nav.Item>
                        {categories.map((category) => (
                            <Nav.Item key={category}>
                                <Nav.Link eventKey={category}>{category}</Nav.Link>
                            </Nav.Item>
                        ))}
                    </Nav>
                </Col>
                <Col md={10}>
                    <Row>
                        {filteredProducts.map((product) => (
                            <Col key={product.id} md={4} className="mb-4">
                                <Card>
                                    <Card.Img
                                        variant="top"
                                        src={product.image}
                                        alt={product.title}
                                    />
                                    <Card.Body>
                                        <Card.Title>{product.title}</Card.Title>
                                        <Card.Text>Precio: {product.price}</Card.Text>
                                        <Card.Text>Categoría: {product.category}</Card.Text>
                                    </Card.Body>
                                </Card>
                            </Col>
                        ))}
                    </Row>
                </Col>
            </Row>
        </Container>
    );
}

```




