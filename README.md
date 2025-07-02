24 Electrical 
from zipfile import ZipFile
import os
import shutil

# Redefine paths due to environment reset
uploaded_images = [
    ("/mnt/data/E6051CBA-24E9-41A2-9674-CD710C844D31.jpeg", "portfolio1.jpeg"),
    ("/mnt/data/E5DFD2D8-FC23-442D-85DE-AEB9A75EB5B5.jpeg", "portfolio2.jpeg"),
    ("/mnt/data/DD8758CB-0CCF-4ED8-81F2-D3D7BD10E8DD.png", "portfolio3.png")
]

logo_path = "/mnt/data/A_logo_for_\"24_Electrical\"_is_set_against_a_white_.png"
output_folder = "/mnt/data/24-electrical-custom"
images_folder = os.path.join(output_folder, "images")
os.makedirs(images_folder, exist_ok=True)

# Copy images to final folder
for src, name in uploaded_images:
    shutil.copyfile(src, os.path.join(images_folder, name))

# Copy logo
shutil.copyfile(logo_path, os.path.join(output_folder, "logo.png"))

# Generate customized HTML
custom_html = f"""<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>24 Electrical | Wire You Waiting?</title>
  <style>
    body {{
      margin: 0;
      font-family: Arial, sans-serif;
      background: #f4f4f4;
      color: #333;
    }}
    header {{
      background-color: #001F3F;
      color: #fff;
      padding: 20px 0;
      text-align: center;
    }}
    header h1 {{
      margin: 0;
      font-size: 2.5em;
    }}
    header p {{
      font-style: italic;
      color: #FFA500;
    }}
    nav {{
      text-align: center;
      background-color: #003366;
      padding: 10px 0;
    }}
    nav a {{
      color: #fff;
      margin: 0 15px;
      text-decoration: none;
      font-weight: bold;
    }}
    .hero {{
      background: linear-gradient(to right, #001F3F, #003366);
      height: 250px;
      color: #fff;
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
    }}
    .hero h2 {{
      font-size: 2em;
      padding: 0 20px;
      color: #FFA500;
    }}
    .section {{
      padding: 40px 20px;
      text-align: center;
    }}
    .services {{
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 20px;
      padding-top: 20px;
    }}
    .service {{
      background: #fff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 0 8px rgba(0,0,0,0.1);
    }}
    .logo {{
      width: 150px;
      margin: 20px auto;
    }}
    footer {{
      background-color: #001F3F;
      color: #fff;
      text-align: center;
      padding: 15px 10px;
      margin-top: 40px;
    }}
    .gallery {{
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      gap: 15px;
      margin-top: 20px;
    }}
    .gallery img {{
      width: 300px;
      border-radius: 8px;
    }}
    .social a {{
      margin: 0 10px;
      text-decoration: none;
      font-weight: bold;
      color: #FFA500;
    }}
    .btn {{
      background-color: #FFA500;
      color: #001F3F;
      padding: 10px 20px;
      border-radius: 5px;
      display: inline-block;
      margin-top: 10px;
      text-decoration: none;
      font-weight: bold;
    }}
  </style>
</head>
<body>

  <header>
    <img src="logo.png" alt="24 Electrical Logo" class="logo" />
    <h1>24 Electrical</h1>
    <p>"Wire you waiting?"</p>
  </header>

  <nav>
    <a href="#">Home</a>
    <a href="#services">Services</a>
    <a href="#portfolio">Portfolio</a>
    <a href="#contact">Contact</a>
  </nav>

  <div class="hero">
    <h2>Professional Electrical & Solar Solutions in Harare</h2>
  </div>

  <section class="section" id="services">
    <h2>Our Services</h2>
    <div class="services">
      <div class="service">
        <h3>House Wiring & Tubing</h3>
        <p>Neat, reliable and efficient wiring for homes and buildings.</p>
      </div>
      <div class="service">
        <h3>Solar System Installation</h3>
        <p>Durable and smart solar solutions customized for your needs.</p>
      </div>
      <div class="service">
        <h3>Electrical Repairs</h3>
        <p>From gadgets to systems, we fix it fast and safely.</p>
      </div>
    </div>
  </section>

  <section class="section" id="portfolio">
    <h2>Our Work</h2>
    <div class="gallery">
      <img src="images/portfolio1.jpeg" alt="Project 1" />
      <img src="images/portfolio2.jpeg" alt="Project 2" />
      <img src="images/portfolio3.png" alt="Project 3" />
    </div>
  </section>

  <section class="section" id="contact">
    <h2>Contact Us</h2>
    <p><strong>Phone:</strong> <a href="tel:+263786100586">+263 78 610 0586</a> | 0786100586 / 0719108427</p>
    <p><strong>Email:</strong> <a href="mailto:24electrical@icloud.com">24electrical@icloud.com</a></p>
    <p><strong>Location:</strong> Harare, Zimbabwe</p>
    <a class="btn" href="https://wa.me/263786100586">📱 Chat on WhatsApp</a>
    <div class="social" style="margin-top: 20px;">
      <a href="https://facebook.com/24Electricals" target="_blank">Facebook</a>
      <a href="https://tiktok.com/@24Electrical" target="_blank">TikTok</a>
    </div>
  </section>

  <footer>
    &copy; 2025 24 Electrical. Built with trust and excellence.
  </footer>

</body>
</html>
"""

# Save the HTML file
html_path = os.path.join(output_folder, "index.html")
with open(html_path, "w", encoding="utf-8") as f:
    f.write(custom_html)

# Create the ZIP file
zip_path = "/mnt/data/24-electrical-custom-website.zip"
with ZipFile(zip_path, "w") as zipf:
    for foldername, subfolders, filenames in os.walk(output_folder):
        for filename in filenames:
            file_path = os.path.join(foldername, filename)
            arcname = os.path.relpath(file_path, output_folder)
            zipf.write(file_path, arcname)

zip_path