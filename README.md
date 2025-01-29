<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IA de Matemáticas y Física</title>
    <link rel="stylesheet" href="estilos.css">
</head>
<body>
    <header>
        <h1>IA de Matemáticas y Física</h1>
    </header>
    <main>
        <section class="contenedor-imagen">
            <input type="file" id="imagen-problema" accept=".jpg, .jpeg, .png">
            <button id="analizar-imagen">Analizar imagen</button>
        </section>
        <section class="contenedor-texto">
            <textarea id="texto-problema" placeholder="Escribe el problema aquí"></textarea>
            <button id="resolver-problema">Resolver problema</button>
        </section>
        <section class="contenedor-solucion">
            <div id="pasos-solucion"></div>
            <div id="resultado-solucion"></div>
        </section>
    </main>

    <!-- Script que carga los estilos y funcionalidades -->
    <script src="script.js"></script>

</body>

</html>
body {
  font-family: Arial, sans-serif;
  background-color: #f2f2f2;
}

header {
  background-color: #333;
  color: #fff;
  padding: 20px;
  text-align: center;
}

main {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.contenedor-imagen {
  margin-bottom: 20px;
}

#imagen-problema {
  width: 100%;
}

#analizar-imagen {
  background-color: #4CAF50;
  color: #fff;
  padding: 10px;
}

.contenedor-texto {
 margin-bottom :20px;

}
#texto-problema{
width :100%;
height :150px ;
padding :10px ;

}
#resolver-problema{
background-color :#4CAF50 ;
color:#fff ;
padding :10px ;


}
.contenedor-solucion{
margin-top :20px;

}
#pasos-solucion{

font-size :18px;

}
#resultado-solucion{

font-size :24px ;
font-weight:bold ;

background-color:#ccc ;
padding :10px;


border-radius :5PX ;


}

// Función que analiza la imagen del problema
function analizarImagen() {
 // Código para analizar la imagen del problema 
 console.log("Analizando imagen...");
 // Obtenemos la imagen seleccionada por el usuario 
 let imagen = document.getElementById("imagen-problema").files[0];
 // Enviamos la imagen al servidor para su análisis 
 fetch("/analizar-imagen", {
 method:"POST",
 body:new FormData(document.getElementById("formulario-imagen")),
 headers:{'Content-Type': 'multipart/form-data'}
 })
 .then(respuesta => respuesta.json())
 .then(data => {

//Mostramos los pasos de solución 

document.getElementById("pasos-solucion").innerHTML = data.pasos.join("<br>");

// Mostramos resultado 


document.getElementById("resultado-solucion").innerHTML = "Resultado:<br>" + data.resultado ;

})
.catch(error => console.error(error));




}


// Función que resuelve el problema mediante texto 
function resolverProblema() {

console.log ("resolviendo texto ...")

let textoProblema = document.getElementById ("texto-problema").value ;

fetch ("/resolver-texto",{

method:"POST",
headers:{'Content-Type': 'application/json'},
body:textoProblema

})

.then(respuesta=>respuesta.json())

.then(data=>{


document.getElementById ("pasos-solucion").innerHTML=data.pasos.join("<br>");

document.getElementById ("resultado-solucion").innerHTML= "Resultado:<br>" +data.resultado;



})

.catch(error=>console.error(error));





}


// Agregamos eventos a los botones 

document.getElementById("analizar-imagen").addEventListener("click", analizarImagen);
document.getElementById("resolver-problema").addEventListener("click", resolverProblema);






