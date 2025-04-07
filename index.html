<?php
// index.php - Reproductor de MP3 con metadatos
session_start();

// Configuración
$password = "asd123"; // Contraseña en texto plano para simplificar
$downloads_dir = 'downloads';

// Crear directorio de descargas si no existe
if (!file_exists($downloads_dir)) {
    mkdir($downloads_dir, 0777, true);
}

// Verificar autenticación
$authenticated = false;
if (isset($_SESSION['authenticated']) && $_SESSION['authenticated'] === true) {
    $authenticated = true;
}

// Procesar inicio de sesión
$login_error = false;
if (isset($_POST['password'])) {
    if ($_POST['password'] === $password) {
        $_SESSION['authenticated'] = true;
        $authenticated = true;
        // Redirigir para evitar reenvío del formulario
        header("Location: " . $_SERVER['PHP_SELF']);
        exit;
    } else {
        $login_error = true;
    }
}

// Función para extraer metadatos de archivos MP3 usando getID3
function extractMetadata($file_path) {
    // Verificar si getID3 está disponible
    if (!class_exists('getID3')) {
        // Si no está disponible, intentamos incluirlo
        if (file_exists('getid3/getid3.php')) {
            require_once('getid3/getid3.php');
        } else {
            // Si no podemos incluirlo, devolvemos datos básicos
            $filename = basename($file_path);
            return [
                'filename' => $filename,
                'title' => pathinfo($filename, PATHINFO_FILENAME),
                'artist' => 'Desconocido',
                'album' => 'Desconocido',
                'year' => '',
                'genre' => '',
                'cover_image' => null,
                'path' => $file_path
            ];
        }
    }
    
    try {
        // Inicializar getID3
        $getID3 = new getID3();
        $file_info = $getID3->analyze($file_path);
        getid3_lib::CopyTagsToComments($file_info);
        
        // Extraer metadatos básicos
        $filename = basename($file_path);
        $title = isset($file_info['comments']['title'][0]) ? $file_info['comments']['title'][0] : pathinfo($filename, PATHINFO_FILENAME);
        $artist = isset($file_info['comments']['artist'][0]) ? $file_info['comments']['artist'][0] : 'Desconocido';
        $album = isset($file_info['comments']['album'][0]) ? $file_info['comments']['album'][0] : 'Desconocido';
        $year = isset($file_info['comments']['year'][0]) ? $file_info['comments']['year'][0] : '';
        $genre = isset($file_info['comments']['genre'][0]) ? $file_info['comments']['genre'][0] : '';
        
        // Extraer imagen de portada si está disponible
        $cover_image = null;
        if (isset($file_info['comments']['picture'][0])) {
            $image_data = $file_info['comments']['picture'][0];
            $cover_image = [
                'data' => base64_encode($image_data['data']),
                'mime' => $image_data['image_mime']
            ];
        }
        
        return [
            'filename' => $filename,
            'title' => $title,
            'artist' => $artist,
            'album' => $album,
            'year' => $year,
            'genre' => $genre,
            'cover_image' => $cover_image,
            'path' => $file_path,
            'duration' => isset($file_info['playtime_string']) ? $file_info['playtime_string'] : ''
        ];
    } catch (Exception $e) {
        // En caso de error, devolvemos datos básicos
        $filename = basename($file_path);
        return [
            'filename' => $filename,
            'title' => pathinfo($filename, PATHINFO_FILENAME),
            'artist' => 'Desconocido',
            'album' => 'Desconocido',
            'year' => '',
            'genre' => '',
            'cover_image' => null,
            'path' => $file_path
        ];
    }
}

// Obtener lista de archivos MP3 con metadatos
$music_files = [];
if ($authenticated) {
    $files = glob($downloads_dir . '/*.mp3');
    if ($files) {
        foreach ($files as $file) {
            $music_files[] = extractMetadata($file);
        }
        
        // Ordenar alfabéticamente por título
        usort($music_files, function($a, $b) {
            return strcasecmp($a['title'], $b['title']);
        });
    }
}
?>

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Reproductor de Música</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            max-width: 1000px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
            color: #333;
        }
        .login-container {
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
            margin-bottom: 20px;
            text-align: center;
        }
        .app-container {
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }
        h1 {
            color: #1db954;
            text-align: center;
            margin-bottom: 30px;
        }
        input[type="password"] {
            width: 100%;
            max-width: 300px;
            padding: 12px;
            margin: 15px 0;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 16px;
        }
        button, input[type="submit"] {
            background-color: #1db954;
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 30px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: background-color 0.3s;
        }
        button:hover, input[type="submit"]:hover {
            background-color: #1ed760;
        }
        .player-container {
            display: flex;
            flex-direction: column;
            margin-bottom: 30px;
        }
        .now-playing-container {
            display: flex;
            align-items: center;
            padding: 20px;
            background-color: #f9f9f9;
            border-radius: 10px;
            margin-bottom: 20px;
        }
        .cover-container {
            width: 150px;
            height: 150px;
            margin-right: 20px;
            background-color: #ddd;
            border-radius: 5px;
            overflow: hidden;
            flex-shrink: 0;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .cover-image {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        .cover-placeholder {
            font-size: 40px;
            color: #aaa;
        }
        .song-info {
            flex-grow: 1;
        }
        .song-title {
            font-size: 24px;
            font-weight: bold;
            margin-bottom: 5px;
            color: #333;
        }
        .song-artist {
            font-size: 18px;
            color: #666;
            margin-bottom: 10px;
        }
        .song-album {
            font-size: 14px;
            color: #888;
        }
        .audio-player {
            width: 100%;
            margin: 15px 0;
        }
        .player-controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 15px 0;
        }
        .control-button {
            background-color: #1db954;
            color: white;
            border: none;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 18px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .control-button:hover {
            background-color: #1ed760;
        }
        .auto-play-toggle {
            display: flex;
            align-items: center;
            margin: 10px 0;
            justify-content: center;
        }
        .auto-play-toggle input {
            margin-right: 10px;
        }
        .music-library {
            margin-top: 30px;
        }
        .music-list {
            list-style-type: none;
            padding: 0;
            margin: 0;
            max-height: 500px;
            overflow-y: auto;
            border: 1px solid #eee;
            border-radius: 5px;
        }
        .music-item {
            padding: 15px;
            border-bottom: 1px solid #eee;
            display: flex;
            align-items: center;
            cursor: pointer;
            transition: background-color 0.2s;
        }
        .music-item:hover {
            background-color: #f0f0f0;
        }
        .music-item.active {
            background-color: #e8f5e9;
            border-left: 4px solid #1db954;
        }
        .music-item-cover {
            width: 50px;
            height: 50px;
            background-color: #ddd;
            border-radius: 3px;
            margin-right: 15px;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .music-item-cover img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        .music-item-info {
            flex-grow: 1;
        }
        .music-item-title {
            font-weight: bold;
            margin-bottom: 3px;
        }
        .music-item-artist {
            font-size: 14px;
            color: #666;
        }
        .music-item-duration {
            color: #888;
            font-size: 14px;
            margin-left: 10px;
        }
        .error {
            color: #e53935;
            margin: 10px 0;
            text-align: center;
        }
        .search-container {
            margin-bottom: 20px;
        }
        .search-input {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 30px;
            font-size: 16px;
            box-sizing: border-box;
        }
        .no-songs {
            text-align: center;
            padding: 30px;
            color: #888;
        }
    </style>
</head>
<body>
    <?php if (!$authenticated): ?>
    <!-- Formulario de inicio de sesión -->
    <div class="login-container">
        <h1>Acceso al Reproductor de Música</h1>
        <form method="post" action="">
            <input type="password" name="password" placeholder="Ingresa la contraseña" required>
            <br>
            <input type="submit" value="Acceder">
            <?php if ($login_error): ?>
                <p class="error">Contraseña incorrecta</p>
            <?php endif; ?>
        </form>
    </div>
    <?php else: ?>
    <!-- Aplicación principal -->
    <div class="app-container">
        <h1>Reproductor de Música</h1>
        
        <!-- Reproductor principal -->
        <div class="player-container">
            <div class="now-playing-container">
                <div class="cover-container" id="cover-container">
                    <div class="cover-placeholder">♪</div>
                </div>
                <div class="song-info">
                    <div class="song-title" id="now-playing-title">Selecciona una canción</div>
                    <div class="song-artist" id="now-playing-artist"></div>
                    <div class="song-album" id="now-playing-album"></div>
                </div>
            </div>
            
            <audio id="central-player" controls class="audio-player">
                <source src="" type="audio/mpeg">
                Tu navegador no soporta el elemento de audio.
            </audio>
            
            <!-- Controles de reproducción -->
            <div class="player-controls">
                <button class="control-button" onclick="playPrevious()">⏮</button>
                <button class="control-button" id="play-pause-btn" onclick="togglePlayPause()">▶</button>
                <button class="control-button" onclick="playNext()">⏭</button>
            </div>
            
            <!-- Opción de reproducción automática -->
            <div class="auto-play-toggle">
                <input type="checkbox" id="auto-play" checked>
                <label for="auto-play">Reproducción automática</label>
            </div>
        </div>
        
        <!-- Biblioteca de música -->
        <div class="music-library">
            <div class="search-container">
                <input type="text" id="search-input" class="search-input" placeholder="Buscar canciones..." oninput="filterSongs()">
            </div>
            
            <?php if (!empty($music_files)): ?>
                <ul class="music-list" id="music-list">
                    <?php foreach ($music_files as $index => $song): ?>
                        <li class="music-item" 
                            data-file="<?php echo htmlspecialchars($song['path']); ?>" 
                            data-title="<?php echo htmlspecialchars($song['title']); ?>"
                            data-artist="<?php echo htmlspecialchars($song['artist']); ?>"
                            data-album="<?php echo htmlspecialchars($song['album']); ?>"
                            data-index="<?php echo $index; ?>"
                            <?php if ($song['cover_image']): ?>
                            data-cover="data:<?php echo $song['cover_image']['mime']; ?>;base64,<?php echo $song['cover_image']['data']; ?>"
                            <?php endif; ?>
                            onclick="playSong(<?php echo $index; ?>)">
                            
                            <div class="music-item-cover">
                                <?php if ($song['cover_image']): ?>
                                <img src="data:<?php echo $song['cover_image']['mime']; ?>;base64,<?php echo $song['cover_image']['data']; ?>" alt="Cover">
                                <?php else: ?>
                                <span>♪</span>
                                <?php endif; ?>
                            </div>
                            
                            <div class="music-item-info">
                                <div class="music-item-title"><?php echo htmlspecialchars($song['title']); ?></div>
                                <div class="music-item-artist"><?php echo htmlspecialchars($song['artist']); ?></div>
                            </div>
                            
                            <?php if (!empty($song['duration'])): ?>
                            <div class="music-item-duration"><?php echo htmlspecialchars($song['duration']); ?></div>
                            <?php endif; ?>
                        </li>
                    <?php endforeach; ?>
                </ul>
            <?php else: ?>
                <div class="no-songs">
                    <p>No hay archivos MP3 en la carpeta de descargas.</p>
                    <p>Por favor, coloca tus archivos MP3 en la carpeta "<?php echo $downloads_dir; ?>".</p>
                </div>
            <?php endif; ?>
        </div>
    </div>
    
    <script>
        // Variables globales para el reproductor
        let currentSongIndex = -1;
        const songs = <?php echo json_encode($music_files); ?>;
        const totalSongs = songs.length;
        const player = document.getElementById('central-player');
        const playPauseBtn = document.getElementById('play-pause-btn');
        
        // Función para reproducir una canción específica
        function playSong(index) {
            if (index >= 0 && index < totalSongs) {
                currentSongIndex = index;
                const song = songs[index];
                
                // Actualizar la fuente del reproductor
                player.src = song.path;
                
                // Actualizar información de la canción
                document.getElementById('now-playing-title').textContent = song.title;
                document.getElementById('now-playing-artist').textContent = song.artist;
                document.getElementById('now-playing-album').textContent = song.album;
                
                // Actualizar imagen de portada
                const coverContainer = document.getElementById('cover-container');
                if (song.cover_image) {
                    coverContainer.innerHTML = `<img class="cover-image" src="data:${song.cover_image.mime};base64,${song.cover_image.data}" alt="Cover">`;
                } else {
                    coverContainer.innerHTML = '<div class="cover-placeholder">♪</div>';
                }
                
                // Reproducir la canción
                player.play()
                    .then(() => {
                        playPauseBtn.textContent = '⏸';
                    })
                    .catch(error => {
                        console.error('Error al reproducir:', error);
                    });
                
                // Marcar la canción activa en la lista
                const songItems = document.querySelectorAll('.music-item');
                songItems.forEach(item => {
                    item.classList.remove('active');
                    if (parseInt(item.dataset.index) === index) {
                        item.classList.add('active');
                        // Hacer scroll para que la canción activa sea visible
                        item.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
                    }
                });
                
                // Actualizar el título de la página
                document.title = `${song.title} - ${song.artist}`;
            }
        }
        
        // Función para alternar entre reproducir y pausar
        function togglePlayPause() {
            if (player.paused) {
                if (currentSongIndex === -1 && totalSongs > 0) {
                    // Si no hay canción seleccionada, reproducir la primera
                    playSong(0);
                } else {
                    player.play();
                    playPauseBtn.textContent = '⏸';
                }
            } else {
                player.pause();
                playPauseBtn.textContent = '▶';
            }
        }
        
        // Función para reproducir la siguiente canción
        function playNext() {
            if (totalSongs > 0) {
                const nextIndex = currentSongIndex >= 0 ? (currentSongIndex + 1) % totalSongs : 0;
                playSong(nextIndex);
            }
        }
        
        // Función para reproducir la canción anterior
        function playPrevious() {
            if (totalSongs > 0) {
                const prevIndex = currentSongIndex >= 0 ? 
                    (currentSongIndex - 1 + totalSongs) % totalSongs : totalSongs - 1;
                playSong(prevIndex);
            }
        }
        
        // Función para filtrar canciones
        function filterSongs() {
            const searchTerm = document.getElementById('search-input').value.toLowerCase();
            const songItems = document.querySelectorAll('.music-item');
            
            songItems.forEach(item => {
                const title = item.dataset.title.toLowerCase();
                const artist = item.dataset.artist.toLowerCase();
                const album = item.dataset.album.toLowerCase();
                
                if (title.includes(searchTerm) || artist.includes(searchTerm) || album.includes(searchTerm)) {
                    item.style.display = '';
                } else {
                    item.style.display = 'none';
                }
            });
        }
        
        // Evento para detectar cuando termina una canción
        player.addEventListener('ended', function() {
            // Verificar si la reproducción automática está activada
            if (document.getElementById('auto-play').checked) {
                playNext();
            }
        });
        
        // Evento para actualizar el botón de reproducción/pausa
        player.addEventListener('play', function() {
            playPauseBtn.textContent = '⏸';
        });
        
        player.addEventListener('pause', function() {
            playPauseBtn.textContent = '▶';
        });
        
        // Teclas de acceso rápido
        document.addEventListener('keydown', function(e) {
            // Evitar acciones si se está escribiendo en un input
            if (e.target.tagName === 'INPUT') return;
            
            switch(e.key) {
                case ' ': // Espacio para reproducir/pausar
                    e.preventDefault();
                    togglePlayPause();
                    break;
                case 'ArrowRight': // Flecha derecha para siguiente canción
                    playNext();
                    break;
                case 'ArrowLeft': // Flecha izquierda para canción anterior
                    playPrevious();
                    break;
            }
        });
    </script>
    <?php endif; ?>
</body>
</html>
