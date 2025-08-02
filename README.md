🔐 Python Password Manager
A secure and minimal local password manager written in Python and MariaDB.
It uses PBKDF2 with SHA-512 to derive a 256-bit key from your MASTER PASSWORD and DEVICE SECRET, which is then used with AES-256 to encrypt and decrypt passwords safely.

⚙️ Installation
This guide is for Linux (Debian-based) systems like Ubuntu or Kali.
Make sure Python 3 and MariaDB are installed before proceeding.

🐍 Install Python Requirements
bash
Copy
Edit
sudo apt update
sudo apt install python3-pip
pip install -r requirements.txt
🛢️ Install MariaDB
bash
Copy
Edit
sudo apt install mariadb-server
Enable and start the service:

bash
Copy
Edit
sudo systemctl enable mariadb
sudo systemctl start mariadb
👤 Create MariaDB User pm
Login to MySQL:

bash
Copy
Edit
sudo mysql -u root
Then, run the following commands in the MariaDB prompt:

sql
Copy
Edit
CREATE USER 'pm'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'pm'@'localhost' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
EXIT;
📋 Fix Clipboard Copy (pyperclip)
If clipboard copy isn't working, install:

bash
Copy
Edit
sudo apt install xclip xsel
🚀 Run
🔧 Configuration
Before first use, configure your environment by setting a MASTER PASSWORD.
This step creates a device secret, initializes the database, and prepares your system.

bash
Copy
Edit
python3 config.py make
This will ask you to enter a master password and automatically set everything up.

⚠️ Reset Configuration
These commands help manage or reset your setup.

bash
Copy
Edit
python3 config.py delete   # Permanently deletes config + all saved entries
python3 config.py remake   # Deletes and re-initializes the configuration
📚 Usage
ℹ️ Help Menu
bash
Copy
Edit
python3 pm.py -h
➕ Add a New Entry
bash
Copy
Edit
python3 pm.py a -s mysite -u mysite.com -e hello@email.com -l myusername
🔎 Retrieve All Entries
bash
Copy
Edit
python3 pm.py e
🔍 Retrieve by Site Name
bash
Copy
Edit
python3 pm.py e -s mysite
🔍 Retrieve by Site Name + Username
bash
Copy
Edit
python3 pm.py e -s mysite -l myusername
📋 Copy Password to Clipboard
bash
Copy
Edit
python3 pm.py e -s mysite -l myusername --copy
🔐 Generate a Random Password
bash
Copy
Edit
python3 pm.py g --length 15
Copies a secure random password (15 characters) to clipboard.

🧠 Notes
All passwords are AES-256 encrypted using a key derived from your MASTER PASSWORD and a DEVICE SECRET.

Your MASTER PASSWORD is never stored anywhere.

If you delete the configuration, all your saved entries are irreversibly lost.
