# SRGAN_Pytorch
At the first we should create the low resolution images from high resolution.for this part I use this code:

''''python'
from PIL import Image
import os
from google.colab import drive

# Mount Google Drive
drive.mount('/content/drive')

# Path to the input and output images on Google Drive
input_folder_path = '/content/drive/My Drive/HR'
output_folder_path = '/content/drive/My Drive/LR2'

# Ensure the output folder exists
if not os.path.exists(output_folder_path):
    os.makedirs(output_folder_path)

# Iterate through all files in the input folder
for filename in os.listdir(input_folder_path):
    # Check if the file is an image (you can customize the list of supported extensions)
    if filename.lower().endswith(('.png', '.jpg', '.jpeg')):
        # Construct the full paths
        input_image_path = os.path.join(input_folder_path, filename)
        output_image_path = os.path.join(output_folder_path, f"Noisy_LR_{filename}")

        # Open the image from Google Drive
        original_image = Image.open(input_image_path)

        # Perform bicubic downsampling by a factor of 2 (adjust as needed)
        new_width = original_image.width // 2
        new_height = original_image.height // 2
        downsampled_image = original_image.resize((new_width, new_height), Image.BICUBIC)

        # Save the processed image back to Google Drive
        downsampled_image.save(output_image_path)

print("Processing complete.")
'''''
be aware that high resolution images were in HR folder and the LR2 folder cntains Low resolution images. the width and height of images came to //2 by bicubic method which can changed by your need.
