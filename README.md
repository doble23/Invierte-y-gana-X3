

<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Grupo Inversión 3X</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: Arial, sans-serif; background: #f4f4f4; color: #333; }

    header { background: #0a3d62; color: white; padding: 20px; text-align: center; }

    nav { text-align: center; margin-top: 20px; }
    nav a {
      margin: 10px;
      text-decoration: none;
      background: #1e90ff;
      color: white;
      padding: 10px 20px;
      border-radius: 8px;
      cursor: pointer;
    }

    form {
      max-width: 400px;
      margin: 30px auto;
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    form input {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    form button {
      padding: 10px 20px;
      background: #27ae60;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    .panel {
      display: none;
      padding: 20px;
    }

    .top-box {
      background: #1976d2;
      padding: 15px;
      color: white;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .logo { font-weight: bold; font-size: 16px; }
    .logo span { color: yellow; }
    .credit {
      background: white;
      color: #1976d2;
      padding: 5px 12px;
      border-radius: 20px;
      font-weight: bold;
      font-size: 14px;
    }

    .balance-box, .investment-section {
      background: white;
      margin: 15px;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      text-align: center;
    }
    .big-amount { font-size: 26px; font-weight: bold; margin-bottom: 8px; }
    .available { color: green; }
    .frozen { color: red; margin-top: 4px; }

    select, button, input[type="file"] {
      padding: 10px;
      font-size: 16px;
      margin: 10px 0;
      width: 100%;
      border: 1px solid #ccc;
      border-radius: 5px;
    }

    .investment-table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
    }
    .investment-table th, .investment-table td {
      padding: 10px;
      text-align: center;
      border: 1px solid #ddd;
    }
    .investment-table th {
      background-color: #1976d2;
      color: white;
    }

    .bottom-nav {
      position: fixed;
      bottom: 0;
      width: 100%;
      background: white;
      display: none;
      justify-content: space-around;
      border-top: 1px solid #ccc;
      padding: 6px 0;
    }
    .bottom-nav div {
      text-align: center;
      font-size: 12px;
      cursor: pointer;
    }

    .modal {
      display: none;
      position: fixed;
      z-index: 99;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0,0,0,0.5);
      justify-content: center;
      align-items: center;
    }
    .modal-content {
      background-color: white;
      padding: 20px;
      border-radius: 10px;
      width: 90%;
      max-width: 400px;
      text-align: center;
    }
    .pago-info { margin-top: 10px; display: none; }

    footer {
      text-align: center;
      padding: 20px;
      background: #0a3d62;
      color: white;
      margin-top: 80px;
    }
  </style>
</head>
<body>

  <header>
    <h1>Grupo de Inversión 3X</h1>
    <p>Invierte hoy, gana el triple mañana</p>
  </header>

  <nav id="navPrincipal">
    <a onclick="mostrar('registro')">Registrarse</a>
    <a onclick="mostrar('login')">Iniciar Sesión</a>
  </nav>

  <!-- Registro -->
  <section id="registroForm">
    <form onsubmit="registrarUsuario(event)">
      <h3>Crear cuenta</h3>
      <input type="text" id="nombreInput" placeholder="Nombre completo" required>
      <input type="text" placeholder="Número de cédula" required>
      <input type="text" placeholder="Ciudad" required>
      <input type="tel" placeholder="Teléfono" required>
      <input type="password" placeholder="Contraseña" required>
      <button type="submit">Registrarme</button>
    </form>
  </section>

  <!-- Login -->
  <section id="loginForm">
    <form onsubmit="iniciarSesion(event)">
      <h3>Iniciar Sesión</h3>
      <input type="email" placeholder="Correo electrónico" required>
      <input type="password" placeholder="Contraseña" required>
      <button type="submit">Entrar</button>
    </form>
  </section>

  <!-- Panel Usuario -->
  <section class="panel" id="panelUsuario">
    <div class="top-box">
      <div class="logo">Invierte y <span>gana</span> 3 veces</div>
      <div class="credit">Crédito: 95</div>
    </div>

    <div class="balance-box">
      <div class="big-amount" id="saldoTotal">$: 0</div>
      <div class="available" id="saldoDisponible">$: 0 Saldo disponible</div>
      <div class="frozen">$0 Cantidad congelada</div>
    </div>

    <div class="investment-section">
      <h3>Simular Inversión</h3>
      <select id="montoInversion">
        <option value="500000">$500.000</option>
        <option value="1000000">$1.000.000</option>
        <option value="2000000">$2.000.000</option>
        <option value="5000000">$5.000.000</option>
        <option value="10000000">$10.000.000</option>
      </select>
      <button onclick="mostrarModal()">Invertir y ganar 3x</button>

      <h3 style="margin-top: 30px;">Rango de Inversión y Ganancia</h3>
      <table class="investment-table">
        <thead>
          <tr><th>Inversión</th><th>Ganancia 3x</th></tr>
        </thead>
        <tbody>
          <tr><td>$500.000</td><td>$1.500.000</td></tr>
          <tr><td>$1.000.000</td><td>$3.000.000</td></tr>
          <tr><td>$2.000.000</td><td>$6.000.000</td></tr>
          <tr><td>$5.000.000</td><td>$15.000.000</td></tr>
          <tr><td>$10.000.000</td><td>$30.000.000</td></tr>
        </tbody>
      </table>
    </div>
  </section>

  <!-- Menú inferior -->
  <div class="bottom-nav" id="navUsuario">
    <div onclick="mostrarAlerta('Inicio')"><i>🏠</i>Inicio</div>
    <div onclick="mostrarPerfil()"><i>👤</i>Yo</div>
  </div>

  <!-- Modal Pago -->
  <div class="modal" id="modalPago">
    <div class="modal-content">
      <h3>Selecciona un método de pago</h3>
      <select id="metodoPago" onchange="mostrarInfoPago()">
        <option value="">-- Elegir método --</option>
        <option value="paypal">PayPal</option>
        <option value="nequi">Nequi</option>
        <option value="bancolombia">Bancolombia</option>
      </select>

      <div class="pago-info" id="infoNequi">
        <p>📱 Número Nequi: <strong>3135343055</strong></p>
        <label>Adjuntar foto del recibo:</label>
        <input type="file" accept="image/*" id="reciboNequi">
      </div>

      <div class="pago-info" id="infoPaypal">
        <p>👉 Usa tu cuenta PayPal para enviar el pago.</p>
      </div>

      <div class="pago-info" id="infoBancolombia">
        <p>🏦 Realiza la transferencia a Bancolombia.</p>
      </div>

      <button onclick="cerrarModal()">Cerrar</button>
    </div>
  </div>

  <!-- Modal Perfil -->
  <div class="modal" id="modalPerfil">
    <div class="modal-content">
      <h3>Perfil del Usuario</h3>
      <p><strong>Nombre:</strong> <span id="nombreUsuario"></span></p>
      <p><strong>Total Invertido:</strong> $<span id="totalInvertido">0</span></p>
      <p><strong>Ganancia (x3):</strong> $<span id="totalGanado">0</span></p>
      <button onclick="cerrarPerfil()">Cerrar</button>
    </div>
  </div>

  <footer>
    <p>&copy; 2025 Grupo de Inversión 3X. Todos los derechos reservados.</p>
  </footer>

  <script>
    let saldo = 0;
    let totalInvertido = 0;
    let nombre = "";

    function mostrar(seccion) {
      document.getElementById('registroForm').style.display = 'none';
      document.getElementById('loginForm').style.display = 'none';
      document.getElementById('panelUsuario').style.display = 'none';
      document.getElementById('modalPerfil').style.display = 'none';
      document.getElementById('navPrincipal').style.display = 'block';
      document.getElementById('navUsuario').style.display = 'none';

      if (seccion === 'registro') {
        document.getElementById('registroForm').style.display = 'block';
      } else if (seccion === 'login') {
        document.getElementById('loginForm').style.display = 'block';
      }
    }

    function registrarUsuario(e) {
      e.preventDefault();
      nombre = document.getElementById("nombreInput").value;
      document.getElementById('registroForm').style.display = 'none';
      document.getElementById('panelUsuario').style.display = 'block';
      document.getElementById('navPrincipal').style.display = 'none';
      document.getElementById('navUsuario').style.display = 'flex';
      actualizarSaldo();
    }

    function iniciarSesion(e) {
      e.preventDefault();
      nombre = "Usuario"; // Simulado
      document.getElementById('loginForm').style.display = 'none';
      document.getElementById('panelUsuario').style.display = 'block';
      document.getElementById('navPrincipal').style.display = 'none';
      document.getElementById('navUsuario').style.display = 'flex';
      actualizarSaldo();
    }

    function actualizarSaldo() {
      document.getElementById("saldoTotal").textContent = `$: ${saldo.toLocaleString()}`;
      document.getElementById("saldoDisponible").textContent = `$: ${saldo.toLocaleString()} Saldo disponible`;
    }

    function mostrarAlerta(nombre) {
      alert("Haz presionado: " + nombre);
    }

    function mostrarModal() {
      document.getElementById("modalPago").style.display = "flex";
    }

    function cerrarModal() {
      const metodo = document.getElementById("metodoPago").value;
      const monto = parseInt(document.getElementById("montoInversion").value);

      if (metodo === "nequi" && document.getElementById("reciboNequi").files.length > 0) {
        const ganancia = monto * 3;
        saldo += ganancia;
        totalInvertido += monto;
        actualizarSaldo();
        alert(`Inversión confirmada: ganancia $${ganancia.toLocaleString()}`);
      }

      document.getElementById("modalPago").style.display = "none";
      document.getElementById("metodoPago").value = "";
      ocultarInfoPago();
    }

    function mostrarInfoPago() {
      ocultarInfoPago();
      const metodo = document.getElementById("metodoPago").value;
      if (metodo === "nequi") {
        document.getElementById("infoNequi").style.display = "block";
      } else if (metodo === "paypal") {
        document.getElementById("infoPaypal").style.display = "block";
      } else if (metodo === "bancolombia") {
        document.getElementById("infoBancolombia").style.display = "block";
      }
    }

    function ocultarInfoPago() {
      document.querySelectorAll('.pago-info').forEach(div => div.style.display = 'none');
    }

    function mostrarPerfil() {
      document.getElementById("nombreUsuario").textContent = nombre || "No disponible";
      document.getElementById("totalInvertido").textContent = totalInvertido.toLocaleString();
      document.getElementById("totalGanado").textContent = (totalInvertido * 3).toLocaleString();
      document.getElementById("modalPerfil").style.display = "flex";
    }

    function cerrarPerfil() {
      document.getElementById("modalPerfil").style.display = "none";
    }

    window.onload = () => {
      mostrar('registro');
    };
  </script>
</body>
</html>


