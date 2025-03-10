from moviepy.editor import ImageClip, concatenate_videoclips, AudioFileClip

image1_path = "file-58m11yyK73AMQLUvcVe9L7.jpg"
image2_path = "file-MHDhxHMuqxHUwZBiL4wycE.jpg"


target_resolution = (3840, 2160)

duration_per_image = 7.5  # Toplam 15 saniye için iki eşit bölüm

clip1 = ImageClip(image1_path).set_duration(duration_per_image).resize(newsize=target_resolution)
clip2 = ImageClip(image2_path).set_duration(duration_per_image).resize(newsize=target_resolution)

video = concatenate_videoclips([clip1, clip2], method="compose")


audio = AudioFileClip("matushka_phonk.mp3").subclip(0, video.duration)
video = video.set_audio(audio)


video.write_videofile("output_edit.mp4", fps=24, codec="libx264")

