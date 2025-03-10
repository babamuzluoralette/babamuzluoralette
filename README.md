from moviepy.editor import ImageClip, concatenate_videoclips, AudioFileClip

# Fotoğraf dosya yolları (uzantıları kontrol ediniz, örneğin .jpg veya .png)
image1_path = "file-58m11yyK73AMQLUvcVe9L7.jpg"
image2_path = "file-MHDhxHMuqxHUwZBiL4wycE.jpg"

# 4K çözünürlük: 3840x2160
target_resolution = (3840, 2160)

# Her bir fotoğrafın gösterim süresi (toplamda 15 saniyeye ulaşacak şekilde)
duration_per_image = 7.5  # Toplam 15 saniye için iki eşit bölüm

# Fotoğrafları klip olarak oluşturma ve 4K'ya yeniden boyutlandırma
clip1 = ImageClip(image1_path).set_duration(duration_per_image).resize(newsize=target_resolution)
clip2 = ImageClip(image2_path).set_duration(duration_per_image).resize(newsize=target_resolution)

# Klipleri birleştirme
video = concatenate_videoclips([clip1, clip2], method="compose")

# Arka plan müziğini ekleme (müzik dosyasını video süresine göre kesiyoruz)
audio = AudioFileClip("matushka_phonk.mp3").subclip(0, video.duration)
video = video.set_audio(audio)

# 4K çözünürlükte video çıktısı oluşturma
video.write_videofile("output_edit.mp4", fps=24, codec="libx264")

