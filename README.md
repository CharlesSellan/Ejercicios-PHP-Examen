 # Ejercicios-PHP-Examen
Ejercicio 4

Crea una página web con la carta de un restaurante. La estructura de archivos debe ser:

/ejercicio4
├── index.php
├── data.php
├── partials/
│   ├── header.php
│   └── footer.php
└── img/
Los datos los defines tú. Crea un array llamado $platos en data.php con mínimo 8 platos. Cada plato debe tener: id, nombre, descripcion, precio, categoria (entrante, principal, postre), alergenos (array con los alérgenos), disponible (true o false) e imagen.

La página debe mostrar:

Todos los platos agrupados por categoría — primero los entrantes, luego los principales y por último los postres. Cada plato se muestra en formato tarjeta con imagen, nombre, descripción, precio y alérgenos. Los platos no disponibles se muestran con un estilo visual diferente y una etiqueta "No disponible"
Una sección de ofertas con los platos cuyo precio sea menor o igual a 10 euros, mostrando el precio con un 15% de descuento
Requisitos:

Crea una función pintarPlato($plato) en data.php y úsala en index.php
Usa <?= ?> para pintar valores y la sintaxis alternativa de PHP en el HTML
La página debe tener estilos propios y verse limpia y apetecible
DATA.PHP

1, "nombre" => "Ensalada César", "descripcion" => "Lechuga, pollo, queso y salsa César", "precio" => 8, "categoria" => "entrante", "alergenos" => ["leche", "gluten", "huevo"], "disponible" => true, "imagen" => "img/ensalada.jpg" ], [ "id" => 2, "nombre" => "Croquetas", "descripcion" => "Croquetas caseras de jamón", "precio" => 7, "categoria" => "entrante", "alergenos" => ["gluten", "leche", "huevo"], "disponible" => true, "imagen" => "img/croquetas.jpg" ], [ "id" => 3, "nombre" => "Patatas bravas", "descripcion" => "Patatas con salsa brava", "precio" => 5, "categoria" => "entrante", "alergenos" => [], "disponible" => false, "imagen" => "img/patatas.jpg" ], [ "id" => 4, "nombre" => "Hamburguesa", "descripcion" => "Carne de ternera, queso y tomate", "precio" => 12, "categoria" => "principal", "alergenos" => ["gluten", "leche", "huevo"], "disponible" => true, "imagen" => "img/hamburguesa.jpg" ], [ "id" => 5, "nombre" => "Pizza", "descripcion" => "Pizza de queso y tomate", "precio" => 10, "categoria" => "principal", "alergenos" => ["gluten", "leche"], "disponible" => true, "imagen" => "img/pizza.jpg" ], [ "id" => 6, "nombre" => "Pasta carbonara", "descripcion" => "Pasta con nata, queso y bacon", "precio" => 11, "categoria" => "principal", "alergenos" => ["gluten", "leche", "huevo"], "disponible" => false, "imagen" => "img/pasta.jpg" ], [ "id" => 7, "nombre" => "Tarta de queso", "descripcion" => "Tarta casera de queso", "precio" => 6, "categoria" => "postre", "alergenos" => ["leche", "gluten", "huevo"], "disponible" => true, "imagen" => "img/tarta.jpg" ], [ "id" => 8, "nombre" => "Helado", "descripcion" => "Helado de vainilla y chocolate", "precio" => 4, "categoria" => "postre", "alergenos" => ["leche"], "disponible" => true, "imagen" => "img/helado.jpg" ] ]; function pintarPlato($plato) { ?>
<div class="tarjeta <?php if (!$plato["disponible"]) echo "no-disponible"; ?>">
    <img src="<?= $plato["imagen"] ?>" alt="<?= $plato["nombre"] ?>">

    <div class="contenido">
        <h3><?= $plato["nombre"] ?></h3>
        <p><?= $plato["descripcion"] ?></p>
        <p class="precio"><?= $plato["precio"] ?> €</p>

        <p>
            <strong>Alérgenos:</strong>
            <?php if (count($plato["alergenos"]) > 0): ?>
                <?= implode(", ", $plato["alergenos"]) ?>
            <?php else: ?>
                Ninguno indicado
            <?php endif; ?>
        </p>

        <?php if ($plato["disponible"]): ?>
            <span class="disponible">Disponible</span>
        <?php else: ?>
            <span class="etiqueta">No disponible</span>
        <?php endif; ?>
    </div>
</div>
partials/header.php

<title>Restaurante La Mesa</title>
Restaurante La Mesa
Sabores caseros para disfrutar

Inicio Entrantes Principales Postres Ofertas
partials/footer.php

Restaurante La Mesa - Todos los derechos reservados

index.php

Entrantes
<div class="platos">
    <?php foreach ($platos as $plato): ?>
        <?php if ($plato["categoria"] == "entrante"): ?>
            <?php pintarPlato($plato); ?>
        <?php endif; ?>
    <?php endforeach; ?>
</div>

<h2 id="principales">Platos principales</h2>

<div class="platos">
    <?php foreach ($platos as $plato): ?>
        <?php if ($plato["categoria"] == "principal"): ?>
            <?php pintarPlato($plato); ?>
        <?php endif; ?>
    <?php endforeach; ?>
</div>

<h2 id="postres">Postres</h2>

<div class="platos">
    <?php foreach ($platos as $plato): ?>
        <?php if ($plato["categoria"] == "postre"): ?>
            <?php pintarPlato($plato); ?>
        <?php endif; ?>
    <?php endforeach; ?>
</div>

<h2 id="ofertas">Ofertas especiales</h2>

<div class="platos">
    <?php foreach ($platos as $plato): ?>
        <?php if ($plato["precio"] <= 10): ?>
            <div class="tarjeta">
                <img src="<?= $plato["imagen"] ?>" alt="<?= $plato["nombre"] ?>">

                <div class="contenido">
                    <h3><?= $plato["nombre"] ?></h3>
                    <p>Precio original: <?= $plato["precio"] ?> €</p>

                    <p class="precio-oferta">
                        Precio con descuento:
                        <?= number_format($plato["precio"] * 0.85, 2) ?> €
                    </p>
                </div>
            </div>
        <?php endif; ?>
    <?php endforeach; ?>
</div>
style.css

body {
font-family: Arial, sans-serif;
margin: 0;
background-color: #fff8f0;
color: #333;
}

header {
background-color: #7c2d12;
color: white;
text-align: center;
padding: 25px;
}

header h1 {
margin: 0;
font-size: 35px;
}

nav {
background-color: #431407;
padding: 15px;
text-align: center;
}

nav a {
color: white;
text-decoration: none;
margin: 0 15px;
}

nav a:hover {
color: #fdba74;
}

main {
width: 90%;
max-width: 1200px;
margin: 30px auto;
}

h2 {
color: #9a3412;
border-bottom: 2px solid #fed7aa;
padding-bottom: 10px;
margin-top: 40px;
}

.platos {
display: flex;
flex-wrap: wrap;
gap: 20px;
}

.tarjeta {
background-color: white;
width: 250px;
border-radius: 12px;
overflow: hidden;
box-shadow: 0 3px 10px #ddd;
}

.tarjeta img {
width: 100%;
height: 170px;
object-fit: cover;
}

.contenido {
padding: 15px;
}

.contenido h3 {
margin-top: 0;
color: #7c2d12;
}

.precio {
font-size: 22px;
font-weight: bold;
color: #15803d;
}

.precio-oferta {
font-size: 18px;
font-weight: bold;
color: #dc2626;
}

.no-disponible {
opacity: 0.55;
background-color: #eee;
}

.etiqueta {
display: inline-block;
background-color: #dc2626;
color: white;
padding: 6px 10px;
border-radius: 5px;
}

.disponible {
display: inline-block;
background-color: #dcfce7;
color: #166534;
padding: 6px 10px;
border-radius: 5px;
}

footer {
margin-top: 50px;
padding: 20px;
background-color: #431407;
color: white;
text-align: center;
}

@media (max-width: 600px) {
.platos {
justify-content: center;
}

nav a {
    display: inline-block;
    margin: 8px;
}
}

Ejercicio 5
Crea un sistema de reservas para un restaurante. La estructura de archivos es:

/ejercicio5
├── index.php
├── confirmacion.php
├── controllers/
│   └── reserva.php
└── partials/
    ├── header.php
    └── footer.php
index.php muestra un formulario de reserva con los siguientes campos:

Campo	Tipo	Validación
Nombre	text	Obligatorio
Email	email	Obligatorio
Fecha	date	Obligatorio
Numero de personas	number	Entre 1 y 10
Preferencia	select (interior / terraza)	Obligatorio
Si existe $_GET["error"] muestra un mensaje de error específico según su valor:

error=campos — "Hay campos obligatorios sin rellenar"
error=personas — "El número de personas debe ser entre 1 y 10"
error=preferencia — "La preferencia seleccionada no es válida"
controllers/reserva.php solo acepta POST. Valida los datos en este orden:

Comprueba que ningún campo esté vacío — si falla redirige a index.php?error=campos
Comprueba que el número de personas esté entre 1 y 10 — si falla redirige a index.php?error=personas
Comprueba que la preferencia sea interior o terraza — si falla redirige a index.php?error=preferencia
Si todo es correcto guarda los datos en $_SESSION y redirige a confirmacion.php.

confirmacion.php muestra un resumen de la reserva con todos los datos recibidos. Si no hay sesión activa redirige a index.php.

PARTIALS/HEADER

<title>Reservas restaurante</title>
Restaurante La Mesa
Reserva tu mesa

PARTIALS/FOOTER

Restaurante La Mesa

INDEX.PHP

Formulario de reserva
<?php if (isset($_GET["error"])): ?>
    <p class="error">
        <?php
        if ($_GET["error"] == "campos") {
            echo "Hay campos obligatorios sin rellenar";
        } elseif ($_GET["error"] == "personas") {
            echo "El número de personas debe ser entre 1 y 10";
        } elseif ($_GET["error"] == "preferencia") {
            echo "La preferencia seleccionada no es válida";
        }
        ?>
    </p>
<?php endif; ?>

<form action="controllers/reserva.php" method="POST">
    <label>Nombre:</label>
    <input type="text" name="nombre" required>

    <label>Email:</label>
    <input type="email" name="email" required>

    <label>Fecha:</label>
    <input type="date" name="fecha" required>

    <label>Número de personas:</label>
    <input type="number" name="personas" min="1" max="10" required>

    <label>Preferencia:</label>
    <select name="preferencia" required>
        <option value="">Selecciona una opción</option>
        <option value="interior">Interior</option>
        <option value="terraza">Terraza</option>
    </select>

    <button type="submit">Reservar</button>
</form>
controllers/reserva.php

10) { header("Location: ../index.php?error=personas"); exit(); } if ($preferencia != "interior" && $preferencia != "terraza") { header("Location: ../index.php?error=preferencia"); exit(); } $_SESSION["reserva"] = [ "nombre" => $nombre, "email" => $email, "fecha" => $fecha, "personas" => $personas, "preferencia" => $preferencia ]; header("Location: ../confirmacion.php"); exit(); confirmacion.php
Reserva confirmada
<div class="tarjeta">
    <p>Nombre: <?= $reserva["nombre"] ?></p>
    <p>Email: <?= $reserva["email"] ?></p>
    <p>Fecha: <?= $reserva["fecha"] ?></p>
    <p>Personas: <?= $reserva["personas"] ?></p>
    <p>Preferencia: <?= $reserva["preferencia"] ?></p>
</div>

<a href="index.php">Volver al inicio</a>
CSS

body {
font-family: Arial, sans-serif;
background: #f4f4f4;
margin: 0;
color: #333;
}

header {
background: #713f12;
color: white;
text-align: center;
padding: 25px;
}

main {
max-width: 600px;
margin: 30px auto;
padding: 25px;
background: white;
border-radius: 10px;
}

form {
display: flex;
flex-direction: column;
gap: 10px;
}

input, select, button {
padding: 10px;
border: 1px solid #ccc;
border-radius: 5px;
}

button {
background: #713f12;
color: white;
cursor: pointer;
border: none;
margin-top: 10px;
}

button:hover {
background: #92400e;
}

.error {
color: #b91c1c;
background: #fee2e2;
padding: 10px;
border-radius: 5px;
}

.tarjeta {
background: #fff7ed;
padding: 20px;
border-radius: 8px;
}

footer {
text-align: center;
padding: 20px;
}

Ejercicio 6
Crea una clase para gestionar un catálogo de coches. La estructura es:

/ejercicio6
├── index.php
└── classes/
    └── Coche.php
La clase Coche debe tener propiedades privadas: id, marca, modelo, precio, kilometros, disponible.

Implementa:

Constructor que reciba todas las propiedades
Getters para todas las propiedades
Setter para precio — solo acepta valores mayores que 0
Setter para kilometros — solo acepta valores mayores o iguales a 0
Método esNuevo() — devuelve true si los kilómetros son 0
Método aplicarDescuento($porcentaje) — devuelve el precio con el descuento aplicado
Método filter($criterio) que acepte:
"disponible" — true si el coche está disponible
"nuevo" — true si los kilómetros son 0
"oferta" — true si el precio es menor o igual a 15000
El nombre de una marca — true si la marca coincide
Método pintarTarjeta() — genera el HTML de la tarjeta del coche
En index.php crea un array con mínimo 6 objetos Coche y muestra cuatro secciones usando filter():

Todos los coches
Solo los disponibles
Solo los nuevos (0 kilómetros)
Solo los que están en oferta, mostrando el precio con un 10% de descuento adicional
La página debe tener estilos propios y verse limpia.

id = $id; $this->marca = $marca; $this->modelo = $modelo; $this->precio = $precio; $this->kilometros = $kilometros; $this->disponible = $disponible; } public function getId() { return $this->id; } public function getMarca() { return $this->marca; } public function getModelo() { return $this->modelo; } public function getPrecio() { return $this->precio; } public function getKilometros() { return $this->kilometros; } public function getDisponible() { return $this->disponible; } public function setPrecio($precio) { if ($precio > 0) { $this->precio = $precio; } } public function setKilometros($kilometros) { if ($kilometros >= 0) { $this->kilometros = $kilometros; } } public function esNuevo() { return $this->kilometros == 0; } public function aplicarDescuento($porcentaje) { return $this->precio - ($this->precio * $porcentaje / 100); } public function filter($criterio) { if ($criterio == "disponible") { return $this->disponible; } elseif ($criterio == "nuevo") { return $this->esNuevo(); } elseif ($criterio == "oferta") { return $this->precio <= 15000; } else { return strtolower($this->marca) == strtolower($criterio); } } public function pintarTarjeta($descuento = false) { echo "
"; echo "
" . $this->marca . " " . $this->modelo . "
"; echo "
Precio: "; if ($descuento) { echo number_format($this->aplicarDescuento(10), 2) . " €"; echo " -10%"; } else { echo number_format($this->precio, 2) . " €"; } echo "

"; echo "
Kilómetros: " . $this->kilometros . "

"; if ($this->disponible) { echo "
Disponible

"; } else { echo "
No disponible

"; } if ($this->esNuevo()) { echo "
Nuevo

"; } echo "
"; } } ?>
index.php

<title>Catálogo de coches</title>
Catálogo de coches
1. Todos los coches
pintarTarjeta(); ?>
<h2>2. Coches disponibles</h2>
<div class="contenedor">
    <?php foreach ($coches as $coche): ?>
        <?php if ($coche->filter("disponible")): ?>
            <?php $coche->pintarTarjeta(); ?>
        <?php endif; ?>
    <?php endforeach; ?>
</div>

<h2>3. Coches nuevos</h2>
<div class="contenedor">
    <?php foreach ($coches as $coche): ?>
        <?php if ($coche->filter("nuevo")): ?>
            <?php $coche->pintarTarjeta(); ?>
        <?php endif; ?>
    <?php endforeach; ?>
</div>

<h2>4. Coches en oferta</h2>
<div class="contenedor">
    <?php foreach ($coches as $coche): ?>
        <?php if ($coche->filter("oferta")): ?>
            <?php $coche->pintarTarjeta(true); ?>
        <?php endif; ?>
    <?php endforeach; ?>
</div>
Catálogo de coches

STYLE.CSS

body {
font-family: Arial, sans-serif;
margin: 0;
background: #f1f5f9;
color: #1e293b;
}

header {
background: #1e3a8a;
color: white;
padding: 25px;
text-align: center;
}

main {
width: 90%;
max-width: 1200px;
margin: 30px auto;
}

h2 {
margin-top: 35px;
color: #1e40af;
}

.contenedor {
display: flex;
flex-wrap: wrap;
gap: 20px;
}

.coche {
width: 220px;
padding: 20px;
background: white;
border-radius: 10px;
box-shadow: 0 3px 8px #cbd5e1;
}

.coche h3 {
margin-top: 0;
}

.si {
color: #15803d;
font-weight: bold;
}

.no {
color: #dc2626;
font-weight: bold;
}

.nuevo {
background: #dbeafe;
color: #1d4ed8;
padding: 6px;
border-radius: 5px;
display: inline-block;
}

.etiqueta {
color: #dc2626;
font-weight: bold;
}

footer {
margin-top: 40px;
background: #1e3a8a;
color: white;
padding: 20px;
text-align: center;
}
