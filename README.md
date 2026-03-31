<!DOCTYPE html>
<html lang="es">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PinkLogic Planner - Hub</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #ffffff;
            color: #000000;

        }

        header {
            background-color: #ffc0cb;
            padding: 15px;
            text-align: center;
            font-size: 24px;
            font-weight: bold;
        }

        .container {
            padding: 20px;
        }

        .task-box {
            background-color: #ffe4e9;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 10px;
        }

        button {
            background-color: #ffb6c1;
            color: black;
            border: none;
            padding: 10px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
        }

        button:hover {
            opacity: 0.8;
        }

        #tarea1-div {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        input[type="checkbox"] {
            width: 20px;
            height: 20px;
            cursor: pointer;
        }
    </style>
</head>

<body>
    <header>
        PinkLogic Planner - Hub
    </header>
    <div class="container">
        <div class="task-box">
            <h3>Tarea de Español</h3>
            <div id="tarea1-div">
                <p>¿Qué son los verbos?</p>
                <button onclick="completar('tarea1-div')">Completar</button>
            </div>
        </div>
    </div>
    <button onclick="agregarTarea()">+</button>
    <script>
        function agregarTarea() {
            const taskBox = document.querySelector('.task-box');
            const nombre = prompt('¿Cuál es la tarea?');
            if (!nombre) return;
            const desc = prompt('¿Descripción? (opcional)');

            const newTaskId = tarea-${Date.now()};
            const newTaskDiv = document.createElement('div');
            newTaskDiv.id = newTaskId;
            newTaskDiv.style.display = 'flex';
            newTaskDiv.style.justifyContent = 'space-between';
            newTaskDiv.style.alignItems = 'center';
            newTaskDiv.innerHTML = `
        <div>
            <p><strong>${nombre}</strong></p>
            <p style="font-size:13px; color:gray;">${desc || ''}</p>
        </div>
        <input type="checkbox" onclick="completar('${newTaskId}')">
    `;
            taskBox.appendChild(newTaskDiv);
            guardarTareas();
        }

        function completar(id) {
            document.getElementById(id).remove();
            guardarTareas();
            const taskBox = document.querySelector('.task-box');
            if (taskBox.querySelectorAll('div').length === 0) {
                taskBox.innerHTML = '<p>Agrega una tarea haciendo clic en el botón +</p>';
            }
        }

        function guardarTareas() {
            const taskBox = document.querySelector('.task-box');
            localStorage.setItem('tareas', taskBox.innerHTML);
        }

        function cargarTareas() {
            const taskBox = document.querySelector('.task-box');
            const guardado = localStorage.getItem('tareas');
            if (guardado) taskBox.innerHTML = guardado;
        }

        cargarTareas();
        function borrar(id) {
            document.getElementById(id).remove();
        }
    </script>
</body>

</html>
