How install,
Create a folder gallery, upload picture inside this folder
run index.php

if you want zoom picture just click picture to zoom....very simple gallery 40 lines

happy coding :)

the code:

<?php
$repertoire = 'gallery/';
$files = scandir($repertoire);
$images = array_filter($files, function($file) use ($repertoire) {
    $extension = strtolower(pathinfo($file, PATHINFO_EXTENSION));
    return in_array($extension, array('jpg', 'jpeg', 'png', 'gif')) && is_file($repertoire . $file);
});
echo '<div class="image-gallery" style="  display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); grid-gap: 1px;">'; 
foreach ($images as $image) {
    echo '<div class="image-item">';
    echo '<img src="' . $repertoire . $image . '" alt="' . $image . '" class="click-to-zoom" >';
    echo '</div>';
}
echo '</div>'; // Fermeture du container
?>
<script>
document.addEventListener('DOMContentLoaded', function() {
    var images = document.querySelectorAll('.click-to-zoom');
    images.forEach(function(image) {
        image.addEventListener('click', function() {   
            image.classList.toggle('zoomed');
        });
    });
});
</script>
<style>
.click-to-zoom {
    max-width: 100%;
    height: auto;
    display: block;
    transition: transform 0.2s ease-in-out;
}
.click-to-zoom.zoomed {
    transform: scale(1.1); 
    z-index: 999;
    position: absolute;
    top: auto;
    left: 5%;
}
</style>
