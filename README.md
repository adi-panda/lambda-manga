# Lambda Manga
##### This is a tutorial for upscaling manga using lambda labs GPUs.

- First create an account on lambda labs webpage

- Start a new instance (a10 is more than enough power for what we need)

- Either create a new ssh key or use an existing one
	- If created new one, save the file somewhere so we can use it later and run:
		```bash
		chmod 600 <YOUR_KEY>.pem
		```
  
- ssh onto your ubuntu with the command provided by lambda labs
	```bash
	ssh -i <YOUR_KEY.pem> ubuntu@<YOUR_IP>
	```
 
- Install gdown to clone the esrgan repository
	```bash
	pip install gdown;
	gdown --folder "https://drive.google.com/drive/folders/1tzDPDQhfW6MOsYs0h0kxJaE6lR77anSr?usp=sharing"
	```

- Back on your computer, copy your input files to the lambda lab server (NAME YOUR FOLDER `input`)
	```bash
	scp -i <YOUR_KEY>.pem "<YOUR_INPUT_FOLDER>" ubuntu@<YOUR_IP>:~/esrgan
	```

- Now ssh back on to your lambda labs server and run the following command:
	```bash
	cd esrgan; 
	pip install -r requirements.txt; 
	python upscale.py models/4x_eula_digimanga_bw_v2_nc1_307k.pth
	```

- Finally, going back onto your local computer, copy the files back to your local

```bash
scp -i <YOUR_KEY>.pem "ubuntu@<YOUR_IP>:~/esrgan/output" "$(pwd)"
```
