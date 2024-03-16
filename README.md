# Remove P7M signature from files with openssl

First, cd to the directory you want to process: 

    cd C:\Users\ciccio\files

    openssl.exe cms -decrypt -verify -inform DER -in file.pdf.p7m -noverify -out file.pdf -binary

Don't forget -binary. Without, your output file (PDF?) will be corrupted.

## Batch operation

    cd [target_folder]
    for /r %i in (*.p7m) do openssl.exe cms -decrypt -verify -inform DER -in "%~ni.p7m" -noverify -out "%~ni" -binary

# Sign P7M file with openssl

    openssl cms -sign -outform DER -binary -md sha256 -in document.pdf -out document.pdf.p7m -signer your_priv_certs.crt.pem -inkey your_priv_certs.key.pem -noverify -nodetach
    
## Batch operation 

    cd [target_folder]
    for /r %i in (*.pdf) do openssl cms -sign -outform DER -binary -md sha256 -in "%~ni.pdf" -out "%~ni.pdf.p7m" -signer your_priv_certs.crt.pem -inkey your_priv_certs.key.pem -noverify -nodetach


# ImageMagick Crop Image and assembly into PDF

You can screenshot automatically and assembly a png result using for example [screenshot captor](https://www.donationcoder.com/software/mouser/popular-apps/screenshot-captor).

    magick.exe convert -crop "805x1214" input.png cropped_%d.png
    magick.exe convert -page a4 "cropped_*.png" -quality 100 outfile.pdf



# Winscp

## Replace putty.exe with Windows Terminal using tabs

    wt.exe  -w 0 --title !N plink.exe !U@!@ -i !K -P !#  -t "cd !/ \; /bin/bash --login"
