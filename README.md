<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>Recordatorio con Registro e Inicio de Sesión</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #f0f2f5, #e0e0e0);
            color: #333;
            margin: 0;
            padding: 0;
        }
        header {
            background: #007bff;
            color: #fff;
            padding: 20px;
            text-align: center;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            border-bottom: 5px solid #0056b3;
        }
        .container {
            width: 90%;
            max-width: 1200px;
            margin: auto;
            padding: 20px;
        }
        .tab-container {
            overflow: hidden;
            border-bottom: 1px solid #ddd;
            margin-top: 20px;
        }
        .tab-container button {
            background: #fff;
            border: 1px solid #ddd;
            border-bottom: none;
            padding: 15px 25px;
            cursor: pointer;
            outline: none;
            transition: background 0.3s, color 0.3s, border-color 0.3s;
            font-size: 16px;
            border-radius: 5px 5px 0 0;
        }
        .tab-container button.active {
            background: #007bff;
            color: #fff;
            border-bottom: 1px solid #007bff;
            font-weight: bold;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .tab-content {
            display: none;
            padding: 20px;
            background: #fff;
            border: 1px solid #ddd;
            border-radius: 0 0 10px 10px;
            margin-top: -1px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .tab-content.active {
            display: block;
        }
        .auth-container input[type="text"], 
        .auth-container input[type="password"], 
        .auth-container input[type="email"] {
            width: 100%;
            padding: 12px;
            margin: 10px 0;
            border: 1px solid #ddd;
            border-radius: 5px;
            box-sizing: border-box;
        }
        .auth-container button {
            background: #007bff;
            color: #fff;
            border: none;
            padding: 12px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            transition: background 0.3s;
        }
        .auth-container button:hover {
            background: #0056b3;
        }
        .note, .reminder, .alarm {
            background: #fff;
            border: 1px solid #ddd;
            padding: 20px;
            margin: 10px 0;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .note textarea, 
        .reminder textarea, 
        .alarm input[type="text"] {
            width: 100%;
            margin-bottom: 10px;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 5px;
            box-sizing: border-box;
        }
        .note button, 
        .reminder button, 
        .alarm button {
            background: #007bff;
            color: #fff;
            border: none;
            padding: 12px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            transition: background 0.3s;
        }
        .note button:hover, 
        .reminder button:hover, 
        .alarm button:hover {
            background: #0056b3;
        }
        .note-item, 
        .reminder-item, 
        .alarm-item {
            background: #f9f9f9;
            border: 1px solid #ddd;
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 5px;
            position: relative;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        .note-item button, 
        .reminder-item button, 
        .alarm-item button {
            position: absolute;
            top: 10px;
            right: 10px;
            background: #dc3545;
            color: #fff;
            border: none;
            padding: 6px 12px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
            transition: background 0.3s;
        }
        .note-item button:hover, 
        .reminder-item button:hover, 
        .alarm-item button:hover {
            background: #c82333;
        }
        #logoutButton {
            text-align: center;
            margin: 20px;
        }
        #logoutButton button {
            background: #dc3545;
            color: #fff;
            border: none;
            padding: 12px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            transition: background 0.3s;
        }
        #logoutButton button:hover {
            background: #c82333;
        }
        a {
            color: #007bff;
            text-decoration: none;
            font-weight: bold;
        }
        a:hover {
            text-decoration: underline;
        }
        .tab-container button {
            border-radius: 5px;
            border: 1px solid #007bff;
        }
        .tab-container button.active {
            border: 1px solid #0056b3;
        }
    </style>
</head>
<body>
    <header>
        <h1>Recordatorio con Registro e Inicio de Sesión</h1>
    </header>

    <div class="container">
        <!-- Pestañas -->
        <div class="tab-container">
            <button class="tab-button" onclick="showTab('register')">Registro</button>
            <button class="tab-button" onclick="showTab('login')">Iniciar Sesión</button>
            <button class="tab-button" onclick="showTab('notes')" id="notesTab">Notas</button>
            <button class="tab-button" onclick="showTab('reminders')" id="remindersTab">Recordatorios</button>
            <button class="tab-button" onclick="showTab('alarms')" id="alarmsTab">Alarmas</button>
        </div>

        <!-- Contenido de las pestañas -->
        <div id="register" class="tab-content">
            <div class="auth-container">
                <h2>Registrarse</h2>
                <input type="text" id="registerUsername" placeholder="Nombre de usuario">
                <input type="email" id="registerEmail" placeholder="Correo electrónico">
                <input type="password" id="registerPassword" placeholder="Contraseña">
                <button onclick="register()">Registrar</button>
                <p id="register-message" style="color:red;"></p>
                <p>¿Ya tienes una cuenta? <a href="#" onclick="showTab('login')">Iniciar sesión</a></p>
            </div>
        </div>

        <div id="login" class="tab-content">
            <div class="auth-container">
                <h2>Iniciar Sesión</h2>
                <input type="text" id="loginUsername" placeholder="Nombre de usuario">
                <input type="password" id="loginPassword" placeholder="Contraseña">
                <button onclick="login()">Iniciar Sesión</button>
                <p id="login-message" style="color:red;"></p>
                <p>¿No tienes una cuenta? <a href="#" onclick="showTab('register')">Registrarse</a></p>
            </div>
        </div>

        <div id="notes" class="tab-content">
            <div class="note">
                <h2>Notas</h2>
                <textarea id="noteContent" placeholder="Escribe tu nota aquí..."></textarea>
                <button onclick="addNote()">Agregar Nota</button>
                <div id="notesList">
                    <!-- Las notas se agregarán aquí dinámicamente -->
                </div>
            </div>
        </div>

        <div id="reminders" class="tab-content">
            <div class="reminder">
                <h2>Recordatorios</h2>
                <textarea id="reminderContent" placeholder="Escribe tu recordatorio aquí..."></textarea>
                <button onclick="addReminder()">Agregar Recordatorio</button>
                <div id="remindersList">
                    <!-- Los recordatorios se agregarán aquí dinámicamente -->
                </div>
            </div>
        </div>

        <div id="alarms" class="tab-content">
            <div class="alarm">
                <h2>Alarmas</h2>
                <input type="text" id="alarmTime" placeholder="Escribe la hora de la alarma (ej: 14:30)">
                <button onclick="setAlarm()">Configurar Alarma</button>
                <div id="alarmsList">
                    <!-- Las alarmas se agregarán aquí dinámicamente -->
                </div>
            </div>
        </div>
    </div>

    <!-- Botón de Cierre de Sesión -->
    <div id="logoutButton" style="display:none;">
        <button onclick="logout()">Cerrar Sesión</button>
    </div>

    <script>
        function showTab(tabId) {
            const tabs = document.querySelectorAll('.tab-content');
            const tabButtons = document.querySelectorAll('.tab-button');
            const currentUser = localStorage.getItem('currentUser');

            tabs.forEach(tab => {
                tab.classList.remove('active');
            });
            tabButtons.forEach(button => {
                button.classList.remove('active');
            });

            const selectedTab = document.getElementById(tabId);
            if (tabId === 'notes' || tabId === 'reminders' || tabId === 'alarms') {
                if (!currentUser) {
                    alert('Debes iniciar sesión para acceder a estas secciones.');
                    showTab('login');
                    return;
                }
            }

            selectedTab.classList.add('active');
            document.querySelector(`.tab-button[onclick="showTab('${tabId}')"]`).classList.add('active');
        }

        function register() {
            const username = document.getElementById('registerUsername').value;
            const email = document.getElementById('registerEmail').value;
            const password = document.getElementById('registerPassword').value;
            const registerMessage = document.getElementById('register-message');
            
            if (username.trim() === '' || email.trim() === '' || password.trim() === '') {
                registerMessage.textContent = 'Todos los campos son obligatorios.';
                return;
            }

            const users = JSON.parse(localStorage.getItem('users')) || [];
            if (users.some(user => user.username === username)) {
                registerMessage.textContent = 'Nombre de usuario ya registrado.';
                return;
            }

            users.push({ username, email, password });
            localStorage.setItem('users', JSON.stringify(users));
            registerMessage.textContent = 'Registro exitoso. Ahora puedes iniciar sesión.';
        }

        function login() {
            const username = document.getElementById('loginUsername').value;
            const password = document.getElementById('loginPassword').value;
            const loginMessage = document.getElementById('login-message');
            
            if (username.trim() === '' || password.trim() === '') {
                loginMessage.textContent = 'Nombre de usuario y contraseña son obligatorios.';
                return;
            }

            const users = JSON.parse(localStorage.getItem('users')) || [];
            const user = users.find(user => user.username === username && user.password === password);
            if (user) {
                localStorage.setItem('currentUser', username);
                document.getElementById('logoutButton').style.display = 'block';
                showTab('notes');
                loginMessage.textContent = '';
            } else {
                loginMessage.textContent = 'Nombre de usuario o contraseña incorrectos.';
            }
        }

        function addNote() {
            const noteContent = document.getElementById('noteContent').value;
            if (noteContent.trim() === '') {
                alert('Por favor, escribe algo en la nota.');
                return;
            }
            const notes = JSON.parse(localStorage.getItem('notes')) || [];
            notes.push(noteContent);
            localStorage.setItem('notes', JSON.stringify(notes));
            displayNotes();
            document.getElementById('noteContent').value = '';
        }

        function addReminder() {
            const reminderContent = document.getElementById('reminderContent').value;
            if (reminderContent.trim() === '') {
                alert('Por favor, escribe el recordatorio.');
                return;
            }
            const reminders = JSON.parse(localStorage.getItem('reminders')) || [];
            reminders.push(reminderContent);
            localStorage.setItem('reminders', JSON.stringify(reminders));
            displayReminders();
            document.getElementById('reminderContent').value = '';
        }

        function setAlarm() {
            const alarmTime = document.getElementById('alarmTime').value;
            if (alarmTime.trim() === '') {
                alert('Por favor, escribe la hora de la alarma.');
                return;
            }
            const alarms = JSON.parse(localStorage.getItem('alarms')) || [];
            alarms.push(alarmTime);
            localStorage.setItem('alarms', JSON.stringify(alarms));
            displayAlarms();
            document.getElementById('alarmTime').value = '';
        }

        function loadUserData() {
            displayNotes();
            displayReminders();
            displayAlarms();
        }

        function displayNotes() {
            const notes = JSON.parse(localStorage.getItem('notes')) || [];
            const notesList = document.getElementById('notesList');
            notesList.innerHTML = '';
            notes.forEach((note, index) => {
                const noteItem = document.createElement('div');
                noteItem.className = 'note-item';
                noteItem.innerHTML = `${note} <button onclick="removeNote(${index})">Eliminar</button>`;
                notesList.appendChild(noteItem);
            });
        }

        function displayReminders() {
            const reminders = JSON.parse(localStorage.getItem('reminders')) || [];
            const remindersList = document.getElementById('remindersList');
            remindersList.innerHTML = '';
            reminders.forEach((reminder, index) => {
                const reminderItem = document.createElement('div');
                reminderItem.className = 'reminder-item';
                reminderItem.innerHTML = `${reminder} <button onclick="removeReminder(${index})">Eliminar</button>`;
                remindersList.appendChild(reminderItem);
            });
        }

        function displayAlarms() {
            const alarms = JSON.parse(localStorage.getItem('alarms')) || [];
            const alarmsList = document.getElementById('alarmsList');
            alarmsList.innerHTML = '';
            alarms.forEach((alarm, index) => {
                const alarmItem = document.createElement('div');
                alarmItem.className = 'alarm-item';
                alarmItem.innerHTML = `Alarma a las ${alarm} <button onclick="removeAlarm(${index})">Eliminar</button>`;
                alarmsList.appendChild(alarmItem);
            });
        }

        function removeNote(index) {
            const notes = JSON.parse(localStorage.getItem('notes')) || [];
            notes.splice(index, 1);
            localStorage.setItem('notes', JSON.stringify(notes));
            displayNotes();
        }

        function removeReminder(index) {
            const reminders = JSON.parse(localStorage.getItem('reminders')) || [];
            reminders.splice(index, 1);
            localStorage.setItem('reminders', JSON.stringify(reminders));
            displayReminders();
        }

        function removeAlarm(index) {
            const alarms = JSON.parse(localStorage.getItem('alarms')) || [];
            alarms.splice(index, 1);
            localStorage.setItem('alarms', JSON.stringify(alarms));
            displayAlarms();
        }

        function logout() {
            localStorage.removeItem('currentUser');
            document.getElementById('logoutButton').style.display = 'none';
            showTab('login');
        }

        window.onload = function() {
            const currentUser = localStorage.getItem('currentUser');
            if (currentUser) {
                document.getElementById('logoutButton').style.display = 'block';
                showTab('notes');
                loadUserData();
            } else {
                showTab('login');
            }
        };
    </script>
</body>
</html>
