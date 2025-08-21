import os
from zipfile import ZipFile

project_name = "skogsro_stuga_hemsida"
folders = [
    project_name,
    f"{project_name}/images",
    f"{project_name}/css"
]

for folder in folders:
    os.makedirs(folder, exist_ok=True)

index_html = """<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Skogsro Stuga</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <header class="hero">
        <h1>Skogsro Stuga</h1>
        <p>En stuga – fyra årstider av ro</p>
    </header>
    <nav>
        <ul>
            <li><a href="#about">Om Oss</a></li>
            <li><a href="#seasons">Årstider</a></li>
            <li><a href="#gallery">Galleri</a></li>
            <li><a href="#contact">Kontakt</a></li>
        </ul>
    </nav>
    <section id="about">
        <h2>Om Oss</h2>
        <p>Vi hyr ut vår mysiga skogsstuga året runt – ett naturnära boende där varje årstid bjuder på sin egen charm.</p>
    </section>
    <section id="seasons">
        <h2>Stugan genom årstiderna</h2>
        <div class="seasons">
            <div class="season"><h3>Vinter</h3><p>Snötäckta granar, sprakande brasa och längdskidor utanför dörren.</p><img src="images/winter.jpg" alt="Vinter"></div>
            <div class="season"><h3>Vår</h3><p>Blommande ängar, fågelkvitter och vårsol som värmer verandan.</p><img src="images/spring.jpg" alt="Vår"></div>
            <div class="season"><h3>Sommar</h3><p>Bada i sjön, grilla vid solnedgången och njut av långa ljusa kvällar.</p><img src="images/summer.jpg" alt="Sommar"></div>
            <div class="season"><h3>Höst</h3><p>Färgsprakande skogar, svampplockning och krispig höstluft.</p><img src="images/autumn.jpg" alt="Höst"></div>
        </div>
    </section>
    <section id="gallery">
        <h2>Galleri</h2>
        <div class="gallery">
            <img src="images/winter.jpg" alt="Vinter">
            <img src="images/spring.jpg" alt="Vår">
            <img src="images/summer.jpg" alt="Sommar">
            <img src="images/autumn.jpg" alt="Höst">
        </div>
    </section>
    <section id="contact">
        <h2>Kontakt</h2>
        <form>
            <label for="name">Namn:</label>
            <input type="text" id="name" name="name" required>
            <label for="email">E-post:</label>
            <input type="email" id="email" name="email" required>
            <label for="message">Meddelande:</label>
            <textarea id="message" name="message" required></textarea>
            <button type="submit">Skicka</button>
        </form>
    </section>
    <footer>
        <p>© 2025 Skogsro Stuga. Alla rättigheter förbehållna.</p>
    </footer>
</body>
</html>
"""

style_css = """
body {
    font-family: 'Segoe UI', sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f9f6f1;
    color: #333;
}
header.hero {
    background-image: url('../images/hero.jpg');
    background-size: cover;
    background-position: center;
    color: white;
    text-align: center;
    padding: 80px 20px;
}
nav ul {
    display: flex;
    justify-content: center;
    list-style: none;
    background-color: #7a6e5d;
    margin: 0;
    padding: 10px 0;
}
nav ul li {
    margin: 0 15px;
}
nav ul li a {
    color: white;
    text-decoration: none;
    font-weight: bold;
}
section {
    padding: 40px 20px;
    max-width: 1000px;
    margin: auto;
}
.seasons {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
}
.season {
    background-color: #eae4db;
    padding: 15px;
    border-radius: 6px;
    text-align: center;
}
.season img {
    width: 100%;
    height: 180px;
    object-fit: cover;
    border-radius: 4px;
    margin-top: 10px;
}
.gallery {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
}
.gallery img {
    width: 220px;
    height: 160px;
    object-fit: cover;
    border-radius: 4px;
}
form {
    display: flex;
    flex-direction: column;
    gap: 10px;
}
input, textarea {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
}
button {
    background-color: #7a6e5d;
    color: white;
    border: none;
    padding: 10px;
    cursor: pointer;
}
footer {
    background-color: #ddd7ce;
    text-align: center;
    padding: 20px;
}
"""

with open(f"{project_name}/index.html", "w", encoding="utf-8") as f:
    f.write(index_html)

with open(f"{project_name}/css/style.css", "w", encoding="utf-8") as f:
    f.write(style_css)

for img in ["hero.jpg", "winter.jpg", "spring.jpg", "summer.jpg", "autumn.jpg"]:
    with open(f"{project_name}/images/{img}", "wb") as f:
        f.write(b"")

with ZipFile(f"{project_name}.zip", "w") as zipf:
    for root, _, files in os.walk(project_name):
        for file in files:
            filepath = os.path.join(root, file)
            arcname = os.path.relpath(filepath, project_name)
            zipf.write(filepath, arcname)

print("✅ Färdig! Zip-filen 'skogsro_stuga_hemsida.zip' är skapad i samma mapp.")
