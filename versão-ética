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

        #tempo {
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
           AÇÕES
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


        /* =========================
           FINAL DO FEED
        ========================= */

        #fim-feed {
            display: none;

            text-align: center;

            max-width: 500px;
            margin: 30px auto;

            padding: 30px 20px;

            background: #1c1c1c;

            border: 1px solid #333;
            border-radius: 10px;
        }

        #fim-feed h2 {
            margin-top: 0;
        }


        /* =========================
           BOTÃO CARREGAR MAIS
        ========================= */

        #carregar-mais {
            display: block;

            margin: 30px auto;

            padding: 12px 25px;

            border: none;
            border-radius: 8px;

            background: #444;
            color: white;

            font-size: 16px;
            cursor: pointer;
        }

        #carregar-mais:hover {
            background: #555;
        }


        /* =========================
           AVISO DE PAUSA
        ========================= */

        #aviso-pausa {
            display: none;

            position: fixed;

            left: 50%;
            top: 50%;

            transform: translate(-50%, -50%);

            width: 90%;
            max-width: 400px;

            padding: 25px;

            text-align: center;

            background: #222;

            border: 1px solid #555;
            border-radius: 12px;

            z-index: 2000;
        }

        #aviso-pausa button {
            margin-top: 15px;

            padding: 10px 20px;

            border: none;
            border-radius: 6px;

            background: #555;
            color: white;

            cursor: pointer;
        }


        /* =========================
           RESPONSIVIDADE
        ========================= */

        @media (max-width: 600px) {

            #feed {
                width: 100%;
            }

            .post {
                border-radius: 0;
                border-left: none;
                border-right: none;
            }

            header h1 {
                font-size: 18px;
            }

        }

    </style>

</head>


<body>


    <!-- CABEÇALHO -->

    <header>

        <h1>Meu Feed</h1>

        <div id="tempo">
            ⏱️ 00:00
        </div>

    </header>


    <!-- STORIES -->

    <div id="stories"></div>


    <!-- FEED -->

    <div id="feed"></div>


    <!-- BOTÃO PARA CARREGAR MAIS -->

    <button id="carregar-mais">
        Carregar mais posts
    </button>


    <!-- FINAL DO FEED -->

    <div id="fim-feed">

        <h2>Você viu tudo por hoje! 🎉</h2>

        <p>
            Não há mais publicações disponíveis neste momento.
            Que tal fazer uma pausa e voltar mais tarde?
        </p>

    </div>


    <!-- AVISO DE PAUSA -->

    <div id="aviso-pausa">

        <h2>Que tal fazer uma pausa? ☕</h2>

        <p>
            Você está nesta página há cinco minutos.
            Talvez seja um bom momento para descansar um pouco.
        </p>

        <button id="fechar-aviso">
            Continuar navegando
        </button>

    </div>


    <script>

        // =========================
        // CONFIGURAÇÕES DO FEED
        // =========================

        // Quantidade máxima de posts
        const LIMITE_POSTS = 30;

        // Quantidade carregada por clique
        const POSTS_POR_CARGA = 10;


        // =========================
        // CONTADOR DE TEMPO
        // =========================

        let segundos = 0;

        const contadorTempo = setInterval(() => {

            segundos++;

            const minutos =
                Math.floor(segundos / 60);

            const segundosRestantes =
                segundos % 60;


            document.getElementById("tempo").textContent =
                `⏱️ ${String(minutos).padStart(2, "0")}:${String(segundosRestantes).padStart(2, "0")}`;

        }, 1000);


        // =========================
        // AVISO APÓS 5 MINUTOS
        // =========================

        setTimeout(() => {

            document.getElementById(
                "aviso-pausa"
            ).style.display = "block";

        }, 300000);


        // Fecha o aviso

        document.getElementById(
            "fechar-aviso"
        ).addEventListener("click", () => {

            document.getElementById(
                "aviso-pausa"
            ).style.display = "none";

        });


        // =========================
        // CONTADOR DE POSTS
        // =========================

        let contador = 0;


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

        function carregarPosts() {

            const feed =
                document.getElementById("feed");


            // Verifica quantos posts ainda
            // podem ser carregados

            const restantes =
                LIMITE_POSTS - contador;


            // Define a quantidade desta carga

            const quantidade =
                Math.min(
                    POSTS_POR_CARGA,
                    restantes
                );


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


                post.className = "post";


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
                // BOTÃO DE COMENTAR
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


                // Adiciona o post ao feed

                feed.appendChild(post);

            }


            // =========================
            // VERIFICA O FINAL
            // =========================

            if (contador >= LIMITE_POSTS) {

                document.getElementById(
                    "carregar-mais"
                ).style.display = "none";


                document.getElementById(
                    "fim-feed"
                ).style.display = "block";

            }

        }


        // =========================
        // BOTÃO CARREGAR MAIS
        // =========================

        document.getElementById(
            "carregar-mais"
        ).addEventListener(
            "click",

            carregarPosts

        );


        // =========================
        // INICIALIZAÇÃO
        // =========================

        carregarStories();

        carregarPosts();

    </script>

</body>

</html>
```
