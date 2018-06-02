### Full example of using **libcurl** with ESP3232

---

Includes examples of using **http**/**https** GET & POST, **ftp** LIST, GET, PUT and sending **EMAIL**

The example uses **wear leveling FAT file system** and the latest **esp-idf** commit has to be used (5. May 2017 or later)

---

Included **libGSM** to test libCurl with GSM modems

---

#### How to build

Configure your esp32 build environment as for other **esp-idf examples**

Clone the repository

`git clone https://github.com/loboris/ESP32_curl_example.git`

Execute menuconfig and configure your Serial flash config and other settings. Included *sdkconfig.defaults* sets some defaults to be used. **Custom partitions table is used!**

Navigate to **Curl Example Configuration** and set your WiFi SSID and password, mail account user name and password, email recipient's mail address. If using **GSM module**, configure GSM parameters.

`make menuconfig`

Edit *testCurl()* function in **testCurl.c** if you want to change some operating parameters.

Make and flash the example.

`make all && make flash`

**All servers used in the example are real working servers.** You can change them if you want to test the responses from your own server(s).

---

#### Example functions

* print info about used **libcurl** version and supported features
* test **http** GET method; sends some parameters and gets response
* test http GET method; requests file and saves the file to file system
* test http GET method; requests large file (~2.4 MB), simulates saving the file to file system
* test **https** GET method; connects to https server using SSL, get the response
* test http POST method; sends 4 parameters including 1 file; gets the response
* test **ftp** LIST directory
* test ftp GET text file; saves the file to the filesystem
* test ftp GET binary file (JPG) to file system
* test ftp PUT binary file from file system (uploads previously downloaded file under different name)
* test **sftp** DOWNLOAD text file from **ssh** server; saves the file to the filesystem
* test sftp UPLOAD jpg file to **ssh** server
* test **SMTP**; sends email with attachment (attaches the jpg file downloaded from ftp server)

The sequence of operation is repeated after 60 second waiting.

If more than 5 consecutive errors are detected, the system is reseted.

While downloading, the files are stored on file system only if they don't already exists. If the file exists, writing to file is simulated. On restart all files on the file system are deleted.
