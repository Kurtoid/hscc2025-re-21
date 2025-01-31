# Dockerfile and scripts available at https://github.com/Kurtoid/hscc2025
download and extract the tar.gz from the above
> github has a bandwidth limit for large files - if this repo cannot be cloned, here is a backup link: https://nextcloud.kurtw.dev/s/WRmYakwH6mQY4N4

Generate an UPPAAL license key at https://uppaal.veriaal.dk/academic.html
Place the key in `uppaal_key.txt` (without a newline at the end)
build with `docker build -t artifact_eval .`. This takes about 15 minutes on the first run (mostly due to downloading packages) but on subsequent runs (assumuing there have been changes to the scripts) it should take no more than 7 seconds.

`docker run -v ./output:/root/output -it artifact_eval:latest` - will generate Fig. 7. and place the output in the `output` directory. To save time, it will generate 100 tasksets per utilization - this can be changed in `scripts/compare_times.bash`. On a 24-core machine, using 20 cores, it takes about 10 minutes. This uses the `car_timing_queries_automatex.xml` file, which can be opened in UPPAAL. The script generates tasksets, and substitutes them into the model file (on definition lines that begin with `$`). It then runs the model, and extracts the results.

`docker run -v ./output:/root/output -it artifact_eval:latest /bin/bash` - will open a shell in the container

Unfortunately, we did not complete porting of the physics-based models to this container, and do not all run. The drivetest model files are present, and can be viewed in UPPAAL or a text editor.
