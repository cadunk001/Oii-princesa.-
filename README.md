<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Um Pedido Especial</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            background-color: #000; /* Fundo preto */
            color: #d8b4fe; /* Lilás claro para o texto principal */
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start; /* Alinhar o conteúdo ao topo inicialmente */
            min-height: 100vh;
            padding-top: 20px; /* Espaçamento superior */
        }

        #content {
            background-color: #1e0038; /* Roxo mais escuro */
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 0 20px rgba(173, 127, 168, 0.3); /* Sombra lilás */
            text-align: center;
            z-index: 10;
            max-width: 800px; /* Largura máxima para um layout clean */
            margin: 0 auto; /* Centralizar horizontalmente */
        }

        h1, h2 {
            color: #f5e0ff; /* Lilás mais claro para os títulos */
            margin-bottom: 20px;
        }

        #image-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .image-container {
            width: 100%;
            overflow: hidden;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(173, 127, 168, 0.1);
            transition: transform 0.3s ease-in-out;
        }

        .image-container:hover {
            transform: scale(1.03);
        }

        .image-container img {
            width: 100%;
            height: auto;
            display: block;
        }

        #upload-section {
            margin-bottom: 30px;
        }

        #message-section {
            margin-bottom: 30px;
        }

        #message {
            width: 100%;
            padding: 15px;
            border: 1px solid #a685e2; /* Borda lilás */
            border-radius: 8px;
            box-sizing: border-box;
            margin-top: 15px;
            font-size: 16px;
            text-align: center;
            background-color: #38006b; /* Roxo mais escuro */
            color: #d8b4fe;
        }

        #proposal-button {
            background-color: #a685e2; /* Lilás */
            color: #fff;
            border: none;
            padding: 18px 40px;
            border-radius: 30px;
            font-size: 20px;
            cursor: pointer;
            transition: background-color 0.3s ease-in-out, transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
        }

        #proposal-button:hover {
            background-color: #8c6bb8; /* Lilás mais escuro no hover */
            transform: scale(1.05);
            box-shadow: 0 5px 10px rgba(173, 127, 168, 0.2);
        }

        #proposal-button.clicked {
            background-color: #634a9e; /* Roxo ainda mais escuro ao clicar */
            transform: scale(0.95);
        }

        #proposal-response {
            margin-top: 30px;
            font-size: 1.3em;
            font-weight: bold;
            color: #f5e0ff;
        }
    </style>
</head>
<body>
    <div id="content">
        <h1>Um Pedido Especial para Você</h1>

        <div id="upload-section">
            <h2>Nossas Lembranças</h2>
            <input type="file" id="image-upload" multiple accept="image/*" style="margin-bottom: 15px; color: #a685e2;">
            <div id="image-grid">
                </div>
        </div>

        <div id="message-section">
            <h2>Minha Mensagem</h2>
            <textarea id="message" rows="4" placeholder="Digite aqui a sua mensagem especial..." style="background-color: #38006b; color: #d8b4fe; border-color: #a685e2;"></textarea>
        </div>

        <button id="proposal-button">
            <span id="button-text">aperte aqui</span>
        </button>
        <div id="proposal-response"></div>
    </div>

    <script>
        const imageUpload = document.getElementById('image-upload');
        const imageGrid = document.getElementById('image-grid');
        const messageInput = document.getElementById('message');
        const proposalButton = document.getElementById('proposal-button');
        const proposalResponse = document.getElementById('proposal-response');
        const buttonText = document.getElementById('button-text');

        let images = [];

        // Carregar imagens salvas localmente
        if (localStorage.getItem('romantic_images')) {
            images = JSON.parse(localStorage.getItem('romantic_images'));
            displayImages();
        }

        // Carregar mensagem salva localmente
        if (localStorage.getItem('romantic_message')) {
            messageInput.value = localStorage.getItem('romantic_message');
        }

        imageUpload.addEventListener('change', (event) => {
            const files = event.target.files;
            for (const file of files) {
                const reader = new FileReader();
                reader.onload = (e) => {
                    images.push(e.target.result);
                    localStorage.setItem('romantic_images', JSON.stringify(images));
                    displayImages();
                };
                reader.readAsDataURL(file);
            }
            // Limpar o input para permitir carregar a mesma imagem novamente
            imageUpload.value = '';
        });

        messageInput.addEventListener('input', () => {
            localStorage.setItem('romantic_message', messageInput.value);
        });

        function displayImages() {
            imageGrid.innerHTML = '';
            images.forEach(imageUrl => {
                const container = document.createElement('div');
                container.classList.add('image-container');
                const img = document.createElement('img');
                img.src = imageUrl;
                container.appendChild(img);
                imageGrid.appendChild(container);
            });
        }

        proposalButton.addEventListener('click', () => {
            proposalButton.classList.add('clicked');
            buttonText.textContent = 'Quer namorar comigo?';
            proposalResponse.textContent = 'Estou ansioso pela sua resposta! 🥰';
            // Aqui você pode adicionar mais ações, como redirecionar para outra página
        });
    </script>
</body>
</html>
