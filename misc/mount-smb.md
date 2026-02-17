# Mount SMB

### Mount SMB

* `Step 1: Install the CIFS Utils pkg sudo apt-get install cifs-utils`
* `Step 2: Create a mount point sudo mkdir /mnt/local_share`
* `Step 3: Mount the volume sudo mount -t cifs //<vpsa_ip_address>/<export_share> /mnt/<local_share>`
