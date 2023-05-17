This works only for redmi bootloader, i think?
It works for redmi note 7, 7S, 7 pro.
Aight here's what to do

1. Design your images , you mostly need 3 images
2. The first (1.bmp) is for the general bootloader
3. The second (2.bmp) is for fastboot mode
4. The third (3.bmp) can be a copy of 1.bmp, idk what it does and most don't add it but you can
5. The fourth (4.bmp) is for "System Destroyed", idk what you did to reach here, i am using a stock image from someone else's repo I will link him below.

Now the important steps:

Assuming the images are created in GIMP or Photoshop.

1. Export these images to png files or jpg files
2. Use ImageMagick, a cli to convert the images to 24 bitmap
Command: convert n.png -type truecolor n.bmp
3. This will create a bmp very close to the specific size in bytes that is required.
4. Now remove excess bytes from the end of the file, you can do this by using notepad++
5. The size of each .bmp has to be exactly 7,581,656 bytes

Well images are created, now combine them using this command

Command: cat header.img 1.bmp 2.bmp 3.bmp 4.bmp end.img > splash.img

If you are on windows, then:

Command: copy \b header.img+1.bmp+2.bmp+3.bmp+4.bmp+end.img splash.img

Finally:

We have to zip this image with the META-INF folder provided, it has a updater script

zip -r splash.zip META-INF splash.img

Now flash it using a recovery.

Note: Using fastboot to flash a new splash.img into the splash slot usually wont work because it is filled.