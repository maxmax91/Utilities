# Decrypt P7M SSL files with openssl

    openssl.exe cms -decrypt -verify -inform DER -in file.pdf.p7m -noverify -out file.pdf -binary

Don't forget -binary. Without, your output file (PDF?) will be corrupted.

## Batch operation

    cd [target_folder]
    for /r %i in (*.p7m) do openssl.exe cms -decrypt -verify -inform DER -in "%~ni.p7m" -noverify -out "%~ni" -binary
