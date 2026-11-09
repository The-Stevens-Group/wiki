You're here because you have an application that only runs on Linux. 

No problem!

Using x2go with Linux has several advantages over Windows-based remote desktops. It's efficient, and most importantly, it lets multiple users connect at the same time, so you don't have to schedule or book a timeslot.

## 1. Request a Linux Account

Please email the Stevens Group IT admin to request a new Linux account. Make sure to **include your MSD account name** in the message.

If you're unsure of your MSD account name, you can find it [here](https://itregister.medsci.ox.ac.uk/sspr/private/login)

Once you receive your account details, please follow the instructions provided to change your password.

## 2. Connect to MSD Network Using MSD VPN

Full instruction can be found [here](https://www.medsci.ox.ac.uk/for-staff/resources/information-technology/document-and-file-storage/vpn).

## 3. Install and Set Up x2go Client

* Download x2go client [here](https://wiki.x2go.org/doku.php/doc:installation:x2goclient). 

  * If you are using a Windows PC, click `Download X2Go for MS Windows™` at the top of the page. If you are using a MAC, click `Download X2Go for OS X™` in the middle of the page.
  * Install the downloaded client following the standard installation steps.

## 4. Configure and Connect via x2go

* Launch the x2go client.
* Click on `Session` → `New Session`.

![image](https://github.com/user-attachments/assets/1c5418d9-3854-4b66-bac6-46a6dcc0fd63)


* Enter the following information:
  * **Session name**: Choose any recognizable name (e.g., `Server`).
  * **Host**: Enter the server hostname or IP address (e.g., `bathspa.dpag.ox.ac.uk` You can see the list of machines available by going [here](https://github.com/The-Stevens-Group/wiki/wiki/Hardware-Resources)).
  * **Login**: Your Linux account username provided by the Stevens Group admin, which should be the same as your MSD account name.
  * **Password**: The password that you received in your Linux account email.
  * **SSH Port**: Set as `22`.
  * **Session Type**: Select `MATE`

![image](https://github.com/user-attachments/assets/f48f9b28-bc4b-4bc8-8687-4f90950dca0d)


* Connect to the Server:
  * Click on your saved session.
  * Enter your Linux account password when prompted.
  * Confirm SSH keys or host authenticity if prompted.

![image](https://github.com/user-attachments/assets/82fb0331-1231-466f-8bfc-76949c79ad0b)
![image](https://github.com/user-attachments/assets/b24aa55f-789a-412c-9ba7-9ac93272b24b)


## 5. Verify Connections

* If you see the following **virtual desktop**, that means you are connected! 

![image](https://github.com/user-attachments/assets/21882c46-e7a4-4d07-81ae-bb896e745bb3)


## 6. Disconnecting (IMPORTANT!)
You can exit by clicking the X button located at the top right. Your ongoing sessions will be preserved for your next login through x2go.

DON'T press `log out` or `shut down` as a bug in the Linux system will prevent your session from closing properly.

