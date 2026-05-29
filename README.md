<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Generador Pro de Contraseñas</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-slate-900 text-white flex items-center justify-center min-h-screen">

    <div class="bg-slate-800 p-8 rounded-2xl shadow-2xl w-full max-w-md border border-slate-700">
        <h1 class="text-2xl font-bold mb-6 text-center text-indigo-400">Generador Seguro</h1>
        
        <div class="relative mb-6">
            <input type="text" id="passwordResult" readonly 
                class="w-full bg-slate-950 border border-slate-600 p-4 rounded-lg text-xl font-mono text-emerald-400 focus:outline-none"
                placeholder="Haz clic en Generar">
        </div>

        <div class="space-y-4">
            <div>
                <label class="block text-sm mb-2">Longitud: <span id="lengthVal" class="font-bold text-indigo-300">16</span></label>
                <input type="range" id="length" min="8" max="50" value="16" 
                    class="w-full h-2 bg-slate-700 rounded-lg appearance-none cursor-pointer accent-indigo-500">
            </div>

            <button onclick="generatePassword()" 
                class="w-full bg-indigo-600 hover:bg-indigo-500 transition-colors py-3 rounded-lg font-bold text-white shadow-lg active:scale-95 transform">
                GENERAR CONTRASEÑA
            </button>
        </div>

        <p class="mt-4 text-xs text-slate-500 text-center uppercase tracking-widest">
            Cifrado Aleatorio Criptográfico
        </p>
    </div>

    <script>
        const lengthInput = document.getElementById('length');
        const lengthVal = document.getElementById('lengthVal');
        const passwordResult = document.getElementById('passwordResult');

        // Actualizar el número visual de la longitud
        lengthInput.addEventListener('input', () => {
            lengthVal.textContent = lengthInput.value;
        });

        function generatePassword() {
            const length = lengthInput.value;
            const charset = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*()_+~`|}{[]:;?><,./-=";
            let password = "";
            
            // Usamos crypto para máxima seguridad
            const array = new Uint32Array(length);
            window.crypto.getRandomValues(array);

            for (let i = 0; i < length; i++) {
                password += charset[array[i] % charset.length];
            }

            passwordResult.value = password;
            
            // Efecto visual al generar
            passwordResult.classList.add('ring-2', 'ring-emerald-500');
            setTimeout(() => passwordResult.classList.remove('ring-2', 'ring-emerald-500'), 300);
        }

        // Generar una al cargar la página
        window.onload = generatePassword;
    </script>
</body>
</html>
