# CodeAlpha_Image-Gallery
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Responsive Image Gallery</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
      background: #f5f5f5;
    }

    h1 {
      text-align: center;
      margin-bottom: 20px;
      color: #333;
    }

    /* Filter Buttons */
    .filter-btns {
      text-align: center;
      margin-bottom: 20px;
    }
    .filter-btns button {
      margin: 5px;
      padding: 8px 16px;
      border: none;
      border-radius: 5px;
      background: #333;
      color: #fff;
      cursor: pointer;
      transition: background 0.3s;
    }
    .filter-btns button:hover {
      background: #555;
    }

    /* Gallery Grid */
    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 15px;
    }

    .gallery img {
      width: 100%;
      height: 200px;
      object-fit: cover;
      border-radius: 10px;
      cursor: pointer;
      transition: transform 0.3s, box-shadow 0.3s;
      box-shadow: 0 4px 8px rgba(0,0,0,0.2);
    }
    .gallery img:hover {
      transform: scale(1.05);
      box-shadow: 0 8px 16px rgba(0,0,0,0.3);
    }

    /* Lightbox */
    .lightbox {
      display: none;
      position: fixed;
      z-index: 9999;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: rgba(0,0,0,0.9);
      justify-content: center;
      align-items: center;
      flex-direction: column;
    }

    .lightbox img {
      max-width: 90%;
      max-height: 80%;
      border-radius: 10px;
      transition: opacity 0.3s ease-in-out;
    }

    /* Buttons */
    .btn {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      font-size: 2rem;
      color: white;
      background: rgba(0,0,0,0.5);
      border: none;
      padding: 10px 20px;
      cursor: pointer;
      border-radius: 50%;
      transition: background 0.3s;
    }
    .btn:hover { background: rgba(255,255,255,0.3); }

    .prev { left: 30px; }
    .next { right: 30px; }

    .close {
      position: absolute;
      top: 20px;
      right: 30px;
      font-size: 2rem;
      color: white;
      cursor: pointer;
    }

    /* Responsive text sizing */
    @media (max-width: 600px) {
      h1 { font-size: 1.5rem; }
      .btn { font-size: 1.5rem; padding: 8px 14px; }
    }
  </style>
</head>
<body>
  <h1>Responsive Image Gallery</h1>

  <!-- Filter Buttons -->
  <div class="filter-btns">
    <button onclick="filterImages('all')">All</button>
    <button onclick="filterImages('nature')">Nature</button>
    <button onclick="filterImages('city')">City</button>
    <button onclick="filterImages('animals')">Animals</button>
  </div>

  <!-- Gallery -->
  <div class="gallery">
    <img src="https://picsum.photos/id/1015/600/400" data-category="nature" alt="Nature 1">
    <img src="https://picsum.photos/id/1016/600/400" data-category="nature" alt="Nature 2">
    <img src="https://picsum.photos/id/1020/600/400" data-category="city" alt="City 1">
    <img src="https://picsum.photos/id/1024/600/400" data-category="animals" alt="Dog">
    <img src="https://picsum.photos/id/1025/600/400" data-category="animals" alt="Horse">
    <img src="https://picsum.photos/id/1031/600/400" data-category="city" alt="City 2">
  </div>

  <!-- Lightbox -->
  <div class="lightbox" id="lightbox">
    <span class="close" id="close">&times;</span>
    <button class="btn prev" id="prev">&#10094;</button>
    <img id="lightbox-img" src="">
    <button class="btn next" id="next">&#10095;</button>
  </div>

  <script>
    const galleryImages = document.querySelectorAll(".gallery img");
    const lightbox = document.getElementById("lightbox");
    const lightboxImg = document.getElementById("lightbox-img");
    const closeBtn = document.getElementById("close");
    const nextBtn = document.getElementById("next");
    const prevBtn = document.getElementById("prev");

    let currentIndex = 0;

    // Open Lightbox
    galleryImages.forEach((img, index) => {
      img.addEventListener("click", () => {
        lightbox.style.display = "flex";
        lightboxImg.src = img.src;
        currentIndex = index;
      });
    });

    // Close Lightbox
    closeBtn.addEventListener("click", () => {
      lightbox.style.display = "none";
    });

    // Next Image
    nextBtn.addEventListener("click", () => {
      currentIndex = (currentIndex + 1) % galleryImages.length;
      lightboxImg.src = galleryImages[currentIndex].src;
    });

    // Previous Image
    prevBtn.addEventListener("click", () => {
      currentIndex = (currentIndex - 1 + galleryImages.length) % galleryImages.length;
      lightboxImg.src = galleryImages[currentIndex].src;
    });

    // Close on background click
    lightbox.addEventListener("click", (e) => {
      if (e.target === lightbox) {
        lightbox.style.display = "none";
      }
    });

    // Filter function
    function filterImages(category) {
      galleryImages.forEach(img => {
        if (category === "all" || img.dataset.category === category) {
          img.style.display = "block";
        } else {
          img.style.display = "none";
        }
      });
    }
  </script>
</body>
</html>
