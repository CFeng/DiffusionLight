1. Setup proxy on DevServer
alias with-proxy="HTTPS_PROXY=http://fwdproxy:8080 HTTP_PROXY=http://fwdproxy:8080 FTP_PROXY=http://fwdproxy:8080 https_proxy=http://fwdproxy:8080 http_proxy=http://fwdproxy:8080 ftp_proxy=http://fwdproxy:8080 http_no_proxy='\''*.facebook.com|*.tfbnw.net|*.fb.com'\'"

2. Clone the repo
with-proxy git clone https://github.com/CFeng/DiffusionLight.git

3. Create conda environment
with-proxy conda env create -f environment.yml
conda activate diffusionlight

4. install requirements
4.1 Set xformers to version 0.0.33 to avoid the "FATAL: kernel `fmha_cutlassF_f32_aligned_64x64_rf_sm80` is for sm80-sm100, but was built for sm50" error.
4.2 You may need to remove the OpenEXR package from the requirements.txt file and install it manually because of the missing "ImfIO.h" error.
with-proxy pip install -r requirements.txt
conda install -c conda-forge openexr openexr-python

5. Copy your image to the example folder. Make sure it's 1024x1024 and in .png format.

6. Run the scripts
with-proxy python inpaint.py --dataset example --output_dir output
with-proxy python ball2envmap.py --ball_dir output/square --envmap_dir output/envmap
with-proxy python exposure2hdr.py --input_dir output/envmap --output_dir output/hdr
