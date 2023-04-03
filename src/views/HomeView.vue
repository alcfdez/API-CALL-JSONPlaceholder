<script setup>

async function obtenerUsuarios() {
  const respuesta = await fetch('https://jsonplaceholder.typicode.com/users');
  const usuarios = await respuesta.json();
  const tabla = document.createElement('table');
  const encabezado = tabla.insertRow();
  const idHeader = encabezado.insertCell();
  const nombreHeader = encabezado.insertCell();
  const ciudadHeader = encabezado.insertCell();
  idHeader.innerText = 'ID';
  nombreHeader.innerText = 'Nombre';
  ciudadHeader.innerText = 'Ciudad';
  
  usuarios.forEach(usuario => {
    const fila = tabla.insertRow();
    const idCell = fila.insertCell();
    const nombreCell = fila.insertCell();
    const ciudadCell = fila.insertCell();
    idCell.innerText = usuario.id;
    nombreCell.innerText = usuario.name;
    ciudadCell.innerText = usuario.address.city;
  });

  document.body.appendChild(tabla);
}

obtenerUsuarios();

async function obtenerUsuarioPorId(id) {
  const respuesta = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`);
  const usuario = await respuesta.json();
  return usuario;
}

function mostrarUsuario(usuario) {
  const resultado = document.createElement('div');
  resultado.innerHTML = `<p>Nombre: ${usuario.name}</p><p>Teléfono: ${usuario.phone}</p>`;
  document.body.appendChild(resultado);
}

const input = document.createElement('input');
input.type = 'number';
input.placeholder = 'Ingrese un ID de usuario';
const boton = document.createElement('button');
boton.innerText = 'Buscar';
boton.addEventListener('click', async () => {
  const id = input.value;
  const usuario = await obtenerUsuarioPorId(id);
  mostrarUsuario(usuario);
});

document.body.appendChild(input);
document.body.appendChild(boton);

</script>

<template>

</template>
