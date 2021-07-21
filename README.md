# ogar-clone

This is a personal project combining https://github.com/m-byte918/MultiOgarII and https://github.com/Cigar2/Cigar2 to run a multiplayer local clone of agar.io on Google cloud compute engine. 


## Summary:

MultiOgarII: is a multiplayer clone of the popular game Agar.io
Cigar2: is the client application users will connect to on port 3000 via vm’s external-ip x.x.x.x:3000 

## How to get it working:

### Create VM
1. Create new gcp instance (Debian GNU/Linux 10 (buster))
2. Make sure allow HTTP/s traffic is enabled
3. Makes sure external IP is static
4. Configure firewall settings to enable ingress and egress on ports: tcp:3000,8080,8888

### Setup
1. `$sudo apt update && upgrade`
2. `$curl -sL https://deb.nodesource.com/setup_14.x | sudo bash -`
3. `$sudo apt-get install -y nodejs`
4. `$node -v  # Make sure this is v14`
5. `$sudo apt install git`
6. `$git clone https://github.com/KD-Long/Ogar-clone.git`
7. Set: Cigar2/web/index.html IP on Line 43 and 44 to the VM external ip
    1. `$cd Ogar-clone/` 
    2. `$nano Cigar2/web/index.html`
         ```
         <option value="your-IP:8888" selected>Stats port 8888</option>
         <option value="your-IP:8080" selected>Game port 8080</option>
         ```
    3. Ctr x -> y to exit and save
8. Install node dependencies MultiOgarII 
    1. `$cd MultiOgarII/`
    2. `$npm i`
    3. `$npm start`
9. Install node dependencies Cigar2 
    1. `$cd ..`
    2. `$cd Cigar2/`
    3. `$npm i`
    4. `$npm start`

### Execute from GCP console
1. Close ssh window and continue from gcp console
2. `$gcloud auth login`
3. `$gcloud compute ssh --zone australia-southeast1-b <your-vm-name> -- '(cd ./Ogar-clone/Cigar2 && nohup npm start &) && (cd ./Ogar-clone/MultiOgarII && npm start)'`
4. Go to “your-external-ip:3000” from any browser to join

