import os
import zipfile
from PIL import Image, ImageDraw, ImageFont

# Create project structure
base_path = "/mnt/data/portfolio"
images_path = os.path.join(base_path, "images")
os.makedirs(images_path, exist_ok=True)

# index.html content
index_html = """<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ansh Singh | Portfolio</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <h1>🙋‍♂️ Ansh Singh</h1>
    <p><span class="typing">Thumbnail Editor | Graphic Designer | Video Editor | Poster Creator</span></p>
  </header>
  <nav>
    <a href="#about">About</a>
    <a href="#skills">Skills</a>
    <a href="#portfolio">Portfolio</a>
    <a href="#contact">Contact</a>
  </nav>
  <section id="about" class="about">
    <img src="images/profile.jpg" alt="Profile">
    <div>
      <h2>About Me</h2>
      <p>
        Hi, I am <b>Ansh Singh</b>, a creative designer passionate about making 
        eye-catching thumbnails, stunning posters, smooth video edits, and unique graphic designs.  
        My goal is to help brands and creators shine through visuals.
      </p>
    </div>
  </section>
  <section id="skills">
    <h2>💡 My Skills</h2>
    <div class="skills">
      <div class="card">🎨 Thumbnail Editing</div>
      <div class="card">🖌️ Graphic Designing</div>
      <div class="card">🎬 Video Editing</div>
      <div class="card">📰 Poster Creation</div>
    </div>
  </section>
  <section id="portfolio">
    <h2>📂 My Works</h2>
    <div class="portfolio">
      <img src="images/thumb-sample.jpg" alt="Thumbnail Work">
      <img src="images/poster-sample.jpg" alt="Poster Work">
      <img src="images/graphic-sample.jpg" alt="Graphic Work">
      <img src="images/video-sample.jpg" alt="Video Work">
    </div>
  </section>
  <section id="contact">
    <h2>📞 Contact Me</h2>
    <p>Email: <a href="mailto:anshdesigns@gmail.com">anshdesigns@gmail.com</a></p>
    <p>Instagram: <a href="#">@ansh_designs</a></p>
  </section>
  <footer>
    <p>© 2025 Ansh Singh | All Rights Reserved</p>
  </footer>
</body>
</html>
"""

# style.css content
style_css = """@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap');
*{margin:0;padding:0;box-sizing:border-box;font-family:'Poppins', sans-serif;}
body{background:#0f0f0f;color:#eee;line-height:1.6;}
header{background:linear-gradient(135deg,#ff004c,#4500ff);color:#fff;padding:60px 20px;text-align:center;}
header h1{font-size:3rem;animation:fadeInDown 1.2s;}
header p{font-size:1.3rem;color:#ddd;height:35px;}
.typing{display:inline-block;border-right:3px solid #fff;white-space:nowrap;overflow:hidden;
animation:typing 4s steps(30,end), blink .7s step-end infinite alternate;}
@keyframes typing{from{width:0;}to{width:100%;}}
@keyframes blink{50%{border-color:transparent;}}
nav{text-align:center;padding:15px;background:#1c1c1c;position:sticky;top:0;z-index:1000;}
nav a{margin:0 20px;text-decoration:none;color:#fff;font-weight:bold;transition:.3s;}
nav a:hover{color:#ff004c;}
section{padding:60px 20px;max-width:1100px;margin:auto;}
.about{display:flex;flex-wrap:wrap;align-items:center;gap:30px;animation:fadeIn 1.5s;}
.about img{width:230px;border-radius:50%;border:5px solid #ff004c;box-shadow:0 5px 15px rgba(0,0,0,0.6);}
.about h2{color:#ff004c;}
.skills{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:25px;margin-top:40px;}
.card{background:#1c1c1c;padding:25px;border-radius:15px;text-align:center;font-size:1.1rem;
box-shadow:0 4px 12px rgba(0,0,0,0.5);transition:.4s;cursor:pointer;}
.card:hover{transform:translateY(-10px) scale(1.05);background:#ff004c;color:#fff;}
.portfolio{display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:25px;margin-top:40px;}
.portfolio img{width:100%;border-radius:15px;box-shadow:0 5px 15px rgba(0,0,0,0.7);transition:.4s;}
.portfolio img:hover{transform:scale(1.07);filter:brightness(1.2);}
#contact a{color:#ff004c;text-decoration:none;}
#contact a:hover{text-decoration:underline;}
footer{background:#1c1c1c;color:#bbb;text-align:center;padding:20px;margin-top:50px;}
@keyframes fadeIn{from{opacity:0;transform:translateY(20px);}to{opacity:1;transform:translateY(0);}}
@keyframes fadeInDown{from{opacity:0;transform:translateY(-30px);}to{opacity:1;transform:translateY(0);}}
"""

# Save index.html and style.css
with open(os.path.join(base_path, "index.html"), "w") as f:
    f.write(index_html)
with open(os.path.join(base_path, "style.css"), "w") as f:
    f.write(style_css)

# Dummy image generator function
def create_dummy_image(path, text, color):
    img = Image.new("RGB", (400, 300), color=color)
    d = ImageDraw.Draw(img)
    try:
        font = ImageFont.truetype("DejaVuSans-Bold.ttf", 28)
    except:
        font = ImageFont.load_default()
    text_w, text_h = d.textsize(text, font=font)
    d.text(((400-text_w)/2,(300-text_h)/2), text, fill="white", font=font)
    img.save(path)

# Create dummy images
create_dummy_image(os.path.join(images_path, "profile.jpg"), "Profile", "purple")
create_dummy_image(os.path.join(images_path, "thumb-sample.jpg"), "Thumbnail", "red")
create_dummy_image(os.path.join(images_path, "poster-sample.jpg"), "Poster", "blue")
create_dummy_image(os.path.join(images_path, "graphic-sample.jpg"), "Graphic", "green")
create_dummy_image(os.path.join(images_path, "video-sample.jpg"), "Video", "orange")

# Create zip file
zip_path = "/mnt/data/portfolio.zip"
with zipfile.ZipFile(zip_path, 'w') as zipf:
    for root, dirs, files in os.walk(base_path):
        for file in files:
            file_path = os.path.join(root, file)
            arcname = os.path.relpath(file_path, base_path)
            zipf.write(file_path, arcname)

zip_path
