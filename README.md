```html
<!DOCTYPE html>
<html lang="pt-BR">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Meu Feed</title>

    <style>

        /* =========================
           CONFIGURAÇÕES GERAIS
        ========================= */

        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background: #111;
            color: white;
        }


        /* =========================
           CABEÇALHO
        ========================= */

        header {
            position: sticky;
            top: 0;

            display: flex;
            justify-content: space-between;
            align-items: center;

            padding: 15px 20px;

            background: #181818;
            border-bottom: 1px solid #333;

            z-index: 1000;
        }

        header h1 {
            margin: 0;
            font-size: 24px;
        }

        #informacoes {
            display: flex;
            gap: 15px;
            font-size: 14px;
        }


        /* =========================
           STORIES
        ========================= */

        #stories {
            max-width: 600px;
            margin: 20px auto;

            display: flex;
            gap: 15px;

            overflow-x: auto;
            padding: 10px;
        }

        .story {
            display: flex;
            flex-direction: column;
            align-items: center;

            min-width: 70px;
            font-size: 12px;
        }

        .story-foto {
            width: 60px;
            height: 60px;

            display: flex;
            align-items: center;
            justify-content: center;

            border-radius: 50%;
            border: 3px solid #e1306c;

            background: #333;

            font-size: 25px;
            margin-bottom: 5px;
        }


        /* =========================
           FEED
        ========================= */

        #feed {
            max-width: 500px;
            margin: auto;
        }


        /* =========================
           POSTS
        ========================= */

        .post {
            background: #1c1c1c;

            margin-bottom: 20px;

            border: 1px solid #333;
            border-radius: 10px;

            overflow: hidden;
        }


        /* =========================
           USUÁRIO
        ========================= */

        .usuario {
            display: flex;
            align-items: center;

            padding: 12px;
        }

        .foto-perfil {
            width: 42px;
            height: 42px;

            display: flex;
            align-items: center;
            justify-content: center;

            border-radius: 50%;

            background: #555;

            margin-right: 10px;

            font-size: 20px;
        }


        /* =========================
           IMAGEM DO POST
        ========================= */

        .imagem-post {
            width: 100%;
            height: 350px;

            object-fit: cover;
            display: block;

            background: #333;
        }


        /* =========================
           BOTÕES
        ========================= */

        .acoes {
            display: flex;
            gap: 15px;

            padding: 12px;
        }

        .botao {
            background: none;
            border: none;

            font-size: 25px;
            cursor: pointer;
        }

        .botao:hover {
            transform: scale(1.1);
        }


        /* =========================
           CONTEÚDO
        ========================= */

        .conteudo {
            padding: 0 12px 15px;
        }

        .curtidas {
            font-weight: bold;
            margin-bottom: 8px;
        }

        .conteudo p {
            margin: 5px 0;
        }


        /* =========================
           POST PREMIADO
        ========================= */

        .post-recompensa {
            border: 2px solid gold;
            background: #302800;
        }

        .recompensa-imagem {
            height: 350px;

            display: flex;
            align-items: center;
            justify-content: center;

            font-size: 100px;

            background: #4a3d00;
        }


        /* =========================
           RESPONSIVIDADE
        ========================= */

        @media (max-width: 600px) {

            header h1 {
                font-size: 18px;
            }

            #informacoes {
                gap: 8px;
                font-size: 12px;
            }

            #feed {
                width: 100%;
            }

            .post {
                border-radius: 0;
                border-left: none;
                border-right: none;
            }

        }

    </style>
</head>


<body>

    <!-- CABEÇALHO -->

    <header>

        <h1>Meu Feed</h1>

        <div id="informacoes">

            <div id="tempo">
                ⏱️ 00:00
            </div>

            <div id="moedas">
                🪙 0
            </div>

        </div>

    </header>


    <!-- STORIES -->

    <div id="stories"></div>


    <!-- FEED -->

    <div id="feed"></div>


    <script>

        // =========================
        // CONTADOR DE TEMPO
        // =========================

        let segundos = 0;

        setInterval(() => {

            segundos++;

            const minutos = Math.floor(segundos / 60);
            const segundosRestantes = segundos % 60;

            document.getElementById("tempo").textContent =
                `⏱️ ${String(minutos).padStart(2, "0")}:${String(segundosRestantes).padStart(2, "0")}`;

        }, 1000);


        // =========================
        // SISTEMA DE MOEDAS
        // =========================

        let moedas = 0;


        // =========================
        // CONTADOR DE POSTS
        // =========================

        let contador = 0;


        // =========================
        // PRÓXIMA RECOMPENSA
        // =========================

        let proximaRecompensa =
            Math.floor(Math.random() * 10) + 5;


        // =========================
        // GERADOR DE USUÁRIOS
        // =========================

        function gerarUsuario() {

            const nomes = [
                "joao", "maria", "pedro", "ana",
                "lucas", "carla", "gabriel",
                "juliana", "rafael", "beatriz",
                "felipe", "camila", "gustavo",
                "isabela", "bruno", "leticia",
                "matheus", "amanda", "vinicius",
                "fernanda", "diego", "mariana",
                "leonardo", "bianca", "thiago",
                "larissa", "daniel", "patricia",
                "henrique", "gabriela"
            ];


            const sobrenomes = [
                "silva", "santos", "oliveira",
                "costa", "souza", "ferreira",
                "rodrigues", "almeida", "pereira",
                "lima", "gomes", "ribeiro",
                "carvalho", "martins", "araujo",
                "barbosa", "rocha", "teixeira",
                "mendes", "cardoso", "correa",
                "nascimento", "dias", "castro",
                "moreira"
            ];


            const nomeAleatorio =
                nomes[Math.floor(Math.random() * nomes.length)];

            const sobrenomeAleatorio =
                sobrenomes[
                    Math.floor(Math.random() * sobrenomes.length)
                ];

            const numero =
                Math.floor(Math.random() * 1000);


            return `${nomeAleatorio}.${sobrenomeAleatorio}${numero}`;
        }


        // =========================
        // LEGENDAS
        // =========================

        const legendas = [
            "Curtindo o dia! ☀️",
            "Mais um momento especial! ✨",
            "Um dia de cada vez. 🚀",
            "Quem mais gosta disso? 😄",
            "Pequenos momentos fazem grandes dias.",
            "Aproveitando cada instante! 📸",
            "Uma lembrança para guardar.",
            "Hoje foi um bom dia! 😊",
            "Vivendo novas experiências. 🌎",
            "Nada melhor do que aproveitar o momento!"
        ];


        function gerarLegenda() {

            return legendas[
                Math.floor(Math.random() * legendas.length)
            ];

        }


        // =========================
        // IMAGENS
        // =========================

        function gerarImagem() {

            const numero =
                Math.floor(Math.random() * 1000);

            return `https://picsum.photos/600/600?random=${numero}`;

        }


        // =========================
        // OBSERVAR RECOMPENSA
        // =========================

        function observarRecompensa(post) {

            const observador = new IntersectionObserver(

                (entradas) => {

                    entradas.forEach((entrada) => {

                        if (entrada.isIntersecting) {

                            // Verifica se a recompensa
                            // já foi coletada

                            if (
                                post.dataset.recompensaColetada !==
                                "true"
                            ) {

                                // Adiciona uma moeda

                                moedas++;


                                // Atualiza o contador

                                document.getElementById(
                                    "moedas"
                                ).textContent =
                                    `🪙 ${moedas}`;


                                // Marca como coletada

                                post.dataset.recompensaColetada =
                                    "true";


                                // Altera a mensagem

                                const mensagem =
                                    post.querySelector(
                                        ".mensagem-recompensa"
                                    );


                                mensagem.textContent =
                                    "🪙 Moeda coletada!";


                                // Para de observar
                                // esse post

                                observador.unobserve(post);

                            }

                        }

                    });

                },

                {
                    // Pelo menos 50% do post
                    // precisa estar visível

                    threshold: 0.5
                }

            );


            // Começa a observar o post

            observador.observe(post);

        }


        // =========================
        // CRIAR STORIES
        // =========================

        function carregarStories() {

            const stories =
                document.getElementById("stories");


            for (let i = 0; i < 8; i++) {

                const usuario =
                    gerarUsuario();


                const story =
                    document.createElement("div");


                story.className =
                    "story";


                story.innerHTML = `

                    <div class="story-foto">
                        👤
                    </div>

                    <span>
                        ${usuario}
                    </span>

                `;


                stories.appendChild(story);

            }

        }


        // =========================
        // CRIAR POSTS
        // =========================

        function carregarPosts(quantidade) {

            const feed =
                document.getElementById("feed");


            for (let i = 0; i < quantidade; i++) {

                contador++;


                const usuario =
                    gerarUsuario();


                const legenda =
                    gerarLegenda();


                const imagem =
                    gerarImagem();


                const curtidas =
                    Math.floor(Math.random() * 5000);


                const post =
                    document.createElement("article");


                post.className =
                    "post";


                // =========================
                // POST PREMIADO
                // =========================

                if (contador === proximaRecompensa) {

                    post.classList.add(
                        "post-recompensa"
                    );


                    post.innerHTML = `

                        <div class="usuario">

                            <div class="foto-perfil">
                                🪙
                            </div>

                            <strong>
                                recompensa.especial
                            </strong>

                        </div>


                        <div class="recompensa-imagem">
                            🪙
                        </div>


                        <div class="conteudo">

                            <div class="curtidas">
                                🎉 Recompensa encontrada!
                            </div>


                            <strong class="mensagem-recompensa">
                                🎉 Você encontrou uma moeda!
                            </strong>


                            <p>
                                A moeda será adicionada quando
                                você visualizar esta publicação.
                            </p>

                        </div>

                    `;


                    // Observa o post para saber
                    // quando ele aparece na tela

                    observarRecompensa(post);


                    // Define a próxima recompensa

                    proximaRecompensa +=
                        Math.floor(Math.random() * 10) + 5;

                }


                // =========================
                // POST NORMAL
                // =========================

                else {

                    post.innerHTML = `

                        <div class="usuario">

                            <div class="foto-perfil">
                                👤
                            </div>

                            <strong>
                                ${usuario}
                            </strong>

                        </div>


                        <img
                            class="imagem-post"
                            src="${imagem}"
                            alt="Imagem da publicação"
                        >


                        <div class="acoes">

                            <button class="botao curtir">
                                🤍
                            </button>

                            <button class="botao comentar">
                                💬
                            </button>

                            <button class="botao compartilhar">
                                📤
                            </button>

                        </div>


                        <div class="conteudo">

                            <div class="curtidas">

                                <span class="numero-curtidas">
                                    ${curtidas}
                                </span>

                                curtidas

                            </div>


                            <strong>
                                ${usuario}
                            </strong>


                            <p>
                                ${legenda}
                            </p>

                        </div>

                    `;


                    // =========================
                    // BOTÃO DE CURTIR
                    // =========================

                    const botaoCurtir =
                        post.querySelector(".curtir");


                    const numeroCurtidas =
                        post.querySelector(
                            ".numero-curtidas"
                        );


                    let curtido = false;


                    botaoCurtir.addEventListener(
                        "click",

                        () => {

                            let totalCurtidas =
                                Number(
                                    numeroCurtidas.textContent
                                );


                            if (!curtido) {

                                totalCurtidas++;

                                botaoCurtir.textContent =
                                    "❤️";

                                curtido = true;

                            } else {

                                totalCurtidas--;

                                botaoCurtir.textContent =
                                    "🤍";

                                curtido = false;

                            }


                            numeroCurtidas.textContent =
                                totalCurtidas;

                        }

                    );


                    // =========================
                    // BOTÃO COMENTAR
                    // =========================

                    const botaoComentar =
                        post.querySelector(".comentar");


                    botaoComentar.addEventListener(
                        "click",

                        () => {

                            const comentario =
                                prompt(
                                    "Digite seu comentário:"
                                );


                            if (comentario) {

                                const novoComentario =
                                    document.createElement("p");


                                novoComentario.textContent =
                                    "Você: " + comentario;


                                post.querySelector(
                                    ".conteudo"
                                ).appendChild(
                                    novoComentario
                                );

                            }

                        }

                    );


                    // =========================
                    // BOTÃO COMPARTILHAR
                    // =========================

                    const botaoCompartilhar =
                        post.querySelector(
                            ".compartilhar"
                        );


                    botaoCompartilhar.addEventListener(
                        "click",

                        () => {

                            alert(
                                "Post compartilhado!"
                            );

                        }

                    );

                }


                // Adiciona o post ao feed

                feed.appendChild(post);

            }

        }


        // =========================
        // INICIALIZAÇÃO
        // =========================

        carregarStories();

        carregarPosts(10);


        // =========================
        // FEED INFINITO
        // =========================

        window.addEventListener(

            "scroll",

            () => {

                const chegouAoFim =

                    window.innerHeight +
                    window.scrollY >=

                    document.documentElement.scrollHeight - 300;


                if (chegouAoFim) {

                    carregarPosts(10);

                }

            }

        );

    </script>

</body>

</html>
```
