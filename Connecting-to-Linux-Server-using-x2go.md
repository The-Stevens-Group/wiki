You're here because you have an application that only runs on Linux. No problem—using x2go with Linux has several advantages over Windows-based remote desktops. It's efficient, and most importantly, it lets multiple users connect at the same time, so you don't have to schedule or book a timeslot.

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
* Click on "Session" → "New Session".

![image](https://github.com/user-attachments/assets/1c5418d9-3854-4b66-bac6-46a6dcc0fd63)


* Enter the following information:
  * **Session name**: Choose any recognizable name (e.g., "Server").
  * **Host**: Enter the server hostname or IP address (e.g., "bathspa.dpag.ox.ac.uk").
  * **Login**: Your Linux account username provided by the Stevens Group admin, which should be the same as your MSD account name.
  * **Password**: The password that you received in your Linux account email.
  * **SSH Port**: Set as 22.
  * **Session Type**: Select `MATE`

![image](https://github.com/user-attachments/assets/3d9dc808-8370-4237-8c45-73f2d2826f66)





