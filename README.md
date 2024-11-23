# FinalTeste
teste 02
<?php
session_start();
require 'config.php';

// Verifica se o usuário está logado e é administrador
$isAdmin = isset($_SESSION['user_role']) && $_SESSION['user_role'] === 'admin';

// Redirecionamento dinâmico para a página de administração
if (isset($_GET['page']) && $_GET['page'] === 'admin' && $isAdmin) {
    include 'admin_dashboard.php';
    exit;
}
?>
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pet Blog</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            background-image: url('https://img.freepik.com/vetores-gratis/fundo-de-impressoes-de-patas-de-design-plano_23-2151169523.jpg');
            background-size: cover;
            background-attachment: fixed;
        }
        .bg-overlay {
            background-color: rgba(255, 255, 255, 0.9);
            padding: 20px;
            border-radius: 10px;
        }
        .pet-icon {
            width: 150px;
            height: 150px;
            object-fit: cover;
            border-radius: 50%;
        }
        .pet-photo {
            width: 100%;
            height: 200px;
            object-fit: cover;
            border-radius: 10px;
        }
        .btn-danger {
            font-weight: bold;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <!-- Navbar -->
    <nav class="navbar navbar-expand-lg navbar-light bg-light bg-overlay">
        <div class="container">
            <a class="navbar-brand" href="#">Pet Blog</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav ms-auto">
                    <?php if ($isAdmin): ?>
                    <li class="nav-item">
                        <a href="?page=admin" class="btn btn-danger me-3">Admin</a>
                    </li>
                    <?php endif; ?>
                    <?php if (!isset($_SESSION['user_id'])): ?>
                    <li class="nav-item">
                        <button class="btn btn-primary me-2" data-bs-toggle="modal" data-bs-target="#loginModal">Entrar</button>
                    </li>
                    <li class="nav-item">
                        <button class="btn btn-outline-primary" data-bs-toggle="modal" data-bs-target="#registerModal">Cadastrar</button>
                    </li>
                    <?php else: ?>
                    <li class="nav-item">
                        <a href="logout.php" class="btn btn-secondary">Sair</a>
                    </li>
                    <?php endif; ?>
                </ul>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <header class="bg-primary text-center py-5">
        <div class="container bg-overlay">
            <h1>Bem-vindo ao Pet Blog</h1>
            <p class="lead">Um espaço para compartilhar e aprender sobre o convívio com nossos amigos peludos</p>
            <a href="#" class="btn btn-light btn-lg mt-3">Conheça o Blog</a>
        </div>
    </header>
 <!-- Sobre Pets Section -->
    <section class="py-5">
        <div class="container bg-overlay">
            <h2 class="text-center mb-5">A Importância do Convívio com Animais de Estimação</h2>
            <style>
                /* Ajuste dos ícones de imagem */
                .pet-icon {
                    width: 150px; /* Define a largura desejada */
                    height: 150px; /* Define a altura desejada */
                    object-fit: cover; /* Ajusta a imagem dentro do contêiner sem distorção */
                    border-radius: 50%; /* Forma circular */
                }
            </style>
            
            <div class="row">
                <div class="col-md-4 text-center">
                    <img src="https://cisavet.com.br/arquivos/banco-de-imagens/categoria-1/dicas-na-hora-de-escolher-um-cao-como-companheiro-20161125143942.jpg" alt="Ícone Companhia" class="pet-icon mb-3">
                    <h4>Companhia e Amizade</h4>
                    <p>Ter um pet traz muita companhia e amizade para o dia a dia, ajudando a combater a solidão e melhorando o humor.</p>
                </div>
                <style>
                    /* Ajuste dos ícones de imagem */
                    .pet-icon {
                        width: 150px; /* Define a largura desejada */
                        height: 150px; /* Define a altura desejada */
                        object-fit: cover; /* Ajusta a imagem dentro do contêiner sem distorção */
                        border-radius: 50%; /* Forma circular */
                    }
                </style>
                
                <div class="col-md-4 text-center">
                    <img src="https://blog-static.petlove.com.br/wp-content/uploads/2021/05/Mulher-gato-no-colo-380x260.jpg" alt="Ícone Redução do Estresse" class="pet-icon mb-3">
                    <h4>Redução do Estresse</h4>
                    <p>Animais ajudam a reduzir o estresse e a ansiedade, criando um ambiente mais calmo e harmonioso.</p>
                </div>
                <style>
                    /* Ajuste dos ícones de imagem */
                    .pet-icon {
                        width: 150px; /* Define a largura desejada */
                        height: 150px; /* Define a altura desejada */
                        object-fit: cover; /* Ajusta a imagem dentro do contêiner sem distorção */
                        border-radius: 50%; /* Forma circular */
                    }
                </style>
                
                <div class="col-md-4 text-center">
                                    <img src="https://vetery.com.br/wp-content/uploads/2023/03/atividades-fisicas-para-seu-pet.jpg" alt="Ícone Atividades Físicas" class="pet-icon mb-3">
                                    <h4>Atividades Físicas</h4>
                                    <p>Com um pet, você se mantém mais ativo, seja em caminhadas com cães ou brincadeiras com gatos e outros animais.</p>
                                </div>
            </div>
        </div>
    </section>
    <!-- Meu Pet Section -->
    <section class="py-5 bg-light">
        <div class="container bg-overlay">
            <h2 class="text-center mb-5">Meu Pet</h2>
            <?php if (isset($_SESSION['user_id'])): ?>
            <div class="row mb-4">
                <div class="col-md-12 text-center">
                    <form action="upload.php" method="POST" enctype="multipart/form-data" class="mb-4">
                        <div class="mb-3">
                            <input type="file" name="photo" class="form-control" required>
                        </div>
                        <button type="submit" class="btn btn-primary">Enviar Foto do Meu Pet</button>
                    </form>
                </div>
            </div>
            <?php endif; ?>
            <div class="row">
                <?php
                $stmt = $pdo->query("SELECT * FROM user_photos ORDER BY uploaded_at DESC");
                $photos = $stmt->fetchAll();
                foreach ($photos as $photo):
                ?>
                <div class="col-md-4 mb-4">
                    <div class="card">
                        <img src="<?= htmlspecialchars($photo['photo_path']); ?>" alt="Foto do Pet" class="pet-photo card-img-top">
                        <div class="card-body text-center">
                            <p class="card-text">Foto enviada por: <?= htmlspecialchars($photo['user_id']); ?></p>
                        </div>
                    </div>
                </div>
                <?php endforeach; ?>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-dark text-light text-center py-4">
        <p class="mb-0">© 2024 Pet Blog - Todos os Direitos Reservados.</p>
    </footer>

    <!-- Modais de Login e Cadastro -->
    <!-- (Os modais de login e cadastro já estão incluídos e permanecem inalterados) -->

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
